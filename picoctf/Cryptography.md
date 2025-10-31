
# 1. rsa_oracle

> Can you abuse the oracle? An attacker was able to intercept communications between a bank and a fintech company. They managed to get the message (ciphertext) and the password that was used to encrypt the message. After some intensive reconassainance they found out that the bank has an oracle that was used to encrypt the password and can be found here nc titan.picoctf.net 50994. Decrypt the password and use it to decrypt the message. The oracle can decrypt anything except the password.
## Solution:

- connected to the oracle and chose E,sent the number 2 to get the encrypted version of 2, which is our blinding factor (c_r = 2^e mod n).
- read the password.enc file's contents (c_p) and multiplied it by the blinding factor to get a new "blinded" ciphertext (c_blinded = c_r * c_p).
- chose D and sent the new c_blinded. The oracle decrypted it because it wasn't the original password.
- the oracle returned the decrypted value in hex, converted this hex value to an integer and divided by 2 to get the real password (m_p).
- used the recovered password 3319c with openssl( from hint) to decrypt the secret.enc file, which revealed the flag.
- Code:-
```
from pwn import *

connection = remote('titan.picoctf.net', 50994)
response = connection.recvuntil(b'decrypt.')
print(response.decode())
payload = b'E' + b'\n'

connection.send(payload)

response = connection.recvuntil(b'keysize):')
print(response.decode())
payload = b'\x02' + b'\n'
connection.send(payload)
response = connection.recvuntil(b'ciphertext (m ^ e mod n)')
response = connection.recvline()
num=int(response.decode())*3567252736412634555920569398403787395170577668834666742330267390011828943495692402033350307843527370186546259265692029368644049938630024394169760506488003
response = connection.recvuntil(b'decrypt.')
print(response.decode())
payload = b'D' + b'\n'
connection.send(payload)
response = connection.recvuntil(b'decrypt:')
print(response.decode())
connection.send(str(num)+b'\n')

response = connection.recvuntil(b'hex (c ^ d mod n):')
print(response.decode())
response = connection.recvline()
print(response.decode())
num=int(response,16)//2
print(hex(num))
hex_string=hex(num)[2:]
byte_array=bytes.fromhex(hex_string)
print(byte_array.decode('ascii'))
connection.close()
```

## Flag:

```
picoCTF{su((3ss_(r@ck1ng_r3@_3319c817}
```

## Concepts learnt:

- How to perform an RSA Blinding Attack on a decryption oracle.


## Resources:

- [Cryptography](./https://youtube.com/playlist?list=PLBlnK6fEyqRhBsP45jUdcqBivf25hyVkU)

***


# 2. Custom encryption
> Can you get sense of this code file and write the function that will decode the given encrypted file content. Find the encrypted file here flag_info and code file might be good to analyze and get the flag. 

## Solution:

- Got the encrypted flag, a, b, and a long list of cipher numbers, had to figure out the encryption script  to reverse it.
- The encryption script basically does three things, makes a shared_key using p, g, a, b ,Takes the flag, reverses it ([::-1]), and XORs it with a TEXT_KEY "trudeau", turns each char into its ASCII number and multiplies it by shared_key * KEY_MULTIPLIER (like 311).
- So, I wrote a decryption script to do all these steps backwards, first, I calculated the same shared_key using pow(g, b, p) and pow(v, a, p), then, I took each number in the cipher list and divided it by (shared_key * KEY_MULTIPLIER) to get the ASCII numbers back, converted these numbers back to characters. This gave me the backward, XOR'd string.
- XOR'd this string again with the same TEXT_KEY to get the original flag. Finally, reversed the string ([::-1]) to get the real flag.
- Encryption Script:
```
import sys
import math

def generator(g, x, p):
    return pow(g, x, p)

def decrypt_flag():
    p = 97
    g = 31
    a = 90
    b = 26
    
    KEY_MULTIPLIER = 311
    TEXT_KEY = "trudeau"

    v = generator(g, b, p)
    shared_key = generator(v, a, p)
    
    print(f"Parameters for YOUR challenge (b={b}):")
    print(f"  p = {p}, g = {g}, a = {a}, b = {b}")
    print(f"  Assuming KEY_MULTIPLIER = {KEY_MULTIPLIER} (from video)")
    print(f"  Assuming TEXT_KEY = '{TEXT_KEY}' (from video)")
    print("-" * 30)
    print(f"Calculated v (g^b % p): {v}")
    print(f"Calculated shared key (v^a % p): {shared_key}")

    key_factor = shared_key * KEY_MULTIPLIER
    print(f"Calculated key_factor (shared_key * {KEY_MULTIPLIER}): {key_factor}")

    cipher = [
        61578, 109472, 437888, 6842, 0, 20526, 129998, 526834, 478940, 287364,
        0, 567886, 143682, 34210, 465256, 0, 150524, 588412, 6842, 424204,
        164208, 184734, 41052, 41052, 116314, 41052, 177892, 348942, 218944,
        335258, 177892, 47894, 82104, 116314
    ]

    intermediate_string = ""
    try:
        if key_factor == 0:
            print("Error: key_factor is zero. Cannot decrypt.")
            return

        decoded_chars = []
        for num in cipher:
            if num == 0:
                decoded_chars.append(chr(0))
            else:
                if num % key_factor != 0:
                    print(f"Warning: Number {num} is not divisible by key_factor {key_factor}")
                
                decoded_val = num // key_factor
                decoded_chars.append(chr(decoded_val))
        
        intermediate_string = "".join(decoded_chars)
        print(f"Intermediate (XOR'd) string: {repr(intermediate_string)}")

    except Exception as e:
        print(f"An error occurred during numeric decoding: {e}")
        return

    key_length = len(TEXT_KEY)
    plaintext_reversed = ""
    
    for i, char in enumerate(intermediate_string):
        key_char = TEXT_KEY[i % key_length]
        
        try:
            decrypted_char = chr(ord(char) ^ ord(key_char))
            plaintext_reversed += decrypted_char
        except Exception as e:
            if ord(char) == 0:
                 plaintext_reversed += chr(0 ^ ord(key_char))
            else:
                print(f"Error during XOR: {e}")
                plaintext_reversed += '?'

    print(f"Plaintext (still reversed): {repr(plaintext_reversed)}")

    final_flag = plaintext_reversed[::-1]

    print("-" * 30)
    print("Decryption successful!")
    print(f"Flag: {final_flag.strip()}")

if __name__ == "__main__":
    decrypt_flag()


```

## Flag:

```
picoCTF{custom_d2cr0pt6d_49fbee5b}
```

## Concepts learnt:

- Reversing a custom encryption algorithm.

## Resources:

- [XOR](./https://ctf101.org/cryptography/what-is-xor/)

***

# 3. miniRSA
> Let's decrypt this: ciphertext? Something seems a bit small.

## Solution:

- Got the ciphertext file and saw the public exponent e = 3. This is a classic "Small e Attack." , now if the original message m was small, the mod N in the encryption does nothing, and the formula just becomes c = m^3.
- So, I just had to reverse it: m=cube_root(3)
- I used the gmpy2.iroot(c, 3) function to calculate the integer cube root, converted that resulting big number to hex, and then converted the hex string to ASCII to get the flag.
- Decryption Script:-
```
import gmpy2 
import binascii
c = 2205316413931134031074603746928247799030155221252519872649649212867614751848436763801274360463406171277838056821437115883619169702963504606017565783537203207707757768473109845162808575425972525116337319108047893250549462147185741761825125
N = 29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705309459438099340427770580064400911431856656901982789948285309956111848686906152664473350940486507451771223435835260168971210087470894448460745593956840586530527915802541450092946574694809584880896601317519794442862977471129319781313161842056501715040555964011899589002863730868679527184420789010551475067862907739054966183120621407246398518098981106431219207697870293412176440482900183550467375190239898455201170831410460483829448603477361305838743852756938687673
e = 3

m, perfect_root = gmpy2.iroot(c, 3)

if perfect_root:
    print(f"Found perfect cube root (m)!\n")
    
    m_hex = hex(m)[2:]
    print(f"Hex value: {m_hex}\n")
    
    try:
        # unhexlify turns the hex string into bytes, then we decode it
        flag = binascii.unhexlify(m_hex).decode('utf-8')
        print(f"Decoded flag: {flag}")
    except Exception as e:
        print(f"Could not decode hex to ASCII: {e}")
else:
    print("Ciphertext is not a perfect cube. This attack won't work.")
```
## Flag:

```
picoCTF{n33d_a_lArg3r_e_606ce004}
```

## Concepts learnt:

- RSA "Small e" (low public exponent) attack.


## Resources:

- [RSA encryption](./https://en.wikipedia.org/wiki/RSA_cryptosystem)
***



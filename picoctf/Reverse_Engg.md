# 1. GDB baby step 1
> Can you figure out what is in the eax register at the end of the main function? Put your answer in the picoCTF flag format: picoCTF{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be picoCTF{17}. Disassemble this.
## Solution:

- Make file executable
```
chmod +x target
```
- Open the program in GDB
```
gdb ./target
```
- Disassemble main to see instructions
```
disassemble main

```
- Set breakpoint at the instruction just before ret
```
break *main+<offset>

```
- Run the program
```
run
```
- Check value in eax
```
info registers eax
```

## Flag:

```
picoCTF{549698}
```

## Concepts learnt:

- Using GDB to debug programs (break, run, stepi, info registers).
- Understanding eax holds a function’s return value in x86/x86_64.
- Reading assembly instructions (mov, add, ret) via disassemble.
- Converting hex to decimal for output/flags.


## Resources:

- Intro to Reverse Engineering - https://youtube.com/watch?v=1d-6Hv1c39c
- Reverse Engineering Walkthrough - https://youtube.com/watch?v=gh2RXE9BIN8
- Reverse Engg. Playlist -https://youtube.com/playlist?list=PLMB3ddm5Yvh3gf_iev78YP5EPzkA3nPdL


***

# 2. ARMssembly 1
> For what argument does this program print `win` with variables 83, 0 and 3? File: chall_1.S Flag format: picoCTF{XXXXXXXX} -> (hex, lowercase, no 0x, and 32 bits. ex. 5614267 would be picoCTF{0055aabb})

## Solution:
- Looked at main, it takes command line argument convert it to integer using atoi and call func with that integer
- After func runs, main checks the return value in w0. If w0 is 0, it prints "You win!". If it's anything else, it prints "You Lose :(".
- The function performs a specific calculation using the provided variables.
   -  lsl w0, w1, w0 → This was 83 << 0, which is just 83.

   -  sdiv w0, w1, w0 → This was 83 / 3. Since it's integer division (sdiv), it just drops the remainder, so the result is 27.

   -  sub w0, w1, w0 → This was the final step. It takes the 27 and subtracts our input (let's call it x). So, the function returns 27 - x.
   
- Retutn  value should be 0 so x=27, i.e., 27 is answer. Now, the flag needs to be 32-bit hex, lowercase, and zero-padded, 27 is 1b in hex and after padding 0000001b
    

## Flag:

```
picoCTF{0000001b}
```

## Concepts learnt:

- learned to read basic commands, like mov to copy a value, sdiv to divide, and sub to subtract.

- found out that w0 is the special register used to send a number into a function and also to get the final answer back out.


## Resources:

- Intro to Reverse Engineering - https://youtube.com/watch?v=1d-6Hv1c39c

***

# 3. VaultDoor3
> This vault uses for-loops and byte arrays. The source code for this vault is here: VaultDoor3.java

## Solution:
- The checkPassword() function then rearranges the letters of our input using loops and stores them in a buffer array.
- Reversed that rearrangement process to find the original password.

## Flag:

```
picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_1fb380}

```

## Concepts learnt:

- Learned how to reverse the logic of code that scrambles data.

***

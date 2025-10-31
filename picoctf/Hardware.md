
# 1. IQ Test

> let your input x = 30478191278.

wrap your answer with nite{ } for the flag.

As an example, entering x = 34359738368 gives (y0, ..., y11), so the flag would be nite{010000000011}.

## Solution:

- Given number is 30478191278 in binary it is 11100011000101001000100101010101110
- There are total 36 inputs and 12 outputs. But the binary number we got was 35 digits and not 36. Therefore, a 0 has to be prepended to the given binary number to make it fit into the 36 inputs.
- the input was 011100011000101001000100101010101110 the output was 100010011000
![Solution](https://github.com/user-attachments/assets/efc712ef-d1c0-40cb-b1c2-3f38f2939b42)


## Flag:

```
nite{100010011000}
```

## Concepts learnt:

- Logic Gates


## Resources:

- [Logic Gates](./https://youtu.be/0lwhoQ5aQe8?si=NijIAGrP3jecPxLq)

***
# 2. I like Logic
> i like logic and i like files, apparently, they have something in common, what should my next step be.

## Solution:

- challenge suggested a connection between "logic" and "files." The provided file had .sal which is a part  of a Saleae Logic Analyzer capture.
  [Image1](./<img width="1805" height="923" alt="Screenshot from 2025-10-31 22-47-05" src="https://github.com/user-attachments/assets/5774f574-56e9-4473-b38b-ae5d6e72ff88" />

- considering there's only one channel, it has to be a UART signal, to analyse a UART signal and decode meaningful data from it, we need to know the baud rate. Next step, finding the baud rate to decode the data.
- to calculate baud rate of a signal, you need to find out the lowest time taken for the transmission of the Least Significant Bit in the signal, which is the lowest time for the 'off' signal.
  <img width="1805" height="923" alt="Screenshot from 2025-10-31 22-47-57" src="https://github.com/user-attachments/assets/1158dcfd-92c2-4953-b609-43039cb93a18" />
  
- The shortest bit time measured was 104.16 microseconds, the Baud Rate calculation (Rate = 1/Time) yielded 9600.61 and the nearest standard Baud Rate was 9600.
- The Async Serial Analyzer in the Saleae Logic software was configured with the following parameters:
    - TX Channel: Digital 3
    - Baud Rate: 9600
    - Data Format: 8 data bits, No parity, 1 stop bit .
      

- Running the analyzer successfully decoded a large block of ASCII text from the signal pulses. The flag was found directly embedded within this recovered text.
  
   <img width="558" height="984" alt="Screenshot from 2025-10-31 22-49-39" src="https://github.com/user-attachments/assets/9159166d-15aa-4a3c-abed-0a96c67ef0fb" />

## Flag:

```
FCSC{b1dee4eeadf6c4e60aeb142b0b486344e64b12b40d1046de95c89ba5e23a9925}
```

## Concepts learnt:

- Digital Logic Analysis and Signal Interpretation

- Asynchronous Serial Communication (UART)

## Resources
  [CyberApocolyse 2021](./https://kashmir54.github.io/ctfs/CyberApocalypse2021/)

***
# 3.  Bare Metal Alchemist
> my friend recommended me this anime but i think i've heard a wrong name.
## Solution:

- The file command identified the binary as an AVR 8-bit executable - an Arduino target,atmega328, due to the complexity of the assembly, I used Ghidra decompiler. 
- I decompiled the file using Ghidra to view the code in C, which is much more readable than Assembly.
  <img width="1597" height="750" alt="image" src="https://github.com/user-attachments/assets/2514c211-ce6a-4e6e-9289-19e4d9e8f662" />

- the main function:-
  
```

void main(void)

{
  char cVar1;
  byte bVar2;
  char cVar3;
  undefined1 auStack_7 [3];
  undefined3 uStack_4;
  undefined1 uStack_1;
  
  R1 = 0;
  uStack_1 = Y._1_1_;
  uStack_4 = 0xbe;
  Y = CONCAT11((char)((uint)(auStack_7 + 2) >> 8),(char)auStack_7 + '\x02');
  R25R24._0_1_ = DAT_mem_0044;
  R25R24._0_1_ = (byte)R25R24 | 2;
  DAT_mem_0044 = (byte)R25R24;
  R25R24._0_1_ = DAT_mem_0044;
  R25R24._0_1_ = (byte)R25R24 | 1;
  DAT_mem_0044 = (byte)R25R24;
  R25R24._0_1_ = DAT_mem_0045;
  R25R24._0_1_ = (byte)R25R24 | 2;
  DAT_mem_0045 = (byte)R25R24;
  R25R24._0_1_ = DAT_mem_0045;
  R25R24._0_1_ = (byte)R25R24 | 1;
  DAT_mem_0045 = (byte)R25R24;
  R25R24._0_1_ = DAT_mem_006e;
  R25R24._0_1_ = (byte)R25R24 | 1;
  DAT_mem_006e = (byte)R25R24;
  DAT_mem_0081 = 0;
  R25R24._0_1_ = DAT_mem_0081;
  R25R24._0_1_ = (byte)R25R24 | 2;
  DAT_mem_0081 = (byte)R25R24;
  R25R24._0_1_ = DAT_mem_0081;
  R25R24._0_1_ = (byte)R25R24 | 1;
  DAT_mem_0081 = (byte)R25R24;
  R25R24._0_1_ = DAT_mem_0080;
  R25R24._0_1_ = (byte)R25R24 | 1;
  DAT_mem_0080 = (byte)R25R24;
  R25R24._0_1_ = DAT_mem_00b1;
  R25R24._0_1_ = (byte)R25R24 | 4;
  DAT_mem_00b1 = (byte)R25R24;
  R25R24._0_1_ = DAT_mem_00b0;
  R25R24._0_1_ = (byte)R25R24 | 1;
  DAT_mem_00b0 = (byte)R25R24;
  R25R24._0_1_ = DAT_mem_007a;
  R25R24._0_1_ = (byte)R25R24 | 4;
  DAT_mem_007a = (byte)R25R24;
  R25R24._0_1_ = DAT_mem_007a;
  R25R24._0_1_ = (byte)R25R24 | 2;
  DAT_mem_007a = (byte)R25R24;
  R25R24._0_1_ = DAT_mem_007a;
  R25R24._0_1_ = (byte)R25R24 | 1;
  DAT_mem_007a = (byte)R25R24;
  R25R24._0_1_ = DAT_mem_007a;
  R25R24._0_1_ = (byte)R25R24 | 0x80;
  DAT_mem_007a = (byte)R25R24;
  DAT_mem_00c1 = 0;
  R25R24._0_1_ = DAT_mem_002a;
  R25R24._0_1_ = (byte)R25R24 | 0xf8;
  DAT_mem_002a = (byte)R25R24;
  R25R24._0_1_ = DAT_mem_0024;
  R25R24._0_1_ = (byte)R25R24 | 3;
  DAT_mem_0024 = (byte)R25R24;
  bVar2 = DAT_mem_002a;
  DAT_mem_002a = bVar2 & 0xfb;
  R25R24._0_1_ = DAT_mem_002b;
  R25R24._0_1_ = (byte)R25R24 & 7;
  DAT_mem_002b = (byte)R25R24;
  R25R24._0_1_ = DAT_mem_0025;
  R25R24._0_1_ = (byte)R25R24 & 0xfc;
  DAT_mem_0025 = (byte)R25R24;
  R11 = 0xa5;
  R12 = 0;
  R13 = '\0';
  do {
    R25R24._0_1_ = DAT_mem_0029;
    R25R24._0_1_ = (byte)R25R24 ^ (byte)R25R24 * '\x02';
    if (((byte)R25R24 & 4) == 0) {
      auStack_7 = (undefined1  [3])0x141;
      z1();
    }
    else {
      R15R14 = 0x68;
      R16 = 0;
      while( true ) {
        Z = (byte *)R15R14;
        R25R24._0_1_ = *(byte *)(uint3)R15R14;
        if ((byte)R25R24 == 0) break;
        Z._1_1_ = (undefined1)(R15R14 >> 8);
        Z._0_1_ = (byte)R25R24 ^ R11;
        if ((byte)R25R24 == 0xa5) break;
        R25R24._0_1_ = DAT_mem_0029;
        R25R24._0_1_ = (byte)R25R24 ^ (byte)R25R24 * '\x02';
        if (((byte)R25R24 & 4) == 0) {
          auStack_7 = (undefined1  [3])0x131;
          z1();
          break;
        }
        Z._0_1_ = (byte)Z - 0x30;
        R17 = 0;
        if ((byte)Z < 0x4e) {
          Z = (byte *)CONCAT11(1,(byte)Z);
          R17 = *Z;
        }
        auStack_7 = (undefined1  [3])0x151;
        z1();
        if ((R17 & 1) != 0) {
          bVar2 = DAT_mem_002b;
          DAT_mem_002b = bVar2 | 8;
        }
        if ((R17 & 2) != 0) {
          bVar2 = DAT_mem_002b;
          DAT_mem_002b = bVar2 | 0x10;
        }
        if ((R17 & 4) != 0) {
          bVar2 = DAT_mem_002b;
          DAT_mem_002b = bVar2 | 0x20;
        }
        if ((R17 & 8) != 0) {
          bVar2 = DAT_mem_002b;
          DAT_mem_002b = bVar2 | 0x40;
        }
        if ((R17 & 0x10) != 0) {
          bVar2 = DAT_mem_002b;
          DAT_mem_002b = bVar2 | 0x80;
        }
        if ((R17 & 0x20) != 0) {
          bVar2 = DAT_mem_0025;
          DAT_mem_0025 = bVar2 | 1;
        }
        if ((R17 & 0x40) != 0) {
          bVar2 = DAT_mem_0025;
          DAT_mem_0025 = bVar2 | 2;
        }
        R25R24._0_1_ = R16 & 0x1f;
        cVar3 = (byte)R25R24 + 0x2d;
        while (cVar1 = cVar3 + -1, cVar3 != '\0') {
          Z = (byte *)0xf9f;
          do {
            Z = (byte *)((int)Z + -1);
            cVar3 = cVar1;
          } while (Z != (byte *)0x0);
        }
        R15R14 = CONCAT11(R15R14._1_1_ - (((char)R15R14 != -1) + -1),(char)R15R14 + '\x01');
        R16 = R16 + 0x25;
      }
      *(byte *)(Y + 2) = R1;
      *(byte *)(Y + 1) = R1;
      while( true ) {
        R25R24._0_1_ = *(byte *)(Y + 1);
        R25R24._1_1_ = *(char *)(Y + 2);
        if (R25R24._1_1_ != '\0' && ((byte)R25R24 < 0x2c) <= (byte)(R25R24._1_1_ - 1U)) break;
        R25R24 = *(int *)(Y + 1) + 1;
        *(char *)(Y + 2) = R25R24._1_1_;
        *(byte *)(Y + 1) = (byte)R25R24;
      }
    }
    if (R12 != R1 || R13 != (byte)(R1 + (R12 < R1))) {
      auStack_7 = (undefined1  [3])0x146;
      __vectors();
    }
  } while( true );
}
```
- looked in the main function and found the encryption steps
    - The code set a secret number: R11 = 0xa5
    - The code pointed to where the encrypted text started:R15R14 = 0x68 
- The program logic executed a single-byte XOR against the data stream,so extracted the raw hexadecimal sequence from memory address 0x68 and performed the final decryption using Python script and flag found.
- Code:-
```
XOR_KEY = 0xA5

hex_data = "F1 E3 E6 E6 F1 E3 DE F1 CD 94 D6 FA 94 D6 FA D6 CA C8 96 FA D6 94 C8 D5 C9 96 FA 91 D7 C1 D0 94 CB CA FA C3 94 D7 C8 D2 91 D7 C0 D8 00"

decrypted_chars = []

for hex_byte in hex_data.split():
    if hex_byte:
        int_value = int(hex_byte, 16)

        decrypted_value = int_value ^ XOR_KEY

        decrypted_char = chr(decrypted_value)

        decrypted_chars.append(decrypted_char)

        if int_value == 0:
            break

flag = "".join(decrypted_chars).strip('\x00')

print(f"Decrypted Flag: {flag}")

```
## Flag:

```
TFCCTF{Th1s_1s_som3_s1mpl3_4rdu1no_f1rmw4re}
```

## Concepts learnt:

- AVR Firmware Reverse Engineering.


***

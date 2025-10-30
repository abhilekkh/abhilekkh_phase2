
# 1. Trivial Flag Transfer Protocol  

 > Figure out how they moved the flag.

## Solution:

- Opened the pcap file with wireshark
- found instruction.txt, plan and others, used tftp.type == octet and exported then to a folder
- opened the instruction file, used base64 and then rot13 got the first hint
- hint mentioned plan, opened plan file again used rot13 got the final hint
- used steghide (used this cause of hint) to extract each image then the 3rd image gave flag.txt


## Flag:

```
picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}
```

## Concepts learnt:

- Learnt how to use wireshark


## Resources:

- [Wireshark Tutorial](./https://www.youtube.com/watch?v=qTaOZrDnMzQ)

***


# 2. tunn3l v1s10n
>  We found this file. Recover the flag.

## Solution:

- downloaded the file, couldn't open, used file command it showed data, then used exiftool and found its a bmp file
- Opened in a hex editor and corrected the DIB Header Size bytes at offset 0x0E to the standard 28 00 00 00. The image then opened showing a decoy flag
- noticed the offset at 0x0A was unusually large BA D0 00 00 = 53434 bytes, standard is 36 00 00 00 = 54 bytes
- guessed that the large offset, combined with the decoy flag, meant that the declared image width or height was smaller than actual image
- increased the image height bytes at 0x16 to 32 03 00 00, saving and opening the modified BMP revealed the flag visually in the expanded upper section.

## Flag:

```
picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}
```

## Concepts learnt:

- Basic BMP header structure (Info Header Size, Image Height)


## Resources:

- [John Hammond-CTF katana](./https://github.com/JohnHammond/ctf-katana?tab=readme-ov-file#forensics)
- [Hex Editor](./https://hexed.it/)
***


# 3. m00nwalk
>  Decode this message from the moon.
## Solution:

- downloaded message.wav,played it, it was just static and beeps

- the first hint mentioned moon landing pictures, searched online and found out NASA used SSTV to send images using sound signals, hence the sound file must have a hidden picture.

- needed software to turn the sound back into a picture, found one called QSSTV for Linux 

- installed and opened QSSTV the QSSTV program,played the message.wav file,and it started drawing the picture.

- then the sound finished, QSSTV showed the full decoded picture, and the flag was clearly visible on it
## Flag:

```
picoCTF{beep_boop_im_in_space}
```

## Concepts learnt:

- how to use QSSTV to decode SSTV signals.


## Resources:

- [John Hammond-CTF katana](./https://github.com/JohnHammond/ctf-katana?tab=readme-ov-file#forensics)
***

# Re: Draw

>Description
Her screen went black and a strange command window flickered to life... She was drawing when it happened, and remnants of a painting program linger.

## Solution
- Stage 1: ran the consoles plugin in Volatility. The first flag was just sitting there in the command history.
- Stage 2: Saw mspaint.exe in the process list. Dumped its memory using memdump. Opened the raw .dmp file in GIMP, treated it as "Raw Image Data," and adjusted the width slider until the drawing appeared. Read the flag written on the canvas.
- Stage 3: Used hashdump to get the user hashes. Cracked Alissa’s hash online to get the password goodmorningindia. Then used filescan to find a hidden rar file, extracted it, and unzipped it with that password.

## Flag:
```
Stage 1: flag{th1s_1s_th3_1st_st4g3!!}
Stage 2: flag{pa1nt_1s_lov3_pa1nt_1s_l1f3}
Stage 3: flag{w3ll_3rd_stage_was_easy}
```

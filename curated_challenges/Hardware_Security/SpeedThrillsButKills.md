# Speed Thrills But Kills
> Description
i recently got involved in a hit and run case in pune, that kids porsche was going wayy too fast, if only i knew what the VIN of the car was :(

## Solution:
- The challenge mentioned a "VIN" (Vehicle Identification Number), which immediately tipped me off that this was a car hacking challenge.
- Cars use a specific network to talk internally called CAN Bus (Controller Area Network).I opened the signal file and saw the classic differential signal structure—two wires interacting with "Dominant" (0) and "Recessive" (1) states.
- To decode the data, I needed to know how fast it was being sent (the baud rate). Since I didn't know it, I had to calculate it manually.
- I zoomed way in on the digital waveform to find the shortest pulse I could see (the time for a single bit).
- I measured it at roughly 8.34 microseconds.I did the math: 1 / 0.00000834 seconds came out to about 119,904 bits per second.That number seemed a bit messy.
- I know standard CAN speeds are usually clean numbers like 125 kbps, 250 kbps, or 500 kbps. Since 119k is closest to 125k, I assumed that was the intended speed.
- I set up a CAN analyzer in the software with a baud rate of 125000, and it worked perfectly. The raw signals translated into text, and I found the flag hidden in the decoded packets.
<img width="1257" height="403" alt="image" src="https://github.com/user-attachments/assets/aa8ba347-23c4-4637-a8be-d1dd1e49326d" />
<img width="523" height="346" alt="image" src="https://github.com/user-attachments/assets/f9605c75-4f4a-4d23-a3c2-6bb982f95f27" />
<img width="291" height="414" alt="image" src="https://github.com/user-attachments/assets/56fd7efa-6a59-45b4-acd8-118c5cf8cb74" />

## Flag:
```
HTB{v1n_c42_h4ck1n9_15_1337!*0^}
```

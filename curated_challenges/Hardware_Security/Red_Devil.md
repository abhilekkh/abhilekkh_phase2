# Red Devil

>Description
this is the worst football team ever(i dont even watch football lmeow)

## Solution:
- Provided with signal.cf32, a raw SDR data file containing Complex Float 32-bit data (unprocessed I/Q samples).
- Opened the file in inspectrum to analyze the waveform.
- Observed the waveform showed amplitude shifting, indicating Amplitude Shift Keying (ASK) modulation where amplitude levels represent binary values.
- Imported the file into Universal Radio Hacker (URH) for demodulation.
- Zoomed into the signal in URH to confirm the ASK nature, selected "ASK" modulation, and clicked Autodetect Parameters to find the sample size.
- Switched to the Analysis tab in URH to test various encoding schemes (like NRZ, Manchester I, etc.).
- Successfully decoded the signal using Manchester II encoding, which revealed the flag.
<img width="1616" height="741" alt="image" src="https://github.com/user-attachments/assets/af36e766-8b57-45db-a173-fef19f79c240" />
<img width="1919" height="1037" alt="image" src="https://github.com/user-attachments/assets/59ab67eb-9f62-4348-a5bc-d57fa7b77279" />
<img width="614" height="343" alt="image" src="https://github.com/user-attachments/assets/5c660414-2354-4a14-965e-54e0b98fb8c6" />
<img width="238" height="329" alt="image" src="https://github.com/user-attachments/assets/15d1eaac-e62a-44f2-81c4-d18388aa2a99" />
<img width="1918" height="693" alt="image" src="https://github.com/user-attachments/assets/3410da20-6b6d-415c-a8e9-963d14b927c8" />

## Flag:
```
HTB{RF_H4ck1n6_1s_c00l!!!}
```

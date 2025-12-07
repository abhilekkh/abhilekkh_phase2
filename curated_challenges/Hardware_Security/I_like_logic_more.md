# i-like-logic more

>Description:
idk man, i feel like microsd cards are a thing of the past.

## Solution:
- Received a .sal file, which is a capture file for Saleae Logic analyzers.
- Since the description mentioned "microsd cards," I looked up their communication protocols and found they often use SPI (Serial Peripheral Interface).
- Opened the file in Saleae Logic 2.
- Analyzed the waveforms to identify the 4 SPI lines:
- Channel 3 was pulsing steadily, so that's the Clock.Channel 2 stayed low during transactions, identifying it as Enable (Chip Select).
- Channel 0 and Channel 1 were the data lines (MOSI/MISO).
- Added an SPI Analyzer in the software with the mapping: MOSI=0, MISO=1, Enable=2, Clock=3.
- The analyzer decoded the bits into text, revealing the flag.
<img width="1919" height="1042" alt="sig1" src="https://github.com/user-attachments/assets/42a1eec6-c4d8-4a94-9aae-a2febadea221" />
<img width="522" height="618" alt="spi_anal" src="https://github.com/user-attachments/assets/34bb95e7-9092-4367-96db-9eeb4cf91249" />
<img width="1914" height="1036" alt="logic" src="https://github.com/user-attachments/assets/60bfb65e-b4f1-4d6c-852f-4a91567e7d22" />

## Flag:
HTB{unp2073c73d_532141_p2070c015_0n_53cu23_d3v1c35}

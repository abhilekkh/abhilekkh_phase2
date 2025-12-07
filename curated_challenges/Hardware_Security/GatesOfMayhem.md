# Gates of Mayhem
>Description
iqtest but its on steriods and you have weird aah inputs aswell.
<img width="1212" height="855" alt="image" src="https://github.com/user-attachments/assets/c35faf9e-63b7-4eb5-9e5b-b6b7f2778cc5" />

## Solution:
- I started with the gates_of_mayhem.pdf schematic and the input_sequence.csv.
- The schematic looked like a mess of electronic components, so I googled the part number BC107. Turns out, they are NPN transistors.
- Since the input was just 1s and 0s, I realized this was actually a logic circuit built from scratch using transistors.
- I traced the wiring to figure out what gates they were forming:
- IN1 and IN2 were wired in series, which acts like an AND gate.
- IN5 and IN6 were wired in parallel, which is a classic OR gate.
- The middle section was a bit trickier, but after staring at it for a while, I recognized it as an XOR gate configuration.
- Once I had the logic mapped out—Output = (IN1 & IN2) XOR ((IN3 & IN4) & (IN5 | IN6))—I didn't want to calculate thousands of lines manually.
- I wrote a quick Python script to run the CSV inputs through that logic equation, turned the resulting binary into text, and got the flag.
```
import csv

with open('input_sequence.csv', 'r') as f:
    
    next(f)
    reader = csv.reader(f)
    
    bits = []
    for row in reader:
        
        i1, i2, i3, i4, i5, i6 = map(int, row)
        
        
        val = (i1 & i2) ^ ((i3 & i4) & (i5 | i6))
        bits.append(str(val))

binary_string = "".join(bits)

n = int(binary_string, 2)
print(n.to_bytes((n.bit_length() + 7) // 8, 'big').decode())
```
## Flag:
```
citadel{1_l0v3_t0_3xpl01t_l0g1c}
```

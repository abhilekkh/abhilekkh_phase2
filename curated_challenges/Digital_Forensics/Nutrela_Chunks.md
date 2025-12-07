
# Nutrela Chunks

 > Description:

One of my favorite foods is soya chunks. But as I was enjoying some Nutrela today, I noticed a few chunks weren’t quite right. Seems like something’s off with their structure. Could you help me fix these broken chunks so I can enjoy my meal again?

## Solution:

- the question hinted at `broken chunks` and the png file wasn't opening so I opened image using Hex Editor
- compared the usual PNG file structure and found that file header is case sensitive and corrected the headers- png,ihdr,idat and iend
- opened the image and found the flag
  <img width="988" height="948" alt="Screenshot_20251207_134317" src="https://github.com/user-attachments/assets/5bcea375-879b-4125-80ce-1202fd95f3cc" />


## Flag:

```
nite{n0w_y0u_kn0w_ab0ut_PNG_chunk5}
```

## Concepts learnt:

- learnt about png file structure


## Resources:

- [PNG File structure](./https://medium.com/@0xwan/png-structure-for-beginner-8363ce2a9f73)

***

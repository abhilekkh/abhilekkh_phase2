
# Hide and Seek

>Description:

Sakamoto’s at it again with a game of hide and seek, but this time, it’s not with Shin or his daughter. An old friend hid some secret data in this image. Can you find it before the others do?

Hint:
Even in retirement, Sakamoto never loses at hide and seek. Maybe stegseek can help you keep up.

## Solution:

- Downloaded the image sakamoto.jpg then installed `stegseek` using the hint
- found `stegseek` is a steganography extractor which use wordlists to crack password of a steg file.
- used rockyou.txt as its commonly used.
- Used
  ```
  [abhilekkh@archlinux Downloads]$ stegseek sakamoto.jpg
  StegSeek 0.6 - https://github.com/RickdeJager/StegSeek

  [i] Found passphrase: "iloveyou1"
  [i] Original filename: "flag.txt".
  [i] Extracting to "sakamoto.jpg.out".
  ```
- opened sakamoto.jpg.out and found flag

## Flag:

```
nite{h1d3_4nd_s33k_but_w1th_st3g_sdfu9s8}

```

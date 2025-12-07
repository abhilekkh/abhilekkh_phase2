# RAR of the Abyss 

 > Description:

Two philosophers peer into the networked abyss and swap a secret. Use the secret to decrypt the Abyss’ RAwR and pull your flag from the void.

## Solution:

- used `strings abyss.pcap` it gave
   ```
  Camus: One must imagine Sisyphus happy but are we happy ?
  Nietzsche: You will be happy after reading my latest work
  Rar!
  wOdp
  Camus: whats the password ?
  Nietzsche: b3y0ndG00dand3vil
  Camus: thanks
  ```
- used `binwalk -e abyss.pcap` then did `unrar x abyss_dump.rar`
- got flag.txt file


## Flag:

```
nite{thus_sp0k3_th3_n3tw0rk_f0r3ns1cs_4n4lyst}

```


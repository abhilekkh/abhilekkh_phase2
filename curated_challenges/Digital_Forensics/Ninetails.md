
# Ninetails

 >Description:

Looks like I got a little too clever and hid the flag as a password in Firefox, tucked away like one of NineTails’ many tails. Recover the "logins" and the "key4" and let it guide you to the flag.

Hint:
I named my Ninetails "j4gjesg4", quite a peculiar name isn't it?

## Solution:

- Identified that the challenge files logins.json and key4.db are Firefox profile data used to store saved credentials.

- Noted the hint "VI named my Ninetails 'j4gjesg4'", which indicated the Master Password for the browser profile.

- Downloaded firefox_decrypt, a python tool for extracting passwords from Mozilla profiles.

- Ran the tool against the profile folder and authenticated using the master password j4gjesg-4.

- Extracted partial flags from the password fields of three different sites (rehack.xyz, reddit.com, warlocksmurf.github.io).

- Concatenated the password segments to form the final flag.

## Flag:

```
GCTF{m0zarella_f1ref0x_p4ssw0rd}
```

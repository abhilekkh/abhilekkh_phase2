# Formwear

> Description
this is most definitely going to ring some bells for those who attended the "router hijacking" workshop L0L

## Solution:
- Analyzed the extracted challenge files (fwu_ver, hw_ver, rootfs) and identified rootfs as a Squashfs filesystem using the file command.
- Mounted the filesystem image to a local directory (/mnt/mounted) to explore the firmware's directory structure.
- Focused the investigation on the /etc directory, as it typically contains system configuration files in Linux-based router firmware.
- Noted the absence of a standard /etc/shadow file and instead found configuration data stored in XML format.
- Searched the configuration files for sensitive keywords by running grep "PASSWORD" config_default.xml.
- Discovered the SUSER_PASSWORD (Super User Password) entry, which contained the flag.

## Flag:
```
HTB{N0w_Y0u_C4n_L0g1n}
```

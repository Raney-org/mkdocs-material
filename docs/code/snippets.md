---
tags:
  - CODE
  - SNIPPETS
---

# yut

This can be adjusted as needed for your particular usecase, this helped me with my Hetzner server when I was messing with netplan. I was changing my nameservers from hetzner to cloudflare due to google blocking a giant block of IPs from hetzner. Well I screwed it up as per usual, and got locked out of the server. It wouldn't boot, so I had to ssh in on rescue mode and do some fun stuff.

```bash
mount /dev/<root partition device> /mnt
mount /dev/<boot partition device> /mnt/boot <-- may need /mnt/boot/efi depending on the board

mount -t proc /proc /mnt/proc
mount -t sysfs /sys /mnt/sys
mount -o bind /dev /mnt/dev
mount -o bind /dev/pts /mnt/dev/pts
mount -o bind /run /mnt/run
chroot /mnt
```

Heres another example of the same thing, done in a different way:

```bash
mount /dev/mapper/vg0-root /mnt 
chroot-prepare /mnt 
chroot /mnt
```

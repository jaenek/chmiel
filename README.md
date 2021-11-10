1. Disk Partitioning.
```sh
lsblk          # shows connected disks
fdisk /dev/sdX # disk formatter

# For efi setup:
#   /boot - boot partition (512M) type FAT(#1 fdisk option)
#   /     - root partition type ext4(#83(default) fdisk option)
#   /home - optional home partition same as /
# For mbr:
#   /     - root partition type ext4(#83(default) fdisk option)
#   /home - optional home partition same as /

mkfs.fat -V /dev/sdaX # format boot partition
mkfs.ext4 /dev/sdaX   # format linux paritions
```

2. Mount drives.
```sh
mount /dev/sdaX /mnt  # mount / partition
```

3. Setup /etc/pacman.d/mirrorlist.
```sh
reflector --latest 200 --protocol http,https --sort rate --save /etc/pacman.d/mirrorlist
```

4. Install essential packages.
```sh
pacstrap /mnt base base-devel linux linux-firmware grub sudo efibootmgr
```

5. Generate fstab.
```sh
genfstab -U /mnt >> /mnt/etc/fstab
```

6. Change root into the new system.
```sh
arch-chroot /mnt
```

7.
```sh
ln -sf /usr/share/zoneinfo/Europe/Warsaw /etc/localtime
```

8.
```sh
hwclock --systohc
```

9.
```sh
echo en_US.UTF-8 UTF-8 > /etc/locale.gen
locale-gen
```
10.
```sh
echo LANG=en_US.UTF-8 > /etc/locale.conf
```

11.
```sh
echo KEYMAP=pl > /etc/vconsole.conf
```

12.
echo <hostname> > /etc/hostname

13.
```sh
mkinitcpio -P
```

14.
```sh
passwd
```

15.
```sh
grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=grub maybe add OS_PROBER
grub-mkconfig -o /boot/grub/grub.cfg
```

19.
```sh
reboot
```

21.
```sh
echo -e "[Match]\nName=e*\n\n[Network]\nDHCP=yes" > /etc/systemd/network/10-wired.network, ip set link <int> up
```

Add to chmiel.sh:
 - add files and folders to cache which are not created for status, python and maybe other

ln -sf /usr/share/zoneinfo/Europe/Warsaw /etc/localtime
hwclock --systohc
nvim /etc/inputrc uncomment set vbell off
nvim /etc/locale.gen uncomment en_US.UTF-8 UTF-8
locale-gen
echo "LANG=en_US.UTF-8" > /etc/locale.conf
echo -e "KEYMAP=pl\nFONT=lat2-16\nFONT_MAP=8859-2" > /etc/vconsole.conf
cat "legion" > /etc/hostname
echo "legion" > /etc/hostname
nvim etc/hosts set hosts 127.0.0.1
mkinitcpio -P
passwd
mkdir efi
mount /dev/sda1 /efi
grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=grub
grub-mkconfig -o /boot/grub/grub.cfg

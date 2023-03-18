# alpine-linux
# Installation instructions

fdisk
1) Min. create two partition for uefi mode
 boot - 256 - 512MB
 root - for all alpine system

apk add e2fsprogs

mean that
boot - /dev/sda5
root - /dev/sda6

mkfs.vfat /dev/sda5
mkfs.ext4 /dev/sda6

apk add grub-efi
apk add efibootmgr

mount -t ext4 /dev/sda6 /mnt
mkdir -p /mnt/boot/efi
mount -t vfat /dev/sda5 /mnt/boot/efi

apk del syslinux

setup-alpine
Last questions - none start from disk

setup-disk -m sys /mnt

# install xfce4
apk update
setup-xorg-base
apk add xfce4 xfce4-terminal xfce4-screensaver lightdm-gtk-greeter dbus
rc-service dbus start
rc-update add dbus
rc-update add lightdm
rc-service lightdm start

apk upgrade --available && sync

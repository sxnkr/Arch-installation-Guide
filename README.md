# Arch-installation-Guide

### Set the console keyboard layout
```
ls /usr/share/kbd/keymaps/**/*.map.gz
```
### Verify the boot mode
```
ls /sys/firmware/efi/efivars
```
### Connect to the internet
```
ip link
```
### Update the system clock
```
timedatectl set-ntp true
```
# Creating necessary partitions
```
Mount point     Partition 	                   Partition type 	         Suggested size
/mnt/boot       /dev/efi_system_partition   	 EFI system partition 	   At least 300 MiB
[SWAP] 	        /dev/swap_partition           Linux swap 	             More than 512 MiB
/mnt 	          /dev/root_partition         	 Linux x86-64 root (/)    
/mnt/home       /dev/home_partition                                    Remainder of the device
```
### Format the partitions

```
mkfs.ext4 /dev/root_partition
```
```
mkfs.ext4 /dev/home_partition
```
If you created a partition for swap, initialize it with mkswap.
```
mkswap /dev/swap_partition
```

```
mkfs.fat -F 32 /dev/efi_system_partition
```
### Mount the file systems
```
mount /dev/root_partition /mnt
```
The directory /boot does not exist yet, so we have to create one.
```
mkdir /mnt/boot
```
Mount the efi partion onto /mnt/boot.
```
mount /dev/efi_system_partition /mnt/boot
```
The directory /home does not exist yet, so we have to create one.
```
mkdir /mnt/home
```
Mount the home partion onto /mnt/home .
```
mount /dev/home_partition /mnt/home
```
If you created a swap volume, enable it with swapon.
```
swapon /dev/swap_partition
```
### Install essential packages
Use the pacstrap script to install the base package, Linux kernel and firmware for common hardware.
```
pacstrap /mnt base linux linux-firmware
```
### Configure the system
# FSTAB
```
genfstab -U /mnt >> /mnt/etc/fstab
```
# Chroot
```
arch-chroot /mnt
```
```
ln -sf /usr/share/zoneinfo/Region/City /etc/localtime
```
hwclock --systohc
# Localization
Edit /etc/locale.gen and uncomment en_US.UTF-8 UTF-8 and other needed locales. Generate the locales by running: 
```
locale-gen
```
Create the locale.conf(5) file, and set the LANG variable accordingly: 
```
/etc/locale.conf
LANG=en_US.UTF-8
```
# Network configuration

Create the hostname file: 

```
/etc/hostname
myhostname
```
#Root password
```
passwd
```



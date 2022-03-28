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
 ```
Mount point 	Partition 	                 Partition type 	       Suggested size
/mnt/boot 	 /dev/efi_system_partition   	EFI system partition 	   At least 300 MiB
[SWAP] 	     /dev/swap_partition          	Linux swap 	          More than 512 MiB
/mnt 	       /dev/root_partition         	Linux x86-64 root (/) 	
/mnt/home    /dev/home_partition                                  Remainder of the device
```

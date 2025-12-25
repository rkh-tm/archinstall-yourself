# Archinstall (Yourself)

I'm writing this to document my arch journey and serve as a back-up in case that I need to reinstall Arch

This will include all my personal settings (I won't be using custom made dotfiles)

## Installing Arch

> The main guide I followed is from the official wiki
> 
> https://wiki.archlinux.org/title/Installation_guide

### 1. Installing ISO
Download ISO from the **torrent** provided in https://arcraiders.wiki

### 2. Load ISO into USB
Use **rufus** to create a live USB

### 3. Boot into the USB
Spam *esc* to open boot menu and press *F9* to pick the USB option

### 4. Connect to Wi-Fi
Package managers require internet to install packages
```bash
iwctl # opens wi-fi menu

device list # list wi-fi [name = wlan0]
station name scan # initiate scanning
station name get-networks # list all available networks [SSID = gtpc5no10]
station name connect SSID

ping ping.archlinux.org # test connection 
```

### 5. Disk Partition
#### Creating Partitions
|Partition|Type|Size|
|-|-|-|
|Partition1|EFI system partition|2 GiB|
|Partition2|Linux x86-64 root (/)|The Rest|

```bash
fdisk -l # shows storage devices

fdisk # opens disk partition menu
G # create new GPT partition
n # spam enter but set size to +2G to create P1
n # spam enter to create P2
t # set the proper Type to each partition
t
w # save
```

#### Formatting Partitions
```bash
mkfs.ext4 /dev/root_partition
mkfs.fat -F 32 /dev/efi_system_partition
```

#### Mounting Partitions
```bash
mount /dev/root_partition /mnt
mount --mkdir /dev/efi_system_partition /mnt/boot
```

### 6. Installing Packages
```bash
timedatectl # update system clock

pacstrap -K /mnt base linux linux-firmware \ # base linux software
base-devel \ # base development kit
amd-ucode \ # CPU microcode
networkmanager \
man-db man-pages \ # manuals
efibootmgr \ # configuring bootloader
nvim
```

### 7. Configuring System
```bash
genfstab -U /mnt >> /mnt/etc/fstab # generate file systems

arch-chroot /mnt

# Timesync
ln -sf /usr/share/zoneinfo/Area/Location /etc/localtime # Asia/Jakarta
hwclock --systohc

# Localization
sudo nano /etc/locale.gen # uncomment preferred locale
sudo locale-gen

# Hostname
nvim /etc/hostname # tamarch

# User
passwd # root
```

### 8. Installing Bootloader
I used systemd-boot, which is suitable for UEFI
> bootctl install doesn't work in live USB so efibootmgr is used

```bash
# Installing systemd-boot
efibootmgr --create --disk /dev/sdX --part Y --loader '\EFI\systemd\systemd-bootx64.efi' --label "Linux Boot Manager" --unicode # X=nvme0n1 Y=1 for nvme0n1p1

# Creating arch.conf file
nvim /boot/loader/entries/arch.conf
title   Arch Linux
linux   /vmlinuz-linux
initrd  /amd-ucode.img
initrd  /initramfs-linux.img
options root=UUID rw # blkid -s UUID -o value /dev/sdXn (find UUID of root)
```

### 9. REBOOT

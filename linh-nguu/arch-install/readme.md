## Arch Linux Install

## 1: Pre-installation

### - Synchronize the system clock

- ```
  "timedatectl set-ntp true"
  ```

### - Internet connection

- First, use this command to check your internet connection.
  ```
  "ping google.com"
  ```
- If there is no internet connection, use this command to connect to the wifi.
  ```
  "iwctl"
  "device scan"
  "device list"
  "station wlan0 scan"
  "station wlan0 get-networks"
  "station wlan0 connect "wifi_name"
  ```

### - Partition disk

- Verify the disk's partitions.
  ```
  "lsblk"
  ```
- Let's set up your disk with gui using the "cfdisk" command.
  - EFI partition
  - SWAP partition
  - Root partition (/)
  - Home partition
- Format partitions
  ```
  "mkfs.fat -F32 /dev/sda1"
  "mkswap /dev/sda2"
  "mkfs.ext4 /dev/sda3"
  "mkfs.ext4 /dev/sda4"
  ```
- Mount partitions
  ```
  "swapon /dev/sda2"
  "mount /dev/sda3 /mnt"
  "mkdir /mnt/{boot,home}"
  "mount /dev/sda1 /mnt/boot"
  "mount /dev/sda4 /mnt/home"
  ```

## 2: Installation

- (Fix keyring error)
  ```
  sudo pacman -Sy archlinux-keyring
  ```

### - Install the required operating system packages and generate the fstab file

- ```
  "pacstrap /mnt linux linux-firmware base base-devel neovim"
  "genfstab -U /mnt >> /mnt/etc/fstab"
  ```

### - Add base configuration

- Enter new system
  ```
  "arch-chroot /mnt"
  ```
- Configure the language of your operating system.
  - Now you have to uncomment the language of your choice
  ```
  "nvim /etc/locale.gen"
  "locale-gen"
  ```
  - Using nvim, edit this file.
  ```
  "nvim /etc/locale.conf"
    LANG=en_US.UTF-8
    LANGUAGE=en_US
  ```
- Set the timezone
  ```
  "ln -sf /usr/share/zoneinfo/Asia/Ho_Chi_Minh /etc/localtime"
  "hwclock —-systohc"
  ```

### - Personalize your computer

- Setup hosts file in your PC
  ```
  "echo linh_ngu > /etc/hostname"
  "nvim /etc/hosts"
    127.0.0.1    localhost.localdomain   localhost
    ::1          localhost.localdomain   localhost
    127.0.0.1    linh_ngu.localdomain    linh_ngu
  ```
- Create new users for linh_ngu and set up the root user.
  ```
  "useradd - m linh"
  "usermod -aG wheel,audio,video,storage,optical,power linh"
    "passwd"(enter your password)
    "passwd linh"(enter your password)
  "EDITOR=nvim visudo"
    (remove "%" before  %wheel ALL=(ALL) NOPASSWD: ALL)
  ```
- Install some Arch-specific packages and configure as needed.
  ```
  "pacman -S git xorg-xinit xorg-server networkmanager grub"
  "systemctl enable NetworkManager"
  ```
- Install bootloader
  ```
  "grub-install --efi-directory=/boot --bootloader-id=arch"
  "grub-mkconfig -o /boot/grub/grub.cfg"
  ```

## 3: Final steps

- ```
  "exit"
  "umount -R /mnt"
  "reboot"
  ```
  ###### yeu Linh Do nhat the gioi

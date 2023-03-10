Before you start, make sure you have a USB drive an Arch Linux ISO image. It is also important that you have a stable and fast internet connection, as you will need to download packages during the installation. This guide uses kernel: 6.2.1.

##  0-Set up your keyboard the way you want (Optional)
```
loadkeys YOURDISTRIBUTION (en=english, es=spanish, etc.)
```

##  1-Wifi (Optional)
```
iwctl
|_  device list
    |_  station YOURNETWORK connect "NAME OF YOUR NETWORK"
```

##  2-Create and resize partitions (part 1)
```
archinstall
|_  language: English
    keyboard layout: es
    mirror region: spain
    locale lang: en_US
    locale encoding: utf-8
    drive: "select desired one with TAB" + ENTER
    disk layout: wipe all - ext4 - "separate partition for /home" - yes
    bootloader: grub-install
    hostname: desired one
    root password: desired one
    user account: desired one (give super-user)
    profile: minimal
    audio: none
    kernels: linux
    aditional packages: git
    network configuration: copy
    tinmezone: desired one
    ntp: true
    optional repositories: multilib
    |_  install
```

##  3-Surface packages & kernel
First you need to import the keys we use to sign packages.
```
curl -s https://raw.githubusercontent.com/linux-surface/linux-surface/master/pkg/keys/surface.asc \
    | sudo pacman-key --add -
```
```
sudo pacman-key --finger 56C464BAAC421453
sudo pacman-key --lsign-key 56C464BAAC421453
```
You can now add the repository by adding the following to the end of /etc/pacman.conf
```
[linux-surface]
Server = https://pkg.surfacelinux.com/arch/
```
After doing that you need to refresh the repository metadata, then you can install the linux-surface kernel and its dependencies.
NOTE: libwacom-surface is packaged through the AUR, so you need to install it from there.

https://aur.archlinux.org/packages/libwacom-surface
```
sudo pacman -Syu
```
```
sudo pacman -S linux-surface linux-surface-headers iptsd
```
```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

##  4-Utilities
The following repositories aim to help you keep your kernel and accompanying software up-to-date. To this end, the Debian, Arch Linux, and Fedora repositories provide the latest kernels pre-compiled as binary packages and pre-signed for secure boot (see the secure boot page).

https://aur.archlinux.org/packages/surface-control
https://aur.archlinux.org/packages/surface-dtx-daemon
```
sudo pacman -Syu
```

##  5-Desktop environment
Using install script (Clone the repository).
```
git clone -b v3 --depth 1 https://www.github.com/Othrondir/dotfiles-2.git
cd dotfiles
chmod +x install-on-arch.sh
./install-on-arch.sh
```

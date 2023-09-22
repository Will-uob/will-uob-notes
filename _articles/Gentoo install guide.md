---
published: true
topic: Installing Gentoo
date: 2022-10-25
tags: linux gentoo filesystems
---

<br>

# Gentoo Install

Hello, and welcome to my Gentoo Installation Guide!
This will be a UEFI install on a Lenovo X230, and we will skip customizing our kernel for now.

### Prerequisites
- A laptop which has hardware support for gentoo linux
- A livecd which you can boot (doesn't have to be the official gentoo livecd)
- Access to the [handbook](https://wiki.gentoo.org/wiki/Handbook:AMD64).

### Partitions
I used f-disk to partition my disk, and created the following GPT table:

| Size          | Partition | Ext   | Purpose       | Command                        |
| ------------- | --------- | ----- | ------------- | ------------------------------ |
| 1G            | /dev/sda1 | FAT32 | used for boot | ```mkfs.fast -F32 /dev/sda1``` |
| 8G            | /dev/sda2 | SWAP  | used for swap | ```mkswap /dev/sda2```         |
| Rest of drive | /dev/sda3 | EXT4  | used for `/`  | ```mkfs.ext4 /dev/sda3```      |

Be sure to use the ```swapon /dev/sda2``` command to activate the swap partition.

### Getting gentoo and setup before chrooting
**Follow the handbook instructions**. I used the openrc-desktop tarball, but you may have different needs, so make sure you choose the right one. Choosing a good match for your needs makes
the process of updating the world set a lot faster, since a lot of packages will already be included. Make sure you install the system on the same day you got the tarball! Apart from that, you'll need to
- Prepare the gentoo ebuild repository
- Copy the DNS info
- Mount the file systems (please copy and paste these, this is one of the reasons having a livecd is so useful)[^1]
  Also, if you see the ```/dev/shm** symbolic link warning, don't worry. It didn't seem to effect my install

### Chrooting and configuring portage
**Follow the handbook instructions**. I chose the desktop profile [5], but this might have changed now, so look at the profile list using ```eselect profile list** before selecting. Once you're happy,
update the world set.

### Configuring use flags
**Follow the handbook instructions**. Especially if you have a non-intel graphics card. But, this was mostly copy and paste.

### Setting up the system
**Follow the handbook instructions**. The following are tasks which I decided to complete, again, according to the handbook:
- Accept license
- Configure timezone
- Configure locale
- Install firmware and kernel distribution[^2]
- Setup fstab[^3]

### Setting up networking
**Follow the handbook instructions** The order I did this is as follows:
- Setup hostname
- Install ```net-misc/dhcpcd```
- Add the above to runtime, and start it using openrc
- Edit ```/etc/hosts**

While technically not part of the networking process, I'd recommend you to use the ```passwd``` command now, to setup your root user.

### System tools
**Read the handbook**. Before starting, setup your ```/etc/rc.conf``` and ```/etc/conf.d/keymaps```, to make the process smoother. The following is a table of categories and packages I installed for them.

| Processes     | Package  |
| ------------- | -------- |
| System logger | sysklogd |
| Cron Daemon   | cronie   |
| File indexing | mlocate  |
| Remote shell access | sshd[^4] |
| Time sync | chrony |
| Filesys tools | io-scheduler-udev-rules, e2fsprogs, dosfstools |
| Network tools | net-wireless/iw, net-wireless/wpa_supplicant |

### Configure the bootloader
**Read the handbook**. We will be using Grub2, and installing on our /boot directory. I used the following commands:
- ```echo 'GRUB_PLATFORMS="efi-64"' >> /etc/portage/make.conf```
- ```emerge --ask --verbose sys-boot/grub```
- ```grub-install --target=x86_64-efi --efi-directory=/boot --removable```
- ```grub-mkconfig -o /boot/grub/grub.cfg```

### Reboot
Alright, you should now have a fully functioning Gentoo system. Please reboot, according to the **handbook**, and then access you new system. But, I would recommend you do two things now, before this, to
avoid a massive headache.

#### Setup your user
I would recommend setting up your user with the following command: ```useradd -m -G wheel, users, audio, video -S /bin/bash username```. Then setup the password using ```passwd username```. Also, depending on
the profile you chose, ```sudo``` may not yet be installed. Install it, and then add your user to the sudoers file using ```EDITOR=nano visudo```, either now or after the reboot.

### Setting up xorg
Now that you have a fully working gentoo install, I'd recommend installing xorg, according to the handbook, gentoo and arch wikis. Some quick tips:
- Install xorg-server
- Install elogind network-manager and dbus
- Add display-manager (or any display manager you prefer) to default runtime
- Install alsa-utils for audio

[^1] Make sure that your ```/boot``` is where ```/dev/sda1``` is mounted, since this is very important when installing grub!

[^2] I installed packages ```sys-kernel/linux-firmware```, ```sys-kernel/installkernel-gentoo``` and ```sys-kernel/gentoo-kernel-bin```.

[^3] You can setup fstab automatically by using [this](https://github.com/glacion/genfstab) install script. Just use wget to download it.

[^4] It was already installed, so you can just add it to the runtime by doing ```rc-update add sshd default```.

# How to Install Arch Linux with Encryption and Hibernation on Btrfs

**Author:** David Boyd<br>
**Date:** 2024-04-21

## Table of Contents

<!-- vim-markdown-toc GFM -->

* [Overview](#overview)
* [Setup the Installation Environment](#setup-the-installation-environment)
  * [1. Connect To Network](#1-connect-to-network)
  * [2. Test Connection](#2-test-connection)
  * [3. Setup System Time](#3-setup-system-time)
  * [4. Setup mirror list](#4-setup-mirror-list)
  * [5. Sync package database](#5-sync-package-database)
* [SSD Setup](#ssd-setup)
  * [Disk Partitioning](#disk-partitioning)
    * [1. List disks](#1-list-disks)
    * [2. Manipulate partition table using either `fdisk`, `gdisk` (gptfdisk), etc](#2-manipulate-partition-table-using-either-fdisk-gdisk-gptfdisk-etc)
  * [Filesystem Formatting](#filesystem-formatting)
    * [1. Format the Boot Partition](#1-format-the-boot-partition)
    * [2. Setup Btrfs and encrypt via main Linux partition via LUKS](#2-setup-btrfs-and-encrypt-via-main-linux-partition-via-luks)
    * [3. Create Btrfs Sub-Volumes](#3-create-btrfs-sub-volumes)
    * [4. Mount The Filesystems](#4-mount-the-filesystems)
* [Installing Arch on Disk](#installing-arch-on-disk)
  * [Bootstrapping the Base System](#bootstrapping-the-base-system)
  * [Configure the System](#configure-the-system)
  * [Chroot](#chroot)
  * [Time](#time)
  * [Localization](#localization)
  * [Network Configuration](#network-configuration)
    * [Hostname](#hostname)
    * [Hosts](#hosts)
  * [Root Password](#root-password)
  * [Bootloader](#bootloader)
    * [1. Install the Booty Utilities](#1-install-the-booty-utilities)
    * [2. Install the GRUB Bootload on a UEFI Supported System](#2-install-the-grub-bootload-on-a-uefi-supported-system)
    * [3. Configure GRUB](#3-configure-grub)
      * [3.1 Choose your ACPI value.](#31-choose-your-acpi-value)
      * [3.2 Configure /etc/default/grub](#32-configure-etcdefaultgrub)
* [Hibernation](#hibernation)
  * [Lid Toggle Hibernation](#lid-toggle-hibernation)
* [Troubleshooting](#troubleshooting)
  * [apropos / whatis Returns "Nothing Appropriate"](#apropos--whatis-returns-nothing-appropriate)
    * [Solution](#solution)
    * [Error Summary](#error-summary)

<!-- vim-markdown-toc -->

## Overview

| Assumptions    |               |
|----------------|---------------|
| Secure Boot    | Disabled      |
| Bootable drive | Already setup |

## Setup the Installation Environment

### 1. Connect To Network

``` bash
iwctl station wlan0 connect <SSID>
```

### 2. Test Connection

``` bash
ping -c2 archlinux.org
```

### 3. Setup System Time

``` bash
# 1. Find your region and city
timedatectl list-timezones | grep -i <city>

# 2. Link localtime
`ln -sf /usr/share/zoneinfo/<Region>/<City> /etc/localtime`

# 3. Prevent clock drift
timedatectl set-ntp true

# 4. Confirm local and UTC times
timedatectl

# 5. Set hardware clock from UTC to local
hwclock --systohc
```

### 4. Setup mirror list

``` bash
reflector --latest 10 --sort rate --country US --save /etc/pacmand.d/mirrolist
```

### 5. Sync package database

``` bash
pacman -Syu
```

## SSD Setup

### Disk Partitioning

#### 1. List disks

``` bash
lsblk
```

#### 2. Manipulate partition table using either `fdisk`, `gdisk` (gptfdisk), etc

``` bash
# 1. Make book EFI partition
n
1
<CR>  # ENTER for default first sector
+550M
ef00

# 2. Make main Linux parition
n
2
<CR>  # ENTER for default first sector
-50G  # Leaving 50G at the end for the SSD to work with
<CR>  # ENTER for default type Linux

# 3. Print partition table
p

# 4. Write partition table to disk and exit
w
Y
```

### Filesystem Formatting

> This install uses BTRFS. More guides will be created later for other
> filesystem types, e.g. ZFS.

#### 1. Format the Boot Partition

``` bash
mkfs.vfat /dev/nvme0n1p1
```

#### 2. Setup Btrfs and encrypt via main Linux partition via LUKS

``` bash
# 1. Encrypt the Root/Main partition
cryptsetup luksFormat /dev/nvme0n1p2
YES
<passphrase>

# 2. Decrypt the partition and map it to 'cryptroot'
cryptsetup luksOpen /dev/nvme0n1p2 cryptroot
<passphrase>


# (Optional): Ensure your partition is opened & decrypted
lsblk
# (Optional): Ensure your device mapper is present
ls /dev/mapper
```

* If using BTRFS:

    ``` bash
    # 3. Format the virtual block device with Btrfs
    mkfs.btrfs /dev/mapper/cryptroot
    ```

* Else if using Ext4:

    ``` bash
    # 3. Format the virtual block device with Ext4
    mkfs.ext4 /dev/mapper/cryptroot
    ```

``` bash
# 4. Mount the encrypted filesystem in 'cryptroot' to /mnt
mount /dev/mapper/cryptroot /mnt

# (Optional): Ensure the mounted 'cryptroot' is accessible
ls /mnt
```

> **`/dev/mapper/`</br>**
> - Files in /dev/mapper/ are block devices managed by the linux device mapper
> framework or more specifically for your case, the dm-crypt kernel subsystem.

#### 3. Create Btrfs Sub-Volumes

``` bash
btrfs subvolume create /mnt/@
btrfs subvolume create /mnt/@home
btrfs subvolume create /mnt/@var
btrfs subvolume create /mnt/@swap
umount /mnt
```

> "**`@`**" symbol</br>
> - The **`@`** symbol is used to denote subvolumes specific to the `btrfs`
> command.

#### 4. Mount The Filesystems

``` bash
# Mount the Root/main filesystem with the specified options
mount -o noatime,compress=zstd,ssd,discard=async,space_cache=v2,subvol=@ /dev/mapper/cryptroot /mnt

# Create the necessary directories within the root filesystem
mkdir -p /mnt/{boot,home,var,swap}

# Mount the home subvolume
mount -o noatime,compress=zstd,ssd,discard=async,space_cache=v2,subvol=@home /dev/mapper/cryptroot /mnt/home

# Mount the var subvolume
mount -o noatime,compress=zstd,ssd,discard=async,space_cache=v2,subvol=@var /dev/mapper/cryptroot /mnt/var

# Mount the swap subvolume
mount -o noatime,ssd,space_cache=v2,subvol=@swap /dev/mapper/cryptroot /mnt/swap

# Mount the boot partition to /mnt/boot
mount /dev/nvme0n1p1 /mnt/boot

# (Optional): List block devices and their mount points
lsblk
```

> **<u>Explanation of mount options:</u>**</br>
>
> **`-o noatime`**</br>
> Tells the filesystem not to update the last access time for files. :bulb: It
> can improve performance by reducing disk writes.
>
> **``-s compress=zstd``**</br>
> Specifies that the filesystem should use the Zstandard compression algorithm
> to compress data. :bulb: Zstd is known for its high compression ratios and fast
> compression/decompression speeds.
>
> **`-o ssd`**</br>
> This option optimizes the filesystem for SSD (Solid State Drive) storage devices. It adjusts certain parameters to improve performance and reduce unnecessary wear on SSDs.
>
> **`-o discard=async`**</br>
> Enable asynchronous TRIM/discard operations. :bulb: <u>**`trim`**</u> is a
> command that informs the SSD which blocks of data are no longer considered in
> use and can be erased internally. :bulb: <u>**Asynchronous discard**</u>
> means that the **TRIM** commands are issued in the background, improving
> performance.
>
> **`-o space_cache=v2`**</br>
> Enable use of the space cache feature in Btrfs version 2. The <u>**space
> cache**</u> improves the performance of filesystem operations by caching
> information about free space on the disk.</br>
> :warning: Errors have been reported when using **`v1`**.

## Installing Arch on Disk

### Bootstrapping the Base System

1. Install Essential Packages (and then some)

:warning: The `grep` command is <u>**untested**</u>:exclamation:</br>
*It's supposed to install either `intel-ucode` or `amd-ucode` based on your
machine's CPU!*

``` bash
pacstrap -K /mnt base linux linux-firmware base-devel linux-headers \
$(grep -m1 'vendor_id' /proc/cpuinfo | awk '{print tolower($3)}' | sed 's/genuine//;s/authentic//')-ucode
btrfs-progs \
sof-firmware pipewire \
networkmanager \
bat git vim tmux \
man-db man-pages texinfo \
reflector \
sudo
```

> **`-K`**</br>
> An option that instructs `pacstrap` to skip copying the host's keys to
> the new system where the hots's keys are already (or ought to be) available
> and trusted. This prevents copying the keys *again* to the new system.

### Configure the System

1. Generate the filesystem table

``` bash
genfstab -U /mnt >> /mnt/etc/fstab
```

> :books: A **filesystem table `(fstab)`** is a configuration file used to
> define how filesystems should be mounted and managed during the system's boot
> process. The **fstab** contains the following fields:
>> | fstab Field     | Definition                             | Examples                                      |
>> |-----------------|----------------------------------------|-----------------------------------------------|
>> | Device          | Specifies which device/partition       | `UUID=<UUID>`, `/dev/sda1`,  `/dev/nvme0n1p1` |
>> | Mount Point     | Dst in system's directory tree         | `/` (root), `/home`, `/boot`, `/var`          |
>> | Filesystem Type | Specifies FS type                      | `ext4`, `efs`, `btrfs`, `ntfs`, `zfs`         |
>> | Mount Options   | Controls how FS is mounted             | `defaults`                                    |
>> | Dump            | Perform FS backup?                     | `0` (no), `1` (yes)                           |
>> | Pass            | FS Consistency Check (`fsck`) on boot? | `0` (no), `1` (yes), `2` (yes, in asc order)  |

### Chroot

``` bash
arch-chroot /mnt
```

> :books: **Change root (`chroot`)** changed the root directory for the current
> process and its children to a new directory. Commonly used for bootstrapping
> a new system, repairing an existing system, running software in a controlled
> environment, or building software in a clean environment.
>> :bulb: **`arch-chroot`** is an Arch specific script that simplifies the
>> process of entering a `chroot` environment on an Arch system--tailored to
>> the installation process.

### Time

:rotating_light: **SUPER IMPORTANT**:exclamation::exclamation::exclamation:<br>
Un/miscofigured localization is a common source of signing keys' issues that
occur when attempting to install programs from the AUR via `pacman`, `yay`, and
`paru`.

1. Set the time zone:

``` bash
# 1. Find your region and city
timedatectl list-timezones | grep -i <city>

# 2. Link localtime
`ln -sf /usr/share/zoneinfo/<Region>/<City> /etc/localtime`

# 3. Prevent clock drift
timedatectl set-ntp true

# 4. Confirm local and UTC times
timedatectl

# 5. Set hardware clock from UTC to local
hwclock --systohc
```

### Localization

1. Generate the locales

``` bash
locale-gen
```

2. Edit the `/etc/locale.gen`

``` bash
# Uncomment YOUR locale language
en_US.UTF-8
```

3. Create/edit the `/etc/locale.conf`

``` bash
# Input YOUR locale language
echo "LANG=en_US.UTF-8" > `/etc/locale.conf`
```

4. Set the console keyboard layout to persistent configuration

> :pencil: The following steps will auto-fill the `/etc/vconsole.conf` file.

``` bash
# 0. Find your country code
localectl list-keymaps

# 1. Load keys for the current session
loadkeys us

# 2. Set keymap persistence and auto-change the Xorg keymap to the nearest match
localectl set-keymap us
```

* Resulting `/etc/vconsole.conf` file should look similar to this:

  ``` bash
  # Written by systemd-localed(8) or systemd-firstboot(1), read by systemd-localed
  # and systemd-vconsole-setup(8). Use localectl(1) to update this file.
  KEYMAP=us
  XKBLAYOUT=us
  XKBMODEL=pc015+inet
  XKBOPTIONS=terminate:ctrl_alt_bksp
  ```

### Network Configuration

#### Hostname

``` bash
export HOST=<myComputerName>
echo $HOST > /etc/hostname
```

#### Hosts

> :warning: Assuming `export HOST=<myComputerName>` is set!

Configure hosts file:

``` bash
echo -e "127.0.0.1\tlocalhost\n::1\tlocalhost\n127.0.1.1\t$HOST.localdomain\t$HOST" > /etc/hosts
```

### Root Password

``` bash
passwd
```

### Bootloader

#### 1. Install the Booty Utilities

``` bash
# Choose the default prompts when installing
pacman -Syu efibootmgr grub
```

#### 2. Install the GRUB Bootload on a UEFI Supported System

``` bash
grub-install --target=x86_64-efi --efidirectory=/boot --bootloader-id=GRUB
```

> **`grub-install`**<br>
> A command used to install the GRUB bootloader.
>
> **`--target=x86_64-efi`**<br>
> An option to specify the target platform for GRUB installation for 64-bit
> UEFI system.
>
> **`--efi-directory=/boot`**<br>
> An option that specifies the directory where the <u>**EFI system
> partition**</u> ***(ESP)*** is to be mounted. :bulb: The <u>**ESP**</u> is a=
> partition on the disk that holds boot loaders and other files used by the
> UEFI firmware.
>
> **`--bootloader-id=GRUB`**<br>
> An option that sets the <u>*identifier*</u> for the GRUB bootloader in the UEFI 
> firmware's boot manager. It typically appears as an entry in the <u>*UEFI
> boot menu*</u>, allowing the user to select "**GRUB**" as the boot loader.

#### 3. Configure GRUB

##### 3.1 Choose your ACPI value.

The **<u>Advanced Configuration and Power Interface</u> (ACPI)**
`acip_osi=""` option in GRUB is often used to address compatibility issues
with certain hardware components, particularly in laptops and other devices
that rely heavily on the **ACPI** for pwr mgmt and hw ctrl. This options can
help ensure that the Linux kernel behaves in a manner similar to how it would
on hardware ***designed to run*** the out-of-box (OOB) OS system, potentially
improving compatibility and stability. Meaning, most laptop brands would be
designed to run `\"Windows 2020\"` whereas Linux-specific brands (TUX,
System76, etc) would be designed to run the `\"Linux"\` ACPI.

| `ascpi_osi=`       | Emulates ACPI behavior compatible with {}             |
|--------------------|-------------------------------------------------------|
| `\"Android\"`      | Android-based hardware                                |
| `\"Linux\"`        | Linux-based hardware                                  |
| `\"Linux\"`        | :question: M Series-based MacBooks hardware:question: |
| `\"Windows 2020\"` | generic modern Windows-based hardware                 |
| `\"Windows 2015\"` | :question: Intel-based MacBooks hardware:question:    |
| `\"Windows 10\"`   | Windows 10-based hardware                             |
| `\"Windows 11\"`   | Windows 11-based hardware                             |
| `\"Virtual\"`      | generic virtualization-based platforms                |
| `\"Hyper-V\"`      | Hyper-V-based virtualization platforms                |
| `\"QEMU\"`         | QEMU-based virtualization platforms                   |
| `\"VMWare\"`       | VMWare-based virtualization platforms                 |
| `\"VirtualBox\"`   | VirtualBox-based virtualization platforms             |
| `\"Xen\"`          | Xen-based virtualization platforms                    |

##### 3.2 Configure /etc/default/grub

``` bash
# 1. Get Root/Main Partition's UUID
blkid -s UUID -o value /dev/nvme0n1p2 >> /etc/default/grub


# 2. Edit /etc/default/grub
GRUB_CMDLINE_LINUX_DEFAULT = "loglevel=3 quiet acpi_osi=\"<CHANGE_ABOVE>\" mem_sleep_default=deep cryptdevice=UUID=PASTED-UUID:cryptroot:allow-discards root=/dev/mapper/cryptroot"

```

## Hibernation

### Lid Toggle Hibernation

1. Install ACPI utilities

``` bash
sudo pacman -S acpid
```

2. Edit the ACPI Configuration

Open the `/etc/systemd/logind.conf` file.

``` bash
# Uncomment the following line
HandleLidSwitch=suspend

# Change value
HandleLidSwitch=hibernate
```

3. Restart systemd-logind Service

:warning: If your login manager is not set up, you will be forced out of your
desktop environment!

``` bash
sudo systemctl restart systemd-logind.service
```

4. Test hibernation on lid close.

## Troubleshooting

### apropos / whatis Returns "Nothing Appropriate"

| Resolved | :heavy_check_mark: |
|---------:|--------------------|

#### Solution

Each time you install new manpages, run `mandb` as root:

``` bash
sudo mandb
```

#### Error Summary

| Command         | Return Error            |
|-----------------|-------------------------|
| `apropos <arg>` | `"Nothing Appropriate"` |
| `whatis <arg>`   | `"Nothing Appropriate"` |


<!-- References -->
[RobFisherMd]: https://gist.github.com/RobFisher/abd9b2b9fca4194ac8df112715045b61
[RobFisherYT]: https://something.com



opensssh \
plocate \
posix-c-development \
posix-software-development \
posix-user-portability \
posix-xsi
unzip \
wev \



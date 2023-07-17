# How to Boot Proxmox VE from an SSD on a Dell PowerEdge R620 Server

**Author:** David Boyd<br>
**Date:** 2023-07-16

## Table of Contents

- [Introduction](#introduction)
- [Steps](#steps)
  - [1. Install the Hardware](#1.-install-the-hardware)
  - [2. Install the OS](#2.-install-the-os)
  - [3. Install the Clover Bootloader](#3.-install-the-clover-bootloader)
  - [4. Autoboot into OS from Clover](#4.-autoboot-into-os-from-clover)

## Introduction

The Dell PowerEdge R620 cannot boot an OS directly from an SSD via a PCIe slot,
but rather is purposed as a storage unit. Nevertheless, this can be
worked around by installing a bootloader in one of the bootable drives that, in
turn, points to the bootloader installed on the SSD.

### Limitations

- :x: ***No bifurcation*** means that only ***one SSD*** slot per PCIe card can 
  be used. I have *not* tested this with multiple risers and PCIe cards.

### Required Hardware

1. Riser Card
    - *I didn't purchase a riser card as my R620 came with two pre-installed.*
2. PCIe Add-on Card
    - :warning: I purchased the
    [Supermicro AOC-SLG3-2M2 PCIe Add-On Card for up to Two NVMe SSDs][card-2]
    as I mistakenly thought I had an R630 (which supports bifurcation). The 
    one slot still works, but there are plenty of cheaper [$10 options][card-1]
    allocating only one M.2 slot.
3. Two USBs:
    - 1 temporary USB to remain in the server to be used as our 
      [Clover][C-official] bootloader
    - 1 USB to boot the [Proxmox installer][pve-dl]
    - :bulb: You can use one USB to install the OS and then re-flash to install
      Clover.
    - :warning: Keep in mind that the Clover USB will need to be permanently 
      inserted on the R620 as this will be the primary bootloader for our
      server!

## Steps

### 1. Install the Hardware

0. Open the R620 chasis
1. Insert the M.2 SSD into the PCIe x4 adapter
2. Insert the PCIe adapter into the riser card slot #1
3. Insert the riser card into the R620's PCIe slot #1
    - :thinking: I haven't tested this on other slot numbers
4. Close the R620 chasis

### 2. Install the OS

#### Flash a Bootable USB

If you've made it this far, I'll assume that you know how to install Proxmox
(or any other OS) by creating a bootable USB image so I won't go through those
steps. But I will say that I've been using [Ventoy][vtoy] on a 64GB USB stick
for awhile now and the ease of use makes it worth mentioning. I've been
successful in booting Linux distros, Windows, and macOS.

1. Boot from USB: `F12` > Select the USB with the bootable image
2. Install the OS as you normally would --just select the SSD as the drive.

:bulb: You will ***NOT*** be able to boot into the SSD!

#####  :x: **Proxmox ERROR** :x: : `Failed to prepare EFI boot using Grub`

This [post][pve-efi-err] addresses the issue clearly. Ultimately, its because
Proxmox wants the servers BIOS to point to its bootloader and *only* its
bootloader. With more than one bootloader option, Proxmox sees this as issue
and you'll have to re-run the installation steps again... ugh

1. Reboot the server and press `F2` to enter the **System Settings**
2. Go to `BIOS Settings` and ***uncheck*** (disable) EVERYTHING
   but the USB Proxmox installer... really, you only need to uncheck anything 
   with a bootable UEFI, but why risk it?
3. Save and exit.
4. Repeat the OS install

### 3. Install the Clover Bootloader

I'm unsure why I've had such difficulty with this, but the following method
worked for me. This combines [Booting from an NVME SSD on an older PC using
Clover][blog-main] by Hamish McIntyre-Bhatty and [bootable NVME install on
old hardware made easy with pcie adapter and clover][blog-pve] by jieku.

1. Download the ***custom Clover image*** ([here][clover-custom1] or 
   [here][clover-custom2]) with NvmExpressDxe preconfigured.
2. Decompress the `7z` image file
3. Flash a USB drive with that image
    - :bulb: I used [Etcher Balena][etcher] to flash the drive
    - :warning: This USB will be permanently staying inside your server.
4. Once completed, insert the Custom Clover USB in either your internal USB
   drive (if available) or into one of the external slots.
5. Boot the R620 and press `F12` to select the Clover USB.
6. Once in Clover:
    1. Press `F3` to bring up the hidden EFIs
    2. Select the last icon (farthest right) to boot into Proxmox.

### 4. Autoboot into OS from Clover

0. Login into Proxmox
1. Get EFI partition drive: `fdisk -l | grep -i nvme`
    - :eyes: Often appears as: `/dev/nvme0n1p2`
    - :warning: If your drive does not appear as an NVMe, then just scan
    through your filesystems: `fdisk -l`
2. Get PARTUUID for that EFI partition: `blkid | grep -i nvme`
3. Shutdown R620
4. Take out the Clover USB and plug it into another computer to edit
    - :thinking: I'm sure there's a faster way to do this, but at this point, I
    just want to get this thing up and running.
5. Backup the current **config.plist** file: `cp EFI/CLOVER/config.plist
   EFI/CLOVER/config.plist.bak`
6. Overwrite the **config.plist** file with:

``` bash
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
  <key>Boot</key>
  <dict>
    <key>Timeout</key>
    <integer>0</integer>
    <key>DefaultVolume</key>
    <string>LastBootedVolume</string>
  </dict>
  <key>GUI</key>
  <dict>
    <key>Custom</key>
    <dict>
      <key>Entries</key>
      <array>
        <dict>
          <key>Path</key>
          <string>\EFI\proxmox\grubx64.efi</string>
          <key>Title</key>
          <string>Proxmox</string>
          <key>Type</key>
          <string>Linux</string>
          <key>Volume</key>
          <string>33BA6C23-4772-294D-9053-72A49FCAEF39</string>
          <key>VolumeType</key>
          <string>Internal</string>
        </dict>
      </array>
    </dict>
  </dict>
</dict>
</plist>
```

7. Replace the Volume's string `33BA6C23-4772-294D-9053-72A49FCAEF39` with your
   EFI's PARTUUID from step #2.
    - :warning: The PARTUUID must be ***CAPITALIZED***:exclamation:
      :exclamation::exclamation:
8. Save, exit, and unmount the drive.
9. Re-insert the Clover USB into the server
10. Boot up the server and press `F2` to enter **System Settings**
11. Select **BIOS Settings** 
    1. Enable the Clover USB
    2. Move the Clover USB to the top of the boot sequence list
    3. Save changes and reboot machine.
12. :tada: ***Done!*** :tada:

<!-- References -->

[card-1]: https://www.amazon.co.uk/gp/product/B07CBJ6RH7/ref=ppx_yo_dt_b_asin_title_o07_s00?ie=UTF8&psc=1
[card-2]: https://www.supermicro.com/en/products/accessories/addon/AOC-SLG3-2M2.php

[pve-dl]: https://proxmox.com/en/downloads
[pve-efi-err]: https://forum.proxmox.com/threads/installation-failing-failed-to-prepare-efi-boot-using-grub.122002/
[vtoy]: https://github.com/ventoy/Ventoy

[blog-pve]: https://forum.proxmox.com/threads/bootable-nvme-install-on-old-hardware-made-easy-with-pcie-adapter-and-clover.78120/
[blog-main]: https://www.hamishmb.com/booting-nvme-older-pc-refind/

[C-official]: https://github.com/CloverHackyColor/CloverBootloader/releases
[etcher]: https://etcher.balena.io/#download-etcher
[clover-custom1]: https://e1.pcloud.link/publink/show?code=XZUdjLZnMTcfJXjWa8Tj8YKtyJM0u2R9faV
[clover-custom2]: https://github.com/dboyd42/it-support/raw/master/Network%20and%20Systems%20Administration/Virtualization/Proxmox/files/Clover.img.7z


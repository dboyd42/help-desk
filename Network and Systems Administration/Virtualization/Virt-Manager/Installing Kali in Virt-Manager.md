# Installing Kali in Virt-Manager

**Author:** David Boyd<br>
**Date:** 2023-09-29

## Table of Contents

## Troubleshooting

### No Display After Kali Install Screen

#### Current Setup:

|      |                                        |
|------|----------------------------------------|
| Date | 2023-09-29                             |
| OS   | Garuda (Arch)                          |
| CPU  | i7-1165G7                              |
| ISO  | kali-2022.4-everything.iso *(renamed)* |

#### The Problem

After the Kali ISO boots up, I select `Install` (tried both the graphical and
non-graphical). Then what appears are three lines at the bottom of the screen
stating that **Kali can't mount /dev/vda** and **media failed** to something
along the lines that it **can't unmount**. The proceeding screen is a loop of
logs that appears similar to the image below:

![Kali No Dispaly Loop](../pics/virt-manager_kali_no_display.png)
*Credit: [StackOverflow][so_display]*

#### Probable Cause

According to [Kraxel's blog about display devices in qemu][k-blog], the VirtIO
(assuming VirtIO VGA) display is *should* be VGA compatable without drivers
already built-in. However, assuming the drivers not installed in the ISO and 
the ISO is not compatable, this would lead to our display issue. Therefore,
changing the display would lead to resolving this issue. *(Also, doesn't this
sound familiar with macOS's UTM and Kali? Having to install via a serial
display rather than the default one?!?!)*

#### The Fix

In the [StackOverflow article][so_display], the fix is to set the display 
from `VirtIO` to `QXL` with the acceleration turned off before switching.

After installation, you should be able to switch back to the VirtIO display
(just as you would remove the Serial dispaly in UTM). However, I went ahead and
logged in via the QXL display to ensure that it was working (it is). Then
updated and upgraded everything.

I will switch back to the VirtIO display once this process has completed.

<!-- References -->

[k-blog]: https://www.kraxel.org/blog/2019/09/display-devices-in-qemu/
[so_display]: https://unix.stackexchange.com/questions/712474/trying-to-install-kali-linux-on-qemu-kvm-using-virt-manager-fails-on-no-displa


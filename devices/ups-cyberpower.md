# CyberPower Instructions

> Author: David Boyd<br>
> Date: 2023-04-10<br>
> Ref: [ArchWiki - CyberPower UPS]

## Install PowerPanel CLI Tool

``` bash
# 1. Install the CyberPower tool
yay -S powerpanel   # AUR Pkg for ArchLinux

# Help menu
prwstat --help
```

## How to Shut the Beep Up

1. Plug in the USB-B on back of UPS to a USB-A on laptop.
2. Initiate Service: `systemctl start pwrstatd.service`
3. Mute: `sudo pwrstat -mute`

*Note: You can check if the computer registered the USP via: `lsusb`*

[ArchWiki - CyberPower UPS]: https://wiki.archlinux.org/title/CyberPower_UPS

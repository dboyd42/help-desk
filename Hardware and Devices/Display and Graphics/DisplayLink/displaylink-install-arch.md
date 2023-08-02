# Installing DisplayLink on Arch Linux

> Author : David Boyd<br>
> Date   : 2023-04-10<br>
>> *Updated*: 2023-06-12

|              |                            |
|:------------:|----------------------------|
|  **STATUS**  | :heavy_check_mark: Working |
| Reference 1: | [ArchWiki]                 |
| Reference 2: | [PageFlip]                 |

## Installation

### 1. Install packages

`sudo yay -S evdi-git displaylink`

### 2. Enable service

`systemctl enable --now displaylink.service`

### 3.1 Link config file

`sudo ln -sf $PWD/20-evdi.conf /etc/X11/xorg.conf.d/20-evdi.conf`

### --OR-- ####

### 3.2 Create file with the following settings

``` bash
echo -E 'Section "OutputClass"
Identifier "DisplayLink"
Driver "modesetting"
Option "PageFlip" "false"
EndSection' >> /etc/X11/xorg.conf.d/20-evdi.conf
```

### 4. Reboot

`sudo reboot 0`

### 5. Update kernel module

:bulb: *This step may no longer be necessary. Testing is required.*

`modprobe udl`

### 6. Apply Settings (KDE Plasma)

  1. Go to: `Settings` > `Display & Monitor`
  2. Configure: `Device: <monitor>`
  3. Enable: `[X] Enabled`
  4. Apply the settings: `Apply`

## ISSUES

- Ghosting: ~5-10 sec delay/lag for cursor
- Redraw / Screen Positioning
  - When configured in portrait mode, half of the monitor is mirrored from
    another monitor.

### Notes

- These issues did not appear when ran with ArcoLinux XL
  - Refer to [dotfiles/etc/X11/xorg.conf.d/20-evdi.conf][evdi-dot] for relative
  instructions.

- There may be an issue with the 11th Gen Intel CPU and DisplayLink/uld.
However, I failed to document the process. --\\\_(\*.\*)_/-- *Oh, Well*

<!-- References -->

[ArchWiki]: https://wiki.archlinux.org/title/DisplayLink
[pageflip]: https://support.displaylink.com/knowledgebase/articles/1181623
[evdi-dot]: https://github.com/dboyd42/dotfiles/blob/master/etc/X11/xorg.conf.d/20-evdi.conf

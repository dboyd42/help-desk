# Installing Display Link on Arch Linux

> Author: David Boyd<br>
> Date: 2023-04-10

|             |            |
|-------------|------------|
| **STATUS:** | *WIP*      |
| Ref:        | [ArchWiki] |

## Installation

``` bash
# 1. Install needed packages
yay -S evdi-compat-git displaylink

# 2. Enable service
systemctl enable --now displaylink.service
```

## ISSUES

- Ghosting: ~5-10 sec delay/lag for cursor
- Redraw / Screen Positioning
  - When configured in portrait mode, half of the monitor is mirrored from
    another monitor.

### Notes

- These issues did not appear when ran with ArcoLinux XL
  - Refer to `dotfiles/etc/X11/xorg.conf.d/20-evdi.conf` for relative
  instructions.

- There may be an issue with the 11th Gen Intel CPU and DisplayLink/uld.
However, I failed to document the process. --\\\_(\*.\*)_/-- *Oh, Well*

[ArchWiki]: https://wiki.archlinux.org/title/DisplayLink

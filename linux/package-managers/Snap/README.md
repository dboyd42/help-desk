# Snap Install on Arch Linux

> Author: David Boyd<br>
> Date: 2023-03-27

## About

**Snap** is a package management system that doesn't suck when it's not forced upon
you like it is on Ubuntu. **snapd** is a REST API daemon for managing snap
packages.  **AppArmor** can be enabled to integrate app isolation/confinement.

|    |            |
|----|------------|
| OS | Arch       |
| DE | KDE Plasma |
| WM | X11        |

## Installation

:warning: Pulling, building, then installing the package was the only method
that successfully made Snap work.  Pacman and yay (AUR) packages were
unsuccessful.

``` bash
# 1. Pull and build the Snap package
git clone https://aur.archlinux.org/snapd.git
cd snapd; makepkg -si
```

**Troubleshooting errors experienced during build:**

:bulb: Always update/upgrade system before attempting other solutions: `pacman
-Syu`

| Displayed Error                                    | Resolution           |
|----------------------------------------------------|----------------------|
| `autoreconf: command not found`                    | `pacman -S autoconf` |
| `failed to run aclocal: No such file or directory` | `pacman -S automake` |

``` bash
# 2. Enable the communication socket
systemctl enable --now snapd.socket

# 3. (Recommended) Enable the AppArmor
systemctl enable --now snapd.apparmor
```

## References

- [Snap - Official](https://snapcraft.io/)
- [Snap - Arch Wiki](https://wiki.archlinux.org/title/Snap)

# IT Support / KBS

**Author:** David Boyd<br>
**Updated:** 2023-06-21

## Table of Contents

- [Introduction](#introduction)
- [Getting Started](#getting-started)
  - [The KBS Structure Explained](#the-kbs-structure-explained)
  - [Command Line Interface](#command-line-interface)
    - [Example 1: Perform a basic operation](#example-1-perform-a-basic-operation)
    - [Example 2: Configure advanced settings](#example-2-configure-advanced-settings)
    - [Example 3: Render MD file](#exmaple-3-render-md-file)
- [Troubleshooting](#troubleshooting)

## Introduction

This repo acts as a knowledge base system (KBS) for various IT issues and their
*hopeful* resolutions that I have worked tirelessly though. The repo has been
updated to fit a more IT KBS structure. Note, there is a current work in
progress to update all RST files to MD.

## Getting Started

The fastest method to search for an issue would be to use `grep -ri` from the
root directory. But to each their own!

### The KBS Structure Explained

- [Cloud Computing][c-cc]
  - Subcategories:
    - [OneDrive][c-cc-onedrive]
  - Tags: `onedrive`

- [Cybersecurity][c-cs]
  - Deals with protecting computer systems, networks, and data from
  unauthorized access, breaches, and other security threats. It includes areas
  like network security, ethical hacking, incident response (IR), and security
  audits.
    - Subcategories: 
      - [Network Security][c-cs-ns]
      - [Web Application Security][c-cs-was]
    - Tags: `vpn`, `openvpn`, `nordvpn`, `tor`, `webapps`, `burpsuite`

- [Hardware and Devices][c-hw]
    - Subcategories: 
      - [Display and Graphics][c-hw-dng]
      - [Keyboard][c-hw-key]
      - [Mouse][c-hw-mouse]
      - [UPS Systems and Power Management][c-hw-ups]
    - Tags: `displaylink`, `usb`, `keyboard`, `mouse`, `ups`

- [Network and Systems Administration][c-nsa]
  - Involves managing and maintaining computer networks, servers, and
  infrastructure, including tasks like network setup, troubleshooting, security
  management, and system configuraton.
    - Subcategories: 
      - [Bluetooth][c-nsa-bt]
      - [Network Connectivity][c-nsa-nc]
      - [Virtualiztion][c-nsa-v]
        - [UTM][c-nsa-v-utm]
        - [Virt-Manager][c-nsa-v-vm]
        - [VirtualBox][c-nsa-v-vb]
        - *#TODO:* Proxmox &/or pfSense
    - Tags: `android`, bluetooth`, `captive portal`, `gpyc`, `gwapt`, 
            `kioptrix`, `sans`, `utm`, `virt-manager`, `virtualbox`, `vmware`

- [Operating Systems][c-os]
    - Subcategories: 
      - [Arch Linux][c-os-arch]
      - [Asahi Linux][c-os-asahi]
      - [File Systems and Disk Management][c-os-fs_dm]
      - [GRUB][c-os-grub]
      - [Kali][c-os-kali]
      - [Raspberry Pi][c-os-rpi]
      - [Localization and Internationalization][c-os-local]
        - [Language Input Methods][c-os-local-lang_input]
      - [Package Managers][c-os-pkgmgr]
      - [Shell and Command-Line][c-os-cli]
      - [Windows][c-os-win]
        - [WSL][c-os-win-wsl]
    - Tags: `bootloader`, `chinese`, `dd`, `discover`, `ext4`, `ime`, `iso`, 
            `os install`, `ramdisk`, `snap`, `xrandr`, `vmlinux`

- [Peripherals and Devices][c-pd]
    - Subcategories: 
      - [Printers][c-pd-printers]
    - Tags: `printers`, `brother`

- [Software Development][c-sd]
  - This includes areas such as application development, web development,
  mobile app development, software engineering, and programming.
    - Subcategories: 
      - [Text Editors][c-sd-tedits]
      - [Version Control Systems (VCS)][c-sd-vcs]
    - Tags: `vim`, `git`

- [Software and Applications][c-sa]
    - Subcategories: 
      - [Command-Line Ultities][c-sa-cli]
      - [System Tools][c-sa-st]
    - Tags: `autojump`, `bitwarden-cli`, ventoy`

- [Troubleshooting][c-ts]
    - Subcategories: 
    - Tags: `troubleshooting methods`, `methodology`

- [Web Browsers and Extensions][c-wbe]
    - Subcategories: 
      - [Elinks][c-wbe-elinks]
      - [Firefox][c-wbe-firefox]
      - [Links2][c-wbe-links2]
    - Tags: `bitwarden`, `elinks`, firefox`, `links2`

### Command Line Interface

### Examples

- [Example 1: Perform a basic search](#example-1-perform-a-basic-search)
- [Example 2: Perform a filename search](#example-1-perform-a-filename-search)
- [Example 3: Render MD file](#exmaple-3-render-md-file)

#### Example 1: Perform a basic search

``` bash
# Search for all files with matching occurences of insensitive case "arch"
PATTERN='arch'
grep -ri $PATTERN
```

Using `r` to search `r`ecursively through the repo and `i` to search regardless
of upper/lowercase.

#### Example 2: Perform a filename search

``` bash
# Search for all filenames with matching occurences of insenitive case "arch"
PATTERN='*arch*'
find ./ -type f -iname $PATTERN
```

Use the `*` to implement a wildcard search with flags `-type f` for filenames
and `-iname` for `i`nsensitive case searching.

#### Example 3: Render MD file

##### Method 1: GitHub

As these files are public, you can navigate to the desired file and have GitHub
render the markdown file from there.

##### Method 2: NeoVim Plugin - MardownPreview

This requires  Neo(vim)'s plugin [MarkdownPreview][mdp]. You can also refer to
my [Arch dotfiles][dotties] or [macOS dotfiles][mac-nvim] for setup.

``` bash
# Open the markdown file in vim and run the plugin
nvim +MarkdownPreview README.md
```

## Troubleshooting

:warning: Not all documents have been verified.  Additionally, some of the 
solutions may have "worked" by a random combination of attempts. So not all 
documents are guaranteed to work. "Here's looking at you, kid."

<!-- Reference Links -->

[c-cc]: https://github.com/dboyd42/it-support/tree/master/Cloud%20Computing
[c-cc-onedrive]: https://github.com/dboyd42/it-support/tree/master/Cloud%20Computing/OneDrive
[c-cs]: https://github.com/dboyd42/it-support/tree/master/Cybersecurity
[c-cs-ns]: https://github.com/dboyd42/it-support/tree/master/Cybersecurity/Network%20Security/VPN%20Services
[c-cs-was]: https://github.com/dboyd42/it-support/tree/master/Cybersecurity/Web%20Application%20Security/BurpSuite
[c-hw]: https://github.com/dboyd42/it-support/tree/master/Hardware%20and%20Devices
[c-hw-dng]: https://github.com/dboyd42/it-support/tree/master/Hardware%20and%20Devices/Display%20and%20Graphics/DisplayLink
[c-hw-key]: https://github.com/dboyd42/it-support/tree/master/Hardware%20and%20Devices/Keyboard
[c-hw-mouse]: https://github.com/dboyd42/it-support/tree/master/Hardware%20and%20Devices/Mouse/Remapping%20SW
[c-hw-ups]: https://github.com/dboyd42/it-support/tree/master/Hardware%20and%20Devices/UPS%20Systems%20and%20Power%20Management/CyberPower
[c-nsa]: https://github.com/dboyd42/it-support/tree/master/Network%20and%20Systems%20Administration
[c-os]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems
[c-pd]: https://github.com/dboyd42/it-support/tree/master/Peripherals%20and%20Devices/Printers/Brother
[c-sd]: https://github.com/dboyd42/it-support/tree/master/Software%20Development
[c-sa]: https://github.com/dboyd42/it-support/tree/master/Software%20and%20Applications
[c-ts]: https://github.com/dboyd42/it-support/tree/master/Troubleshooting
[c-wbe]: https://github.com/dboyd42/it-support/tree/master/Web%20Browsers%20and%20Extensions
[c-nsa-bt]: https://github.com/dboyd42/it-support/tree/master/Network%20and%20Systems%20Administration/Bluetooth
[c-nsa-nc]: https://github.com/dboyd42/it-support/tree/master/Network%20and%20Systems%20Administration/Network%20Connectivity
[c-nsa-v]: https://github.com/dboyd42/it-support/tree/master/Network%20and%20Systems%20Administration/Virtualization
[c-nsa-v-utm]: https://github.com/dboyd42/it-support/tree/master/Network%20and%20Systems%20Administration/Virtualization/UTM
[c-nsa-v-vm]: https://github.com/dboyd42/it-support/tree/master/Network%20and%20Systems%20Administration/Virtualization/Virt-Manager
[c-nsa-v-vb]: https://github.com/dboyd42/it-support/tree/master/Network%20and%20Systems%20Administration/Virtualization/VirtualBox
[c-os-arch]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/Arch%20Linux
[c-os-asahi]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/Asahi%20Linux%20(M1)
[c-os-fs_dm]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/File%20Systems%20and%20Disk%20Management
[c-os-grub]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/GRUB%20(Grand%20Unified%20Bootloader)
[c-os-kali]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/Kali
[c-os-rpi]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/Raspberry%20Pi
[c-os-local]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/Localization%20and%20Internationalization/Language%20Input%20Methods
[c-os-local-lang_input]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/Localization%20and%20Internationalization/Language%20Input%20Methods
[c-os-pkgmgr]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/Package%20Managers/Linux
[c-os-cli]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/Shell%20and%20Command-Line
[c-os-win]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/Windows
[c-os-win-wsl]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/Windows/WSL
[c-pd-printers-bro]: https://github.com/dboyd42/it-support/tree/master/Peripherals%20and%20Devices/Printers/Brother
[c-sd-tedits]: https://github.com/dboyd42/it-support/tree/master/Software%20Development/Text%20Editors/Vim
[c-sd-vcs]: https://github.com/dboyd42/it-support/tree/master/Software%20Development/VCS%20(Version%20Control%20Systems)/Git/git
[c-sa-cli]: https://github.com/dboyd42/it-support/tree/master/Software%20and%20Applications/Command-Line%20Utilities
[c-sa-st]: https://github.com/dboyd42/it-support/tree/master/Software%20and%20Applications/System%20Tools/Bootable%20Media%20Creation/Ventoy
[c-wbe-elinks]: https://github.com/dboyd42/it-support/tree/master/Web%20Browsers%20and%20Extensions/Elinks
[c-wbe-firefox]: https://github.com/dboyd42/it-support/tree/master/Web%20Browsers%20and%20Extensions/Firefox
[c-wbe-links2]: https://github.com/dboyd42/it-support/tree/master/Web%20Browsers%20and%20Extensions/Links2

[mdp]: https://github.com/iamcco/markdown-preview.nvim
[dotties]: https://github.com/dboyd42/dotfiles/tree/master/home/.config/nvim
[mac-nvim]: https://github.com/dboyd42/dotfiles/blob/master/macos-setup.md


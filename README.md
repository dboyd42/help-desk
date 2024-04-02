# IT Support / KBS

**Author:** David Boyd<br>
**Updated:** 2024-04-01<br>

## Table of Contents

<!-- vim-markdown-toc GFM -->

* [Introduction](#introduction)
* [KBS Overview](#kbs-overview)
  * [Cloud Computing](#cloud-computing)
  * [Hardware and Devices](#hardware-and-devices)
  * [Network and Systems Administration](#network-and-systems-administration)
  * [Operating Systems](#operating-systems)
  * [Peripherals and Devices](#peripherals-and-devices)
  * [Software Development](#software-development)
  * [Software and Applications](#software-and-applications)
  * [Web Browsers and Extensions](#web-browsers-and-extensions)
  * [Troubleshooitng](#troubleshooitng)
* [Usage](#usage)
  * [Keyword Search via grep](#keyword-search-via-grep)
  * [Filename Search via find](#filename-search-via-find)
  * [Render an MD file](#render-an-md-file)
    * [Method 1: via GitHub](#method-1-via-github)
    * [Method 2: via NeoVim Plugin - Mardown Preview](#method-2-via-neovim-plugin---mardown-preview)
* [Troubleshooting](#troubleshooting)

<!-- vim-markdown-toc -->

## Introduction

This repo acts as a knowledge-base system (KBS) for various IT issues and their
*hopeful* solutions that I have worked tirelessly through.

## KBS Overview

### [Cloud Computing][c-cc]

  * [OneDrive][c-cc-onedrive]

### [Hardware and Devices][c-hw]

  * [Display and Graphics][c-hw-dng]
  * [Keyboard][c-hw-key]
  * [Mouse][c-hw-mouse]
  * [UPS Systems and Power Management][c-hw-ups]

### [Network and Systems Administration][c-nsa]

  * [Bluetooth][c-nsa-bt]
  * [Dell PowerEdge R620][c-nsa-dell]
  * [Network Connectivity][c-nsa-nc]
  * [Remote Desktop (VNC)][c-nsa-vnc]
  * [VirtualBox][c-nsa-v-vb]
  * [Virtualization][c-nsa-v]
    * [Proxmox][c-nsa-v-proxmox]
    * [UTM][c-nsa-v-utm]
    * [Virt-Manager][c-nsa-v-vm]
    * [VirtualBox][c-nsa-v-vb]

### [Operating Systems][c-os]

  * [Arch Linux][c-os-arch]
  * [Asahi Linux (M1)][c-os-asahi]
  * [File Systems and Disk Management][c-os-fs_dm]
  * [GRUB][c-os-grub]
  * [Kali][c-os-kali]
  * [Raspberry Pi][c-os-rpi]
  * [Localization and Internationalization][c-os-local]
  * [Package Managers][c-os-pkgmgr]
  * [Shell and Command-Line][c-os-cli]
  * [Windows][c-os-win]
  * [WSL][c-os-win-wsl]

### [Peripherals and Devices][c-pd]

  * [Printers][c-pd-printers]

### [Software Development][c-sd]

  * [Text Editors][c-sd-tedits]
  * [Version Control Systems (VCS)][c-sd-vcs]

### [Software and Applications][c-sa]

  * [Command-Line Utilities][c-sa-cli]
  * [System Tools][c-sa-st]

### [Web Browsers and Extensions][c-wbe]

  * [Elinks][c-wbe-elinks]
  * [Firefox][c-wbe-firefox]
  * [Links2][c-wbe-links2]

### [Troubleshooitng][c-ts]

  * [Methodology][c-ts-methodology]

## Usage

### Keyword Search via grep

```bash
# Search for all files with matching occurrences of insensitive case "arch"
PATTERN='arch'
grep -ri $PATTERN
```
Using `-r` to search recursively through the repo and i to search regardless
of upper/lowercase.

### Filename Search via find

```bash
Copy code
# Search for all filenames with matching occurrences of insensitive case "arch"
PATTERN='*arch*'
find ./ -type f -iname $PATTERN
```

Use the `*` character to implement a wildcard search with flags `-type f` for 
filenames and `-iname` for insensitive case searching.

### Render an MD file

#### Method 1: via GitHub

As these files are public, you can navigate to the desired file and have GitHub
render the markdown file from there.

#### Method 2: via NeoVim Plugin - Mardown Preview

[!IMPORTANT] This requires Neo(vim)'s plugin [Markdown Preview][mdp]. You can also refer to
my [Arch dotfiles][dotties] or [macOS dotfiles][mac-nvim] for setup.

1. Open the markdown file in vim and run the plugin: `nvim +MarkdownPreview 
README.md`

## Troubleshooting

[!WARNING] Not all documents have been verified! 

Some of the solutions may have "worked" by a random combination of attempts. 
So not all documents are guaranteed to work. "Here's looking at you, kid."

<!-- Reference Links -->

[c-cc]: https://github.com/dboyd42/it-support/tree/master/Cloud%20Computing/OneDrive
[c-cc-onedrive]: https://github.com/dboyd42/it-support/tree/master/Cloud%20Computing/OneDrive
[c-hw]: https://github.com/dboyd42/it-support/tree/master/Hardware%20and%20Devices
[c-hw-dng]: https://github.com/dboyd42/it-support/tree/master/Hardware%20and%20Devices/Display%20and%20Graphics/DisplayLink
[c-hw-key]: https://github.com/dboyd42/it-support/tree/master/Hardware%20and%20Devices/Keyboard
[c-hw-mouse]: https://github.com/dboyd42/it-support/tree/master/Hardware%20and%20Devices/Mouse/Remapping%20SW
[c-hw-ups]: https://github.com/dboyd42/it-support/tree/master/Hardware%20and%20Devices/UPS%20Systems%20and%20Power%20Management/CyberPower
[c-nsa]: https://github.com/dboyd42/it-support/tree/master/Network%20and%20Systems%20Administration
[c-nsa-bt]: https://github.com/dboyd42/it-support/tree/master/Network%20and%20Systems%20Administration/Bluetooth
[c-nsa-dell]: https://github.com/dboyd42/it-support/tree/master/Network%20and%20Systems%20Administration/Dell%20PowerEdge%20R620
[c-nsa-nc]: https://github.com/dboyd42/it-support/tree/master/Network%20and%20Systems%20Administration/Network%20Connectivity
[c-nsa-v]: https://github.com/dboyd42/it-support/tree/master/Network%20and%20Systems%20Administration/Virtualization
[c-nsa-v-proxmox]: https://github.com/dboyd42/it-support/tree/master/Network%20and%20Systems%20Administration/Virtualization/Proxmox
[c-nsa-v-utm]: https://github.com/dboyd42/it-support/tree/master/Network%20and%20Systems%20Administration/Virtualization/UTM
[c-nsa-v-vm]: https://github.com/dboyd42/it-support/tree/master/Network%20and%20Systems%20Administration/Virtualization/Virt-Manager
[c-nsa-v-vb]: https://github.com/dboyd42/it-support/tree/master/Network%20and%20Systems%20Administration/Virtualization/VirtualBox
[c-nsa-vnc]: https://github.com/dboyd42/it-support/tree/master/Network%20and%20Systems%20Administration/Remote%20Desktop%20(VNC)
[c-os]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems
[c-os-arch]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/Arch%20Linux
[c-os-asahi]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/Asahi%20Linux%20(M1)
[c-os-fs_dm]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/File%20Systems%20and%20Disk%20Management
[c-os-grub]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/GRUB%20(Grand%20Unified%20Bootloader)
[c-os-kali]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/Kali
[c-os-local]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/Localization%20and%20Internationalization/Language%20Input%20Methods
[c-os-pkgmgr]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/Package%20Managers/Linux
[c-os-rpi]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/Raspberry%20Pi
[c-os-cli]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/Shell%20and%20Command-Line
[c-os-win]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/Windows
[c-os-win-wsl]: https://github.com/dboyd42/it-support/tree/master/Operating%20Systems/Windows/WSL
[c-pd]: https://github.com/dboyd42/it-support/tree/master/Peripherals%20and%20Devices/Printers/Brother
[c-pd-printers]: https://github.com/dboyd42/it-support/blob/master/Peripherals%20and%20Devices/Printers/Brother/How%20to%20Bypass%20Toner%20Warning%20on%20a%20Brother%20DCP-L2540DW%20Printer.md
[c-sd]: https://github.com/dboyd42/it-support/tree/master/Software%20Development
[c-sd-tedits]: https://github.com/dboyd42/it-support/tree/master/Software%20Development/Text%20Editors/Vim
[c-sd-vcs]: https://github.com/dboyd42/it-support/tree/master/Software%20Development
[c-sa]: https://github.com/dboyd42/it-support/tree/master/Software%20and%20Applications
[c-sa-cli]: https://github.com/dboyd42/it-support/tree/master/Software%20and%20Applications/Command-Line%20Utilities
[c-sa-st]: https://github.com/dboyd42/it-support/tree/master/Software%20and%20Applications/System%20Tools/Bootable%20Media%20Creation/Ventoy
[c-ts]: https://github.com/dboyd42/it-support/tree/master/Troubleshooting
[c-ts-methodology]: https://github.com/dboyd42/it-support/blob/master/Troubleshooting/Troubleshooting%20Methods.md
[c-wbe]: https://github.com/dboyd42/it-support/tree/master/Web%20Browsers%20and%20Extensions
[c-wbe-elinks]: https://github.com/dboyd42/it-support/tree/master/Web%20Browsers%20and%20Extensions/Elinks
[c-wbe-firefox]: https://github.com/dboyd42/it-support/tree/master/Web%20Browsers%20and%20Extensions/Firefox
[c-wbe-links2]: https://github.com/dboyd42/it-support/tree/master/Web%20Browsers%20and%20Extensions/Links2
[mdp]: https://github.com/iamcco/markdown-preview.nvim
[dotties]: https://github.com/dephraiim/dotfiles
[mac-nvim]: https://github.com/dephraiim/dotfiles/blob/main/nvim/vimrc


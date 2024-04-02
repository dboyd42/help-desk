# IT Support / KBS

**Author:** David Boyd<br>
**Updated:** 2024-04-01<br>

## Table of Contents

<!-- vim-markdown-toc GFM -->

* [Introduction](#introduction)
* [Overview](#overview)
  * [Cloud Computing](#cloud-computing)
  * [Hardware and Devices](#hardware-and-devices)
  * [Network and Systems Administration](#network-and-systems-administration)
  * [Operating Systems](#operating-systems)
  * [Peripherals and Devices](#peripherals-and-devices)
  * [Software Development](#software-development)
  * [Software and Applications](#software-and-applications)
  * [Web Browsers and Extensions](#web-browsers-and-extensions)
* [Usage](#usage)
  * [Keyword Search via grep](#keyword-search-via-grep)
  * [Filename Search via find](#filename-search-via-find)
  * [Render an MD file](#render-an-md-file)
    * [Method 1: GitHub](#method-1-github)
    * [Method 2: NeoVim Plugin - Mardown Preview](#method-2-neovim-plugin---mardown-preview)
      * [Open the markdown file in vim and run the plugin:](#open-the-markdown-file-in-vim-and-run-the-plugin)
  * [Troubleshooting](#troubleshooting)

<!-- vim-markdown-toc -->

## Introduction

This repo acts as a knowledge-base system (KBS) for various IT issues and their
*hopeful* solutions that I have worked tirelessly through. The repo has been
updated to fit a more IT KBS structure. 

## Overview

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

#### Method 1: GitHub

As these files are public, you can navigate to the desired file and have GitHub
render the markdown file from there.

#### Method 2: NeoVim Plugin - Mardown Preview
This requires Neo(vim)'s plugin [Markdown Preview][mdp]. You can also refer to
my [Arch dotfiles][dotties] or [macOS dotfiles][mac-nvim] for setup.

##### Open the markdown file in vim and run the plugin:

``` bash
nvim +MarkdownPreview README.md
```

### Troubleshooting

:warning: Not all documents have been verified! 

Some of the solutions may have "worked" by a random combination of attempts. 
So not all documents are guaranteed to work. "Here's looking at you, kid."

<!-- Reference Links -->

<!-- Reference Links -->

[c-cc]: ./tree/master/Cloud%20Computing
[c-cc-onedrive]: ./tree/master/Cloud%20Computing/OneDrive
[c-hw]: ./tree/master/Hardware%20and%20Devices
[c-hw-dng]: ./tree/master/Hardware%20and%20Devices/Display%20and%20Graphics/DisplayLink
[c-hw-key]: ./tree/master/Hardware%20and%20Devices/Keyboard
[c-hw-mouse]: ./tree/master/Hardware%20and%20Devices/Mouse/Remapping%20SW
[c-hw-ups]: ./tree/master/Hardware%20and%20Devices/UPS%20Systems%20and%20Power%20Management/CyberPower
[c-nsa]: ./tree/master/Network%20and%20Systems%20Administration
[c-nsa-bt]: ./tree/master/Network%20and%20Systems%20Administration/Bluetooth
[c-nsa-dell]: ./tree/master/Network%20and%20Systems%20Administration/Dell%20PowerEdge%20R620
[c-nsa-nc]: ./tree/master/Network%20and%20Systems%20Administration/Network%20Connectivity
[c-nsa-v]: ./tree/master/Network%20and%20Systems%20Administration/Virtualization
[c-nsa-v-proxmox]: ./tree/master/Network%20and%20Systems%20Administration/Virtualization/Proxmox
[c-nsa-v-utm]: ./tree/master/Network%20and%20Systems%20Administration/Virtualization/UTM
[c-nsa-v-vm]: ./tree/master/Network%20and%20Systems%20Administration/Virtualization/Virt-Manager
[c-nsa-v-vb]: ./tree/master/Network%20and%20Systems%20Administration/Virtualization/VirtualBox
[c-nsa-vnc]: ./tree/master/Network%20and%20Systems%20Administration/Remote%20Desktop%20(VNC)
[c-os]: ./tree/master/Operating%20Systems
[c-os-arch]: ./tree/master/Operating%20Systems/Arch%20Linux
[c-os-asahi]: ./tree/master/Operating%20Systems/Asahi%20Linux%20(M1)
[c-os-fs_dm]: ./tree/master/Operating%20Systems/File%20Systems%20and%20Disk%20Management
[c-os-grub]: ./tree/master/Operating%20Systems/GRUB%20(Grand%20Unified%20Bootloader)
[c-os-kali]: ./tree/master/Operating%20Systems/Kali
[c-os-local]: ./tree/master/Operating%20Systems/Localization%20and%20Internationalization
[c-os-pkgmgr]: ./tree/master/Operating%20Systems/Package%20Managers/Linux
[c-os-rpi]: ./tree/master/Operating%20Systems/Raspberry%20Pi
[c-os-cli]: ./tree/master/Operating%20Systems/Shell%20and%20Command-Line
[c-os-win]: ./tree/master/Operating%20Systems/Windows
[c-os-win-wsl]: ./tree/master/Operating%20Systems/Windows/WSL
[c-pd]: ./tree/master/Peripherals%20and%20Devices
[c-pd-printers]: ./tree/master/Peripherals%20and%20Devices/Printers
[c-sd]: ./tree/master/Software%20Development
[c-sd-tedits]: ./tree/master/Software%20Development/Text%20Editors/Vim
[c-sd-vcs]: ./tree/master/Software%20Development/VCS%20(Version%20Control%20Systems)/Git
[c-sa]: ./tree/master/Software%20and%20Applications
[c-sa-cli]: ./tree/master/Software%20and%20Applications/Command-Line%20Utilities
[c-sa-st]: ./tree/master/Software%20and%20Applications/System%20Tools
[c-ts]: ./tree/master/Troubleshooting
[c-wbe]: ./tree/master/Web%20Browsers%20and%20Extensions
[c-wbe-elinks]: ./tree/master/Web%20Browsers%20and%20Extensions/Elinks
[c-wbe-firefox]: ./tree/master/Web%20Browsers%20and%20Extensions/Firefox
[c-wbe-links2]: ./tree/master/Web%20Browsers%20and%20Extensions/Links2
[mdp]: https://github.com/iamcco/markdown-preview.nvim
[dotties]: https://github.com/dephraiim/dotfiles
[mac-nvim]: https://github.com/dephraiim/dotfiles/blob/main/nvim/vimrc


# How to Enable Multiple Monitors in Kali Linux via DisplayLink

**Author:** David Boyd</br>
**Date:** 2022-02-10

---
---

**:exclamation:I'm using GNOME for my desktop manager:exclamation:**
  - Therefore, I don't know if this'll work with the default Xfce layout.  If
    you want to switch to Gnome, then follow this
    [guide](./desktop-mgr-kali.txt)

## Requirements

  - DisplayLink adapter/device
  - [DisplayLink Driver][d]

## Current Environment

| Setting         | Cmd                         | Description
|-----------------|-----------------------------|-------------------------------------------------------------------------------------|
| Kernel/OS       | `uname -a`                  | Linux 5.15.0-kali3-amd64 #1 SMP Debian 5.15.15-2kali1 (2022-01-31) x86_64 GNU/Linux |
| Desktop Manager | `echo $XDG_CURRENT_DESKTOP` | GNOME                                                                             |


## Steps


### 1. Install DisplayLink Driver


1. Install [DisplayLink USB Graphics Software for Ubuntu (Beta)(5.5 Beta)][1]
2. Extrac the zip folder
3. Run the `displaylink-driver-5.5.0-beta-59.118.run` as `sudo`
4. Restart computer

### 2. Display Detection

> This section is copy and pasted from @AdnanHodzic's [Post-Install-Guide][2]

Only do this in case your monitors weren't automatically detected.

First run `xrandr --listproviders`.
The output should be similar to this:
```
Providers: number : 5
Provider 0: id: 0x44 cap: 0x9, Source Output, Sink Offload crtcs: 3 outputs: 2 associated providers: 0 name:Intel
Provider 1: id: 0x138 cap: 0x2, Sink Output crtcs: 1 outputs: 1 associated providers: 0 name:modesetting
Provider 2: id: 0x116 cap: 0x2, Sink Output crtcs: 1 outputs: 1 associated providers: 0 name:modesetting
Provider 3: id: 0xf4 cap: 0x2, Sink Output crtcs: 1 outputs: 1 associated providers: 0 name:modesetting
Provider 4: id: 0xd2 cap: 0x2, Sink Output crtcs: 1 outputs: 1 associated providers: 0 name:modesetting
```
Notes:
* Provider 0 is the actual graphics provider and 1-4 are DisplayLink providers.
* All providers have 0 associated providers. Which means that we will have to connect all the DisplayLink providers to the main provider.

We can do this with the command `xrandr --setprovideroutputsource <prov-xid> <source-xid>`
In this case we would run:
```
xrandr --setprovideroutputsource 1 0
xrandr --setprovideroutputsource 2 0
xrandr --setprovideroutputsource 3 0
xrandr --setprovideroutputsource 4 0
```
If we would re-run `xrandr --listproviders` this would output:
```
Providers: number : 5
Provider 0: id: 0x44 cap: 0x9, Source Output, Sink Offload crtcs: 3 outputs: 2 associated providers: 4 name:Intel
Provider 1: id: 0x138 cap: 0x2, Sink Output crtcs: 1 outputs: 1 associated providers: 1 name:modesetting
Provider 2: id: 0x116 cap: 0x2, Sink Output crtcs: 1 outputs: 1 associated providers: 1 name:modesetting
Provider 3: id: 0xf4 cap: 0x2, Sink Output crtcs: 1 outputs: 1 associated providers: 1 name:modesetting
Provider 4: id: 0xd2 cap: 0x2, Sink Output crtcs: 1 outputs: 1 associated providers: 1 name:modesetting
```

For further reference I suggest reading:
[How to use xrandr](https://web.archive.org/web/20180224075928/https://pkg-xorg.alioth.debian.org/howto/use-xrandr.html)

***...***

### 3. GNOME Displays

If you're GNOME desktop user, simply run:

`gnome-control-center display`

> "END" copy and Paste.

In GNOME's display manager,

1. Select the 3rd screen from the drop down menu.
2. Enable the screen by toggling the switch to the right of the drop-down menu.

# 4. :champagne:Enjoy Your Multiple Monitors!:champagne:

<!-- links                                                                  -->

[1]: [https://www.synaptics.com/products/displaylink-graphics/downloads/ubuntu-5.5-Beta?filetype=exe]
[2]: [https://github.com/AdnanHodzic/displaylink-debian/blob/master/post-install-guide.md]


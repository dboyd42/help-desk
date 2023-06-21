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

Reference Guide: [Post-Install-Guide][2]

```bash
# Display detection
xrandr --listproviders

# Connect all the DisplayLink providers to the main power
for i in {1..4}; do xrandr --setprovideroutputsource $i 0; done
```

#### Persistence

To set up persistence:

1. Write the following code into your `~/.profile` file.

```bash
# Setup Multiple Monitors via DisplayLink
# Connect all the DisplayLink providers to the main power
for i in {1..4}; do xrandr --setprovideroutputsource $i 0; done
gnome-control-center display &
```

2. Configure GNOME display (see step 3).

### 3. GNOME Displays

If you're GNOME desktop user, simply run: `gnome-control-center display` or got
to Settings > Display.

In GNOME's display manager,

1. Select the 3rd screen from the drop down menu.
2. Enable the screen by toggling the switch to the right of the drop-down menu.
3. Apply changes.

# 4. :champagne:Enjoy Your Multiple Monitors!:champagne:

<!-- links                                                                  -->

[1]: (https://www.synaptics.com/products/displaylink-graphics/downloads/ubuntu-5.5-Beta?filetype=exe)
[2]: [https://github.com/AdnanHodzic/displaylink-debian/blob/master/post-install-guide.md]


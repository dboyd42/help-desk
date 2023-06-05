# How to Install Asahi Linux on an M1 MacBook Pro

**Author:** David Boyd<br>
**Date:** 2023-06-04

## Table of Contents

- [Steps](#steps)
  - [Step 1: Installing Asahi](#step-1-installing-asahi)
  - [Step 2: Post-Arch Installation](#step-2-post-arch-installation)
  - [Step 3: Upgrade the GPU Drivers](#step-3-upgrade-the-gpu-drivers)
- [Tips and Best Practices](#tips-and-best-practices)

## Steps

### Step 1: Installing Asahi

The setup is rather easy and is self-explanatory, so I won't go into the
details as the Asahi team did an amazing job. For reference, please hit up the
[official Asahi documentation][asahi-install].

1. Open a terminal on macOS and install Asahi.

``` bash
curl https://alx.sh | sh
```

2. Follow the instructions.

### Step 2: Post-Arch Installation

1. My personal guide can be found *[here][basic-arch-install]*. :warning: It's
   a bit of a mess at the moment.

### Step 3: Upgrade the GPU Drivers

1. Install Wayland (:warning: X11 has noticable screen tearing :dizzy_face:)

``` bash
# Synchronize and update all packages
sudo pacman -Syu
# Install Wayland
sudo pacman -S plasma-wayland-session
# Install Wayland clipboard support (if not already installed)
#   *This also aids with NeoVim's unnamed clipboard!
sudo pacman -S wl-clipboard
```

2. Install the Asahi and Mesa drivers

The M1 GPU driver support *doesn't* come pre-installed as I'm sure these
drivers are prone to issues (albeit not having come across any myself... yet
:pray:). Check out the official articles and instructions [here][gpu-drivers] and
[here][road-to-vulkan].

```
# Install the drivers (and accept the removal of the other driver)
sudo pacman -S linux-asahi-edge mesa-asahi-edge
# Update grub so you won't boot into Zork
sudo update-grub
```
## Tips and Best Practices

After reboot, lower the resolution to a more comfortable setting by going to
`Settings` > `Hardware` > `Display and Monitor` > `Scale` > `150%`.

<!-- Reference Links -->
[asahi-install]: https://asahilinux.org/2022/03/asahi-linux-alpha-release/
[basic-arch-install]: ../arch-linux/README.md
[gpu-drivers]: https://asahilinux.org/2022/12/gpu-drivers-now-in-asahi-linux/
[road-to-vulkan]: https://asahilinux.org/2023/03/road-to-vulkan/

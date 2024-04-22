# How to Install Hyprland on Arch Linux

**Author:** David Boyd<br>
**Date:** 2024-04-22

## Table of Contents

## Overview

## Installation

### 1. Install Dependecies

#### GUI Widget Toolkits

``` bash
# QT
pacman -S qt6ce qt6-wayland

# GTK (Install these even if you're "only" running QT)
pacman -S gtk3 gtk4

# Hyprland recommends the following for a GTK setup
pacamn -S nwg-look

# Hyprland's recommended terminal
pacman -S kitty  # Optional
```

### 2. Install Hyprland

``` bash
pacman -S hyprland
```

### 3. Set Environment Variables

Configure the following env vars in the `~/.config/hypr/hyprland.conf` file.

``` bash
env = QT_QPA_PLATFORM,wayland
env = QT_QPA_PLATFORMTHEME,qt6ct
```

:bulb: For good measure, I have a terminal open upon launch to determine if
there's an issue with loading the configuration file.

``` bash
exec-once = /usr/bin/kitty
```

## Run Hyprland

``` bash
# From terminal
Hyprland
```

## Troubleshooting

### $maidMod Key Not Working

| Resolved | :heavy_check_mark: |
|----------|--------------------|

### Solution

> :bulb: Unsure of the exact solution, but by performing the following steps, 
> I was able to get my keys working on the Hyprland compositor.

### 1. Set the Console Keyboard Layout to Persistent Configuration

> :pencil: For some reason, the `/etc/vconsole.conf` was not filled out.

``` bash
# Create a backup file
cp /etc/vconsole.conf /etc/vconsole.conf.bak

# Find your country code
localectl list-keymaps

# Load keys for the current session
loadkeys us

# Set keymap persistence and auto-change the Xorg keymap to the nearest match
localectl set-keymap us

# Reboot
reboot 0
```

:bulb: Determine if `Hyprland` is properly running before going to step 2.

### 2. Install `wofi`

> :pencil: I'm unsure of why this worked, but Hyprland began to function
> properly after installation...
>> Even after running `pacman -Rns wofi`, Hyprland continued to function
>> properly.

``` bash
# Install wofi
pacman -S wofi

# Run Hyprland
Hyprland
```

### Error Summary

Upon loading `Hyprland`, no keys seemed to properly function.


<!-- References -->

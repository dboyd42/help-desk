# 'Alt' Key Not Registering (+) G305 Mouse Cursor Not Moving

> Author: David Boyd<br>
> Date: 2023-03-09<br>
> Status: Resolved

System Settings:

|         |                  |
|---------|------------------|
| Mfg     | Lenovo           |
| Product | ThinkBook        |
| OS      | Arch - ArcoLinux |
| DE      | KDE Plasma       |

## Issue

### Summary

The left `Alt` was not working when running Emacs shortcuts in terminal.  This
was validated with and preset and custom shortcuts such as `Alt` + `Tab` to
switch applications.  This applied to the right `Alt` as well.

### Root Cause

Most likely a hardware issue as the solutions to the probable causes did not
fix the issue upon reboot.  Long story short, this laptop was dropped from a
second floor onto a tile floor and everything came loose (yet surprisingly
still functional) thus requiring all the internal connections to be
re-slotted/reconnected: RAM, keyboard, touchpad, etc.

#### Other Probable Causes

Previous possible factors that may have affected the non-registering key:

- Having the keyboard layout switched out via KDE shortcut: `Alt` + `Shift`
- Troubleshooting the Logitech G305 mouse (no movement, but buttons work)
  - Enabling/disabling `logid.service`
  - Running/closing Piper (mouse controls)
  - An issue in [keyd](https://github.com/rvaiya/keyd) was fixed in issue
  [#441](0fb86d3a95f0c91a4266391d05158cfd5dd4500f).  When the G305 mouse
  receiver was plugged in, the Keyd service took over the mouse controls and
  incorrectly identified and modified the keyboard layout.

## Solution

## 1. Reconnect Keyboard Ribbon

1. Open laptop and disconnect battery.
2. Remove keyboard ribbon and reconnect.
3. Reconnect battery
4. Boot and verify functionality
5. Reboot and verify functionality

If problem persists, proceed to solution #2.

### 2. G305 Cursor Solution

Update the Keyd program:

1. Go to [Keyd's Github page](https://github.com/rvaiya/keyd) and follow the
   instructions to install.

Your configuration files will still remain and be active upon enabling the
service.

If problem persists, proceed to solution #3.

### 3. Reset KDE's Keyboard Settings' Layouts

***Note: The original solution order was resetting KDE's keyboard layout below,
and then applying the update to the Keyd service.  By doing this second, it
shouldn't alter the fix for the `Alt` key.**

Reset and switch keyboard layout in KDE's Settings:

1. Open KDE's Settings > Hardware > Input Devices > Keyboard

- Hardware tab:
  - Keyboard model: Generic | Generic 104-key PC
  - NumLock on Plasma Startup: Turn on
  - **When a key is held: Repeat the key**

- Layouts tab:
  - Switching Policy: Global
  - Shortcuts for Switching Layout: None, None, None
    - OSD on layout change: [Check]

- Advanced tab:
  - Configure keyboard options: [Check]
    - **Switching to another layout:**
      - **Alt+Shift: [Check]**

- Apply

2. Press the `Alt` + `Shift` once to **switch to another layout**.
3. Disable the "Configure keyboard options"; then click "Apply".
4. Verify the 'Alt' key functionality.

## Preventive Measures

1. Don't drop laptop from the second floor.
2. Be weary of updates/upgrades and their affects on 3rd party services and
   programs, and desktop environment settings.

By updating the Keyd service, the mouse malfunction should work from here on
out.

Before updating the Keyd service:

- By disabling the "Switch to another layout" in the "Configure keyboard
  options", the user shouldn't be able to disable the current layout.  However,
  if the advanced user wishes to customize their layouts, it may be best to map
  this feature to another key combination.
- Additionally, by having the  **When a key is held:** Repeat the key

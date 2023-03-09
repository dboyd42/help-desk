# 'Alt' Key Not Properly Registering

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
switch applications.  This applied to the rigt `Alt` as well.

### Root Cause

Factors that may have affected the non-registering key:

- ***Having the keyboard layout switched out via KDE shortcut: `Alt` +
     `Shift`***

- Troubleshooting the Logitech G305 mouse (no movement, but buttons work)
  - Enabling/disabling `logid.service`
  - Running/closing Piper (mouse controls)


## Solution

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

By disabling the "Switch to another layout" in the "Configure keyboard
options", the user shouldn't be able to disable the current layout.  However,
if the advanced user wishes to customize their layouts, it may be best to map
this feature to another key combination.

Additionally, by having the  **When a key is held:** Repeat the key

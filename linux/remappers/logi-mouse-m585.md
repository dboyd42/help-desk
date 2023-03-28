# Remap Logitech Mouse - M585

> Author: David Boyd<br>
> Date: 2023-03-27

# About

[Input Remapper (Official)](https://github.com/sezanzeb/input-remapper/)

|    |            |
|----|------------|
| OS | Arch       |
| DE | KDE Plasma |
| WE | X11        |

# Installation

1. Install AUR pkg and enable

    ``` bash
    yay -S input-remapper-git
    sudo systemctl restart input-remapper
    sudo systemctl enable input-remapper
    ```

2. Open Input Remapper & Configure:

    1. Input Remapper
    2. Choose Device: `M585/M590 Mouse`
    3. Open `new preset`
    4. Input > Record: Click button to remap: Button EXTRA
    5. Output:
        - Type: Key or Macro
        - Target: keyboard
        - Enter your output here: KEY_LEFTCTRL + KEY_C
    6. Input > Record: Click button to remap: Button SIDE
    7. Output:
        - Type: Key or Macro
        - Target: keyboard
        - Enter your output here: KEY_LEFTCTRL + KEY_V
    8. Rename preset: Copy_Paste
    9. Save (Click the floppy disk icon)
    10. Autoreload: Enable
    11. Apply

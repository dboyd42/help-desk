# Chinese IME/IMF on Arch Linux

> Author: David Boyd<br>
> Date: 2023-03-27

## About

Integrate Chinese input via Pinyin on Arch Linux.

| Status:   | :heavy_check_mark: Running |
|-----------|----------------------------|
| Platform: | Arch Linux                 |
| DE:       | KDE Plasma                 |
| IME/IMF:  | fcitx5                     |

## Conflicts

| Issue                                     | Resolution/Workaround           |
|-------------------------------------------|---------------------------------|
| :x: Konsole terminal doesn't input 漢字 | :arrow_right: 用 Xfce4-Terminal |

## Installation

| Package               | Description                     | Class     |
|-----------------------|---------------------------------|-----------|
| fcitx5                | Google's IME                    | fcitx5-im |
| fcitx5-configtool     | Frontend tool                   | fcitx5-im |
| fcitx5-gtk            | GUI                             | fcitx5-im |
| fcitx5-qt             | GUI                             | fcitx5-im |
| fctix5-chinese-addons | Traditional Characters' Library |           |
| fctix5-pinyin-zhwiki  | Pinyin Dictionary               |           |


1. Install fctix5: `pacman -S fcitx5-im fcitx5-chinese-addons
   fcitx5-pinyin-zhwiki`
2. Add environment variables to bashrc/zshrc file:

    ``` bash
    export GTK_IM_MODULE=fcitx5
    QT_IM_MODULE=fcitx5
    XMODIFIERS=@im=fcitx5
    ```

    :penci2: The Arch Wiki will state to not append the '5', but this appears
    to have no adverse effect.

3. Configure Pinyin keyboard:
    1. **Navigate to Fcitx 5:** System Settings > Regional Settings > Add
    Input Method
    2. **Add Pinyin Keyboard:** Filter: "Pinyin" > 简体中文（中国）> Pinyin >
    Add
    3. **Apply Settings:** Apply

4. Configure Input Method Pinyin (Keyboard Settings):

      | Option                                    | Value                   |
      |-------------------------------------------|-------------------------|
      | Page size:                                | 7                       |
      | Enable Spell:                             | :ballot_box_with_check: |
      | Enable Emoji:                             | :ballot_box_with_check: |
      | Enable Chaizi:                            | :ballot_box_with_check: |
      | Enable Chars in Unicode CJK Extension B:  | :ballot_box_with_check: |
      | Enable Cloud Pinyin:                      | :ballot_box_with_check: |
      | Cloud Pinyin Index:                       | 2                       |
      | Show preedit within application:          | :ballot_box_with_check: |
      | Fix embedded preedit cursor @beg preedit: | :ballot_box_with_check: |
      | Show complete pinyin in preedit:          | :ballot_box_with_check: |
      | Enable Prediction:                        | :ballot_box_with_check: |
      | Prediction Size:                          | 10                      |
      | Action when switching input method:       | Commit current preedit  |
      | Forget word:                              | Ctrl+7                  |
      | Previous Page:                            | -, Up, kP_Up            |
      | Next Page:                                | =, Down, kP_Down        |
      | Previous Candidate:                       | Shift+Tab               |
      | Next Candidate:                           | Tab                     |
      | Select 2nd Candidate:                     | (blank)                 |
      | Select 3d Candidate:                      | (blank)                 |
      | Use Keypad as Selection key:              | :black_square_button:   |
      | Choose Character from Phrase:             | [                       |
      | Choose Character from Phrase:             | ]                       |
      | Use BackSpace to cancel the selection:    | :ballot_box_with_check: |
      | Filter by stroke:                         | `                       |
      | Number of Sentences:                      | 2                       |
      | Prompt long word len when input len over: | 4                       |
      | Dictionaries:                             | zhwiki                  |
      | Punctuation:                              | (default)               |

      | Simplified & Trad'l Chinese Translation       | Value        |
      |-----------------------------------------------|--------------|
      | Translation engine:                           | Open CC      |
      | Toggle key:                                   | Ctrl+Shift+F |
      | OpenCC profile for Simplified to Traditional: | (blank)      |
      | OpenCC profile for Traditional to Simplified: | (blank)      |

      | Cloud Pinyin           | Value            |
      |------------------------|------------------|
      | Toggle Key:            | Ctrl+Alt+Shift+C |
      | Minimum Pinyin Length: | 4                |
      | Backend                | GoogleCN         |
      | Proxy:                 | (blank)          |

      | Option (cont'd)                  | Value              |
      |----------------------------------|--------------------|
      | Key to trigger quickphrase:      | ;                  |
      | Use V to triggher quickphrase    | :ballot_box_with_check: |
      | Quick Phrase:                    | (blank)            |
      | Strings to trigger quick phrase: | (default)          |

      | Fuzzy Pinyin Settings                         | Value                   |
      |-----------------------------------------------|-------------------------|
      | ue -> ve:                                     | :ballot_box_with_check: |
      | Common Typo:                                  | :ballot_box_with_check: |
      | Inner Segment (xian -> xi'an):                | :ballot_box_with_check: |
      | Inner Segment for Short Pinyin (qie -> qi'e): | :ballot_box_with_check: |
      | Match partial finals (e -> en, eng, ei):      | :ballot_box_with_check: |
      | (Remaining Settings):                         | :black_square_button:   |

5. Customize Options:

    - **Global Options:**<br>

      | Hotkey                                   | Value                   |
      |------------------------------------------|-------------------------|
      | Trigger Input Method:                    | Super+Space             |
      | Enum when press trigger key repeatedly:  | :ballot_box_with_check: |
      | Temp switch b/t 1st & curr Input Method: | Left Shift              |
      | Enumerate Input Method Forward:          | Ctrl+Left Shift         |
      | Enumerate Input Method Backward:         | Ctrl+Right Shift        |
      | Skip first input method while enum:      | :black_square_button:   |
      | Enum Input Method Group Forward:         | (blank)                 |
      | Enum Input Method Group Backward:        | (blank)                 |
      | Activate Input Method:                   | (blank)                 |
      | Deactivate Input Method:                 | (blank)                 |
      | Default Previous page:                   | Up                      |
      | Default Next page:                       | Down                    |
      | Default Previous Candidate:              | Shift+Tab               |
      | Default Next Candidate:                  | Tab                     |
      | Toggle embedded preedit:                 | Ctrl+Alt+P              |

      | Behavior                          | Value                   |
      |-----------------------------------|-------------------------|
      | Active By Default:                | :black_square_button:   |
      | Share Input State:                | No                      |
      | Show preedit in application:      | :ballot_box_with_check: |
      | Show IM Info when changing focus: | :ballot_box_with_check: |
      | Show compact input method info:   | :ballot_box_with_check: |
      | Show first input method info:     | :ballot_box_with_check: |
      | Default page size:                | 5                       |
      | Override Xkb Option:              | :black_square_button:   |
      | Custom Xkb Option:                | (blank)                 |

6. Configure addons...

    All settings are set to their defaults.


## Notes

- **System Settings > Shortcusts > Keyboard Layout Switcher:** None.
- **Hardware > Input Devices > Keyboard > Layouts:** English (US) only.


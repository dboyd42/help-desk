# AutoJump Troubleshooting

> Author: David Boyd<br>
> Date: 2023-05-21

# Issue: ModuleNotFoundError autojump_argparse

> Date: 2023-05-21<br>
> Ref: [Install Autojump - Official][aj-install]

**Root Cause:** Arch update: `pacman -Syu`

**Solution:** Reinstall the package manually.

1. Remove the current package: `pacman -Rns autojump` or `yay -Rns autojump`
2. Download the repo: `git clone https://github.com/wting/autojump.git`
3. Install the package: `cd autojump && ./install.py`
4. Update ZSH config: :bulb: *Note: These lines differ slightly from the
previous install!*
```
[[ -s /home/bhatm/.autojump/etc/profile.d/autojump.sh ]] && source /home/bhatm/.autojump/etc/profile.d/autojump.sh
autoload -U compinit && compinit -u
```

5. Restart shell

All previously saved autojump configs should be active.

<!-- Reference Links -->

[aj-install]: https://github.com/wting/autojump/blob/master/docs/install.md

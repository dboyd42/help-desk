# [SOLVED] Module evdi Not found in Directory

> Author: David Boyd<br>
> Date: 2023-03-01

## About evdi

| Property        | Value                                        |
|-----------------|----------------------------------------------|
| EVDI            | [Extensible Virtual Display Interface][evdi] |
| Current Version | [evdi-git 1.12.0.r1.gb884877-1][evdi-git]    |
| Dependency of   | [DisplayLink][]                              |
| Dependencies    | None                                         |

### Duplicate Error

1. Upgrade Linux kernel to 6.2.-arch1-1: `pacman -Syyu`
2. Start/Enable DisplayLink: `sudo systemctl enable --now dispalylink.service`

## Error Logs

``` bash
journalctl -xeu displaylink.service

modprobe[3528]: modprobe: FATAL: Module evdi not found in directory /lib/modules/6.2.1-arch1-1
systemd[1]: displaylink.service: Control process exited, code=exited, status=1/FAILURE
```

## Solution

> Reference URL: [Kernel update to 6.2.1-arch1-1 broke evdi-git][archwiki]

1. Clone the evdi-git repo: `git clone https://aur.archlinux.org/evdi-git.git`
2. Prepare/extract the repo: `makepkg -o`
3. Replace the `evdi_fb.c` file with [evdi_fb.c-2023_03_01][evdi-2023]

    - `cp ./files/evdi_fb.c-2023_03_01 evdi-git/src/evdi/module/evdi_fb.c`
      - Reference code:
        [Pull#401](https://github.com/DisplayLink/evdi/pull/401),
        [Issue#402](https://github.com/DisplayLink/evdi/issues/402)

4. Compile the modified repo: `makepkg -e`
5. Install the `evdi-git` package: `pacman -U`
6. Verify DisplayLink's service:
    - Start the service: `sudo systemctl start displaylink.service`
    - Verify the status: `sudo systemctl status displaylink.service`

[archwiki]: https://bbs.archlinux.org/viewtopic.php?pid=2087381
[DisplayLink]: https://aur.archlinux.org/packages/displaylink
[evdi]: https://github.com/DisplayLink/evdi
[evdi-2023]: ./files/evdi_fb.c-2023_03_01
[evdi-git]: https://aur.archlinux.org/packages/evdi-git

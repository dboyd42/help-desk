# [Discover] Failed Offline Update (SOLVED)

> Author: David Boyd<br>
> Date: 2023-03-01

| Property | Value      |
|----------|------------|
| Distro   | Arch       |
| Bug      | [450973][] |

## Reproduce Error

1. Either:
    - an upgrade to kernel module 6.2.1-arch1-1
    - Removing the `ffmpeg-git` package and all of its dependencies

2. Error appears as a notification upon boot
    - Error message: `Failed to update database: unexpected system error`

## Error Log

``` bash
cat  /var/lib/PackageKit/offline-update-competed

  [PackageKit Offline Update Results]
  Success=false
  ErrorCode=failed-initialization
  ErrorDetails=failed to update database: unexpected system error
```

## Solution

1. Delete the `offline-update-competed` file: `sudo rm
   /var/lib/PackageKit/offline-update-competed`

*Note: Unlike the [450973] webpage, the error does not reappear upon boot.*

[450973]: https://www.mail-archive.com/kde-bugs-dist@kde.org/msg783159.html

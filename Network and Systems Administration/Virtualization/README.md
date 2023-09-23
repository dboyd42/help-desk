# Virtualization

**Author:** David Boyd<br>
**Date:** 2023-09-23

## Table of Contents

<!-- vim-markdown-toc GFM -->

* [QEMU Commands](#qemu-commands)
  * [Create QCOW2 Image](#create-qcow2-image)

<!-- vim-markdown-toc -->

## QEMU Commands

| Option      | Argument  | Description              |
|-------------|-----------|--------------------------|
| `-system`   | `-x86_64` | ISO's CPU architechture  |
| `-m`        | `4G`      | VM's memory set to 4 GB  |
| `-boot`     | `d`       | VM's boot set to disk    |
| `-smp`      | `2`       |                          |
| `-hda`      |           |                          |
| `out.qcow2` |           | VM's output name and ext |

### Create QCOW2 Image

``` bash
qemu -system -x86_64 -m 4G -boot d -smp 2 -hda gmob.qcow2
```

<!-- References -->


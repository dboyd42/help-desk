# Proxmox Cheat Sheet

**Author:** David Boyd<br>
**Date:** 2023-06-30

- [Virtual Machines](#virtual-machines)
  - [Installing VMs](#installing-vms)
    - [Install VM via CLI](#install-vm-via-cli)
  - [VM Troubleshooting](#vm-troubleshooting)
    - [Force Shutdown a VM](#force-shutdown-a-vm)

## Virtual Machines

### Installing VMs

#### Install VM via CLI

``` bash
# 0. Create a sandbox directory in /tmp
mkdir /tmp/sandbox && cd $_
curl -O https://kali.download/base-images/kali-2023.2/kali-linux-2023.2a-installer-amd64.iso

# 1.0 *If necessary, decompress image. I.e.)
gunzip pfSense-CE-2.7.0-RELEASE-adm64.gz

# 1.1 Move or copy ISO image to ISO Images directory
mv kali-linux2023.2a-installer-amd64.iso
```

### VM Troubleshooting

#### Force Shutdown a VM

``` bash
# 1. Find lock file
ls -l /run/lock/qemu-server/

# 2. Delete the lock
rm -f /run/lock/qemu-server/lock-<VMid>

# 3. Force shutdown VM
qm shutdown <vmid> --forceStop --skiplock
```

# Proxmox Cheat Sheet

**Author:** David Boyd<br>
**Date:** 2023-06-30

- [VM Issues](#vm-issues)

## VM Issues

### Force Shutdown a VM

1. Find lock file: `ls -l /run/lock/qemu-server/`
2. Delete the lock: `rm -f /run/lock/qemu-server/lock-<VMid>`
3. Force shutdown VM: `qm shutdown <vmid> --forceStop --skiplock`


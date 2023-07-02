# How to Run a Proxmox VM via SPICE on macOS (M1)

**Author:** David Boyd<br>
**Date:** 2023-07-02 

## Steps

### Step 1: Install Virt-Viewer on macOS

``` bash
sudo port install virt-viewer
```

### Step 2: Ensure SPICE Agents are Installed on Guest VM

- `spice-vdagent` is the actual agent 
- `spice-webdavd` is used for file sharing between host & guest machines

1. Install the agents:

```bash
# Debian
sudo apt install spice-vdagent      
sudo apt install spice-webdavd
```

2. Start and enable agents:

``` bash
sudo systemctl start --now spice-vdagent.service
sudo systemctl start --now spice-webdavd.service
```

### Step 3: Configure Guest VM's Hardware via Proxmox

1. Enable SPICE:
  1. VM > `Hardware` > `Display`: `SPICE (qxl)`

2. Add USB Device for passthrough from the client:
  1. VM > `Hardware` > `Add` > `USB Device` > `Spice Port` > `Add`

3. Add an Audio Device:
  1. VM > `Hardware` > `Add` > `Audio Device` > `ich9-intel-hda` > `Add`

### Step 4: Run Guest VM from macOS's SPICE Client

1. Start SPICE console:
  1. Proxmox: VM > `Start`

2. Download SPICE console:
  1. Proxmox: VM > `>_ Console` > `SPICE`

3. macOS Terminal:
  1. `remote-viewer ~/Downloads/<filename>`

:warning: If no display is running, try logging into the VM via the VM's
          `Console` inside of Proxmox; then the display should run via SPICE.

## Additional Resources

- [Proxmox Official Guide - SPICE][pve-spice]

<!-- Reference Links -->

[pve-spice]: (https://pve.proxmox.com/wiki/SPICE)

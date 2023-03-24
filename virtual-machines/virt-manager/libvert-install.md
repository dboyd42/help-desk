# Virt-Manager && LibVert Setup

> Author: David Boyd<br>
> Date: 2023-01-30 <br>
> Revision: 2023-03-23

## Host Machine

### Installation

``` bash
# 1. Install programs
pacman -S libvirt qemu-kvm bridge-utils

# 2. Enable libvert service
systemctl enable --now libvirtd

# 3. Add yourself to the libvert group
sudo usermod -aG libvirt $USER
```

### Network Setup

:pencil2: I originally configured these settings out of order, so I believe you
may first need to add a connection, then enable the connection.

1. Add a connection: `File > Add Connection...`

| Setting                         | Value     |
|---------------------------------|-----------|
| Hypervisor:                     | QEMU/KVM  |
| Connect to remote host over SSH | [Uncheck] |
| Username:                       | <blank>   |
| Hostname:                       | <blank>   |
| Autoconnect:                    | [Check]   |
| Generated URI: qemu:///system   |           |

# 2. Connect
```

``` bash
# Networking
yay -S ebtables dnsmasq

# Manually Start/Destroy Virtual Adapters
sudo virsh net-start default
sudo virsh net-destroy default

# Enable Virtual Adapters upon Start-Up
sudo virsh net-autostart default
# Start Virtual Adapter (if not already started)
sudo virsh net-start default

```

### QEMU

``` bash
# Install QEMU tools
install qemu-full
```

## Guest Machines

> Virt-Manager's default VDI (virtual desktop infra) uses Spice

``` bash
# Install Spice agent
apt install spice-vdagent

# Enable and start agent
systemctl enable --now spice-vdagent

# Fix the virtual display to fit window
xrandr --output Virtual-1 --auto
## OPTIONAL -persistence
echo "xrandr --output Virtual-1 --auto" >> ~/.bashrc
```
# Virt-Manager && LibVirt Setup

> Author: David Boyd<br>
> Date: 2023-01-30 <br>
> Revision: 2023-03-23

## Host Machine

### Installation

``` bash
# 1. Install programs
pacman -S iproute2 qemu-full virt-manager
# Windows Drivers ISO
yay -S virtio-win

# 2. Enable libvert service
systemctl enable --now libvirtd

# 3. Add yourself to the libvert group
sudo usermod -aG libvirt $USER
```

- :warning: [`bridge-utils`][butils] has been replaced with `iproute2`
- :warning: `qemu-kvm` in not in the pacman repo, use `qemu-full`
- :bulb: `libvirt` is included in the `virt-manager` package

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
pacman -S iptables  # If not already installed
pacman -S dnsmasq

# Method #1: Enable Virtual Adapters upon Start-Up
sudo virsh net-autostart default

# Method #2: Manually Start/Destroy Virtual Adapters
# Start Virtual Adapter (if not already started)
sudo virsh net-start default
# Stop Virtual Adapter
sudo virsh net-destroy default
```

## Guest Machines

### Linux Distros

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

### Windows Boxes

#### Issues:

- Can't scale to Window even after changing the Display type and installing
most and pseudo-random drivers.

#### TODO (add instructions)

- Pre-Installation:
  - CPU:
    - XML > clock; && change to "yes"
  - Storage:
    - Change SATA -> VirtIO
  - Add HW:
    - CDROM > drivers.iso
- Post-Install:
  - Drivers:
    - drivers.iso > x64.msi

<!-- Reference Links -->
[butils]: https://wiki.linuxfoundation.org/networking/bridge

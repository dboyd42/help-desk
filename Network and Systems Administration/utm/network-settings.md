# UTM's Network Settings

## Lab Setup

### Attack Machine Settings

Use **2** Network Devices:

    1. Host Only - to connect to other VMs
    2. Shared Network - to connect to the Internet

### Vulnerable Box Settings

Use `Host Only` network mode - to connect ONLY to other VMs.

    - *Note: You will not be able to access host machine from this VM!*

## Network Mode Overview & Settings

### Emulated VLAN

With `Emulated VLAN` mode, every VM gets the **SAME IP ADDRESS!!!**<br>
You'll be able to connect to... well, nothing really.  -\_(*.*)_/-

| Hardware               | Setting                                      |
|------------------------|----------------------------------------------|
| Network Mode           | Emulated VLAN                                |
| Emulated Network Card  | VMWare Paravirtualized Ethernet v3 (vmxnet3) |
| MAC Address            | [Random]                                     |
| Show Advanced Settings | [] [Unchecked]                               |
| Port Forward [New]     | [] [Unassigned]                              |

### Shared Network

With `Shared Network` mode, you'll get assigned an IP from ???, be able to
connect to the host machine, online, and other VMs.

| Hardware               | Setting                                      |
|------------------------|----------------------------------------------|
| Network Mode           | Shared Network                               |
| Emulated Network Card  | VMWare Paravirtualized Ethernet v3 (vmxnet3) |
| MAC Address            | [Random]                                     |
| Show Advanced Settings | [] [Unchecked]                               |

*Note: `Isolate Guest from Host` under `Show Advanced Settings` doesn't appear
to restrict access from VM to host machine.*

### Host Only

With `Host Only` mode, you'll get assigned an IP from the Emulated NIC.<br>
You'll be able to connect to other VMs, but will not be able to go online or
connect to the host machine.

| Hardware               | Setting                                      |
|------------------------|----------------------------------------------|
| Network Mode           | Host Only                                    |
| Emulated Network Card  | VMWare Paravirtualized Ethernet v3 (vmxnet3) |
| MAC Address            | [Random]                                     |
| Show Advanced Settings | [] [Unchecked]                               |

If `Isolate Guest from Host` is [X] [Checked] under `Show Advanced Settings`,
you will NOT be able to connect to another VM!

### Bridged (Advanced)

With `Bridged (Advanced)` mode, you'll get assigned an IP from your SOHO unit,
connect to the host machine, online, and other VMs.

| Hardware               | Setting                                      |
|------------------------|----------------------------------------------|
| Network Mode           | Bridged (Advanced)                           |
| Bridged Itnerface      | en0 (default)                                |
| Emulated Network Card  | VMWare Paravirtualized Ethernet v3 (vmxnet3) |
| MAC Address            | [Random]                                     |
| Show Advanced Settings | [] [Unchecked]                               |

*Note: The VMWare NIC requires VMWare Fusion to be installed, but you can
probably use whatever NIC is available.*

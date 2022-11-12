
# GWAPT (SANS) on UTM (macOS)

## Settings Quicklook

username: student<br>
password: Security542

### Overview

| Setting          | Spec                     |
|------------------|--------------------------|
| Status           | Stopped                  |
| Architecture     | x86_64                   |
| Machine          | Standard PC (Q35 + IC... |
| Size             | 26.61 GB                 |
| Shared Directory | Browse...                |

### System

| Hardware        | Spec                                                       |
|-----------------|------------------------------------------------------------|
| Architecture    | x86_64                                                     |
| System          | Standard PC (Q35 + ICH9, 2009) (alias of pc-q35-7.0) (q35) |
| RAM             | 6144 MB                                                    |
| CPU             | Default                                                    |
| CPU Cores       | 4                                                          |
| Force Multicore | [X] [Checked]                                             |
| JIT Cache       | [Default]                                                  |

### QEMU

| Logging       | Spec        |
|---------------|-------------|
| Debug Logging | [Unchecked] |

| Tweaks                        | Spec           |
|-------------------------------|----------------|
| UEFI Boot                     | [] [Unchecked] |
| RNG Device                    | [X] Checked    |
| Balloon Device                | [] [Unchecked] |
| Use Hypervisor                | [] [Unchecked] |
| Use local time for base clock | [] [Unchecked] |
| Force PS/2 controller         | [] [Unchecked] |
| QEMU Machine Properties       | [Default]      |

### Input

| USB                        | Spec           |
|----------------------------|----------------|
| USB Support                | USB 3.0 (XHCI) |
| Maximum Shared USB Devices | 3              |

### Sharing

| Setting              | Spec                         |
|----------------------|------------------------------|
| Clipboard Sharing    | [X] Enable Clipboard Sharing |
| Directory Share Mode | SPICE WebDAV                 |
| Path                 | [EMPTY]                      |
| Read Only            | [] [Unchecked]               |

### Devices

#### Display

| Hardware                                    | Spec        |
|---------------------------------------------|-------------|
| Emulated Display Card                       | virtio-vga  |
| VGA Device RAM (MB)                         | [EMPTY]     |
| Resize display to window size automatically | [X] Checked |

| Scaling     | Spec             |
|-------------|------------------|
| Upscaling   | Nearest Neighbor |
| Downscaling | Linear           |
| Retina Mode | [] [Unchecked]   |

#### Network

*Bridged Mode will need to be added*

| Hardware               | Spec                           |
|------------------------|--------------------------------|
| Network Mode           | Shared Network                 |
| Emulated Network Card  | Intel Gigabit Ethernet (e1000) |
| MAC Address            | [dynamically assigned]         |
| Show Advanced Settings | [] [Unchecked]                 |

#### Sound

| Hardware            | Spec                                         |
|---------------------|----------------------------------------------|
| Emulated Audio Card | Intel HD Audio Controller (ich6) (intel-hda) |

### Drives

#### IDE Drive

| Setting         | Spec               |
|-----------------|--------------------|
| Removable Drive | [] [Unchecked]     |
| Name            | Virtual Disk.qcow2 |
| Image Type      | Disk Image         |
| Interface       | IDE                |
| Size            | 26.61 GB [Default] |



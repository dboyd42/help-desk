# Kioptrix Level 1 on UTM (macOS)

## Settings Quicklook

### Overview

| Setting          | Spec                                              |
|------------------|---------------------------------------------------|
| Status           | Stopped                                           |
| Architecture     | i386 (x86)                                        |
| Machine          | Standard PC (i440FX + PIIX, 1996) (pc-i440fx-2.2) |
| Size             | 746.8 MB                                          |
| Shared Directory | Browse...                                         |

### System

| Hardware        | Spec                                              |
|-----------------|---------------------------------------------------|
| Architecture    | i386 (x86)                                        |
| System          | Standard PC (i440FX + PIIX, 1996) (pc-i440fx-2.2) |
| RAM             | 512 MB                                            |
| CPU             | Default                                           |
| CPU Cores       | 1                                                 |
| Force Multicore | [] [Unchecked]                                    |
| JIT Cache       | [Default]                                         |

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

| USB         | Spec     |
|-------------|----------|
| USB Support | Disabled |

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

*This'll need to be changed to Bridged Mode*

| Hardware               | Spec                   |
|------------------------|------------------------|
| Network Mode           | Shared Network         |
| Emulated Network Card  | rtl8139                |
| MAC Address            | [dynamically assigned] |
| Show Advanced Settings | [] [Unchecked]         |

#### Sound

*Removed*

### Drives

#### IDE Drive

| Setting         | Spec                  |
|-----------------|-----------------------|
| Removable Drive | [] [Unchecked]        |
| Name            | Kioptix Level 1.qcow2 |
| Image Type      | Disk Image            |
| Interface       | IDE                   |
| Size            | 746.8 MB [Default]    |



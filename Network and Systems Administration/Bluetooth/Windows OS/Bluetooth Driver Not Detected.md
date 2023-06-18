# How to Fix the Bluetooth Enabled Button from Not Showing

**Author:** David Boyd<br>
**Date:** 2021-08-31

| Status   | :heavy_check_mark: Resolved        |
|----------|------------------------------------|
| REF:     | [Dell Community Support][dell-dnd] |
| OS:      | Windows 10                         |
| Mfg:     | Dell                               |
| Product: | XPS 9370                           |

## Issue

Bluetooth stopped working and no button to enable bluetooth is available.

## Solution 1: Update Drivers from Manufacturer

### Step 1: Find and Download Available Drivers

#### 1. Go to Dell's [Drivers and Downloads][dell-dnd] webpage.
#### 2. Download available drivers

- :bulb: This file `XPS_93701.13.1.exe` resolved the issue for me.
- :eyes: The `Killer Wireless AC 1435 Bluetooth Driver<...>.exe` file
  temporarily resolved the issue.

#### 3. Reboot the computer.

- :warning: Be sure to **Restart** the device if *Fast Boot* is turned on, otherwise
   **Shut Down** will *NOT* restart the needed services!

### Step 3: Find and Flash Available UEFI

:cry: If the issue still has not been resolved, then proceed.

1. Repeat [Step 1](#step-1-find-and-download-available-drivers) but search for
   "BIOS" and "UEFI" files.

## Failed Attempts

This section is here to notate time wasted.

### Specific Dell Updates

| Status | :x: FAIL                               |
|-------:|:---------------------------------------|
|   REF: | [Dell Drivers and Downloads][dell-dnd] |

1. Go to: `Category` > `Audio` 
2. Downloads: `Realtek High Definition Audio Driver` 
3. Restart computer

### Services

Attempt to restart relative and associated services:

|  Action | Service                                 | Resolved? |
|--------:|:----------------------------------------|:---------:|
|   Start | `Bluetooth User Support Service_226a4a` |    :x:    |
| Restart | `AtherosSvc`                            |    :x:    |
| Restart | `Bluetooth Support Service`             |    :x:    |
| Restart | `Qualcomm Atheros WLAN Driver Service`  |    :x:    |

### Dell SupportAssist

Attempt manufacture's software to do what it's supposed to do.... :sweat:

1. Open: `Dell SupportAssist`
2. Go to: `Troubleshoot` > `System Devices` 

| Result                   | Resolved? |
|--------------------------|:---------:|
| Bluetooth Device: Passed |    :x:    |

### Reinstall Drivers

Attempt to reinstall Windows recommended drivers via Device Manager.

- :pencil: *Note: This was performed before installing updated drivers from the
manufacturer's website.*

| Status | :x: FAIL |
|--------|----------|

1. Go to: `Control Panel` > `Programs & Features`
2. Uninstall: `Qualcomm QCA61x4a`
3. In `Device Manager` > `Scan for Hardware Changes`
4. In `Device Manager` > `Uninstall & Delete the driver SW for this device`
5. In `Device Manager` > `Scan for Hardware Changes`

#### Rollback Bluetooth 

Attempt to rollback the Qualcomm QCA61x4A Bluetooth driver.

| Status | :x: FAIL |
|--------|----------|

1. Go to: `Device Manager` 
2. Right-click: `Qualcomm QCA61x4A Bluetooth` driver 
3. Go to: `Driver` tab > `Roll Back Driver` > `Yes`
4. Restart computer.

### Windows Troubleshooter

Attempt to have **Windows' Troubleshooter** fix the issues... :sweat:

| Status | :x: FAIL |
|--------|----------|


## Other Resouces

### Bluetooth Driver Not Detected in Windows 10 'Devices & Drivers'

Article claimed that the root cause was because of a Windows update issue and 
specified specific drivers to install from manufacturer's website. The 
specified drivers failed to resolve the issue, but was on the right track.

| Drivers                                                                           | Resolved? |
|-----------------------------------------------------------------------------------|:---------:|
| Killer-Wireless-AC-1535-and-1435-Bluetooth-Driver_VGPP7_WIN_10.0.0.953_A15_02.EXE |    :x:    |

1. Go to: [Dell][dell-dnd]
2. Navigate to: `View all support` > `<enter service tag>` > `<device>` > 
`View system configuration`
	- :bulb: If you don't know your service tag, then download `Dell 
      SupportAssist`
3. Find your bluetooth device (i.e. `Killer 1435 802.11ac 2x2` and `B lutooth`)
	- :bulb: The *typo* is from the website
4. Close > `drivers & downlaods` > `show all` > `downloads`
5. Download and install Wi-Fi card driver (the bluetooth driver should be
   included in the file).
6. Restart computer.

<!-- References -->

[dell-dnd]: https://www.dell.com/support/home/en-us/product-support/product/xps-13-9370-laptop/drivers

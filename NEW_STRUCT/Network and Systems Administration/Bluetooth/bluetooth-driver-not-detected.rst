Bluetooth Stops Working
#######################

Bluetooth Stopped Working --No Button to Enable Bluetooth
*********************************************************
:Reason: Possible update issue --I have Windows 'Preview'
:Fix: Install updates from dell.com
:URL: https://www.dell.com/support/home/en-us/product-support/servicetag/0-ODkzbXo3UWMrbWhXOTMwRTVocEJ3dz090/drivers
:File: XPS_93701.13.1.exe

1. Flash BIOS with latest version

Previously what worked:

2. Update Killer Wireless AC 1435 Bluetooth Driver...exe

Failed Attempts
***************

Dell.com Updates
================
:Status: != fix problem
:URL: https://www.dell.com/support/home/en-us/product-support/servicetag/0-ODkzbXo3UWMrbWhXOTMwRTVocEJ3dz090/drivers

Download and install latest updates for drivers

	-> Audio | Realtek High Definition Audio Driver (Restart Required)

Services
========

1. Restart: AtherosSvc ::> != fix problem
2. Restart: Bluetooth Support Service ::> != fix problem
3. Start: Bluetooth User Support Service_226a4a ::> != fix problem
4. Restart: Qualcomm Atheros WLAN Driver Service ::> != fix problem

Dell SupportAssist
==================

1. Troubleshoot > System Devices > Bluetooth Device: Passed ::> != fix problem

Control Panel -> Programs & Features
====================================
:Status: != fix problem

1. Uninstall Qualcomm QCA61x4a
2. Device Mgr > Scan for Hardware Changes
3. Device Mgr > Uninstall & Delete the driver SW for this device
4. Device Mgr > Scan for Hardware Changes

Device Manager
==============

Bluetooth -> Qualcomm QCA61x4A Bluetooth

1. Uninstall -> Scan for Hardware Changes -> [Reinstall] ::> != fix problem
2. Rollback ::> != fix problem

Start -> ... -> Additional troubleshooters -> Bluetooth
=======================================================
:Status: Does not fix the issue

	- Reinstall device
	- "Reinstall Qualcomm QCA61x4a Bluetooth"

-> Apply this fix

Other Resouces
**************

Bluetooth Driver Not Detected in Windows 10 'Devices & Drivers'
===============================================================
:Reason: Possible update issue
:Fix: Install driver from dell.com
:URL: https://www.dell.com/support/home/en-us/product-support/servicetag/0-ODkzbXo3UWMrbWhXOTMwRTVocEJ3dz090/drivers
:File: Killer-Wireless-AC-1535-and-1435-Bluetooth-Driver_VGPP7_WIN_10.0.0.953_A15_02.EXE

1. dell.com > view all support > <enter service tag> > <device> > view system configuration
	- if you don't know your service tag, THEN download 'Dell SupportAssist'

2. find your bluetooth device (I.e.) Killer 1435 802.11ac 2x2 and B lutooth)
	- note: the typo is from the website

3. <close> > drivers & downlaods > show all <n> downloads
4. download and install wifi card driver.
5. resstart after installation, and viola!  problem solved!


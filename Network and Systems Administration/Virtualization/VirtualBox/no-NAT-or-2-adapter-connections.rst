No Internet Connection with 2 Adapters (NAT, Host-Only)
#######################################################
:STATUS: Resolved

NAT Issues
==========
:SOLUTION: Release & Renew IP address
:SYNTAX: dchlient [option] [interface]

.. code-block:: Bash

	# release current ip address
	dhclient -r eth0

	# renew ip address
	dhclient eth0

Quick Fix
=========
:Display: VMSVGA, disable 3D acceleration
:Networking: Disable Adapter 1 -> save; Enable Adapter 1
:VM>Bash: service smbd start; dhclient eth1

Resources
=========
:VBox: https://www.vituralbox.org/manual
:docs.MS: https://docs.microsoft.com/en-us/windows-hardware/drivers/devtest/bcdedit--set
:man-pages: smbd

Sumamary
--------

Imported Jason Dion's Kali Linux from his Udemy's Pentest+ course.

	- display issues: black-screen-o-death
	- boot hang on: "started update UTMP about System Runlevel Changes..."
	- Internet connectivity
	- Resolved dhcp client <> created WSL issue

Display
=======
:Issues: black-screen-o-death
:Reason: Misconfigured display settings
:Source: https://www.virtualbox.org/manual/ch03.html#settings-display

Resolution
----------

Set the display to be VMSVGA.

VMSVGA
	Use this graphics controller to emulate a VMware SVGA graphics device.
	This is the default graphics controller for Linux guests.

Boot Hang On
============
:Issues: "started update UTMP about System Runlevel Changes..."
:Reason: Most likely issues between Hyper-V and VBox trying to access services
:Reason2: VBox needs video resources from host but Hyper-V says no
:Source: https://forums.kali.org/showthread.php?31257-No-Boot-system-hang-on-quot-Started-Update-UTMP-about-System-Runlevel-Changes-quot

Resolution
----------

Disable the 3D Accelerator

No Internet
===========
:Issue: No internet connectivity, but can ping other VMs
:Reason: NAT adapter not being properly leased an IPv4 addr from VBox Engine
:Source: man smbd, man dhclient

Resolution
----------
:NOTE: On reboot, smbd will re-disable (but we'll no longer need it post this)

Login to the Kali VM and open terminal as root.

.. code-block:: Bash

	service smbd start
	dhclient eth1

man smbd
	smbd is the server daemon that provides filesharing and printing services
	to Windows clients using SMB (or CIFS) protocol.
	:NOTE: the vendor's preset smbd is disabled

man dhclient
	dhclient provides a means for configuring one or more network interfaces
	using the DHCP, BOOTP protocol, or if these protocols fail, by statically
	assigning an address.
	:Operation: The DHCP protocol allows a host to contact a central server (in
	this case, the VirturalBox Engine) which maintains a list of IP addresses
	which may be assigned on one or more subnets.  A DHCP client may request an
	address from this pool, and then use it on a temporary basis for
	communication on a network.  The DHCP protocol also provides a mechanism
	whereby a client can learn important details about the network to which it
	is attached, such as the location of a default router, the location of a
	name server, and so on.

Resolved dhcp client <> created WSL issue
=========================================
:Issue: No Internet
:Reason: VBox and Hyper-V don't work well together.
:Source: https://docs.microsoft.com/en-us/windows-hardware/drivers/devtest/bcdedit--set
:ERRORS: causes WSL to no longer run

NO Resolution
-------------

**Disable Hyper-V**

This is the quick and dirty way to resolve the VBox NAT connectivity issue.
This ultimately gets rid of Hyper-V, but in doing so, you lose all of the WSL.

.. code-block:: Command.exe

	" Disable Hyper-V
	bcdedit /set hypervisorlaunchtype off

	" Enable Hyper-V
	bcdedit /set hypervisorlaunchtype auto


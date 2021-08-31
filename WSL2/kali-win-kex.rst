Kali-Win-Kex
############
:URL: https://www.kali.org/docs/wsl/win-kex/
:Summary: Kali20.3@WSL GUI
:Additional Doc: Sound, Public Netw --FW, MultiScreen Support

Quick Start
===========

.. code-block:: Bash

	# Start kex
	kex

	# Window kex (once inside kex)
	<F8>[checkbox]FullScreen

	# Stop kex
	kex stop

	# show running kex services
	kex status

######
Manual
######

Kex Modes
=========
:Modes: Window, Seamless

Window
------
:Summary: Window mode helps keeping the Windows and Kali environments visually
apart.
:URL: https://www.kali.org/docs/wsl/win-kex-win/

.. code-block:: Bash

	# Start in Window mode
	kex
	kex --win	# long version
	### =============
	### **IMPORTANT**
	### =============
	# To properly configure pop-up KeX window
	<F8> Options ... display




Seamless
--------
:URL: https://www.kali.org/docs/wsl/win-kex-sl/
:Summary:  Launches Kali panel on the screen top of the Windows desktop.

**Description**

Seamless mode removes the visual segregation b/t linux & win apps
Offers platform to run a penetration test and copy results into Win app
for final report.

.. code-block:: Bash

	# Start Win-KeX as normal user in seamless mode
	kex --sl

Change Window Size
==================

FullScreen vs Window
--------------------
:Note: dunno if that's an 'o' or a '0'... probably a 'zero'

sudo sed -ie "s/FullScreen=1/FullScreen=o" /usr/bin/kex


Logged Out
==========
:Issue: Logged out resulting in black screen
:Status: Resolved
:Summary: <C-M-del>; kex -stop; kex

What happened what you started the VNCServer and the TigerVNC client.
When you close the client, the server is still running.

Installation
============
:Requirements: WSL2

sudo apt update -y &&
sudo apt upgrade -y &&
sudo apt install kali-win-kex -y

######
Issues
######

TigerVNC viewer unable to connect to socket: Conncetion refused (10061)
=======================================================================
:Status: Resolved
:Reasons: Session not properly closed out of
:Quick Fix: Restart WSL service on Windows (LxssManager)
:Remediation: Kex>Terminal:# kex stop

Probable Causes
---------------
:Tmux: Prevous session still running in tmux
:User: Previous session running as either $USER or root

Note: Kex can be ran under multiple sessions simulataneous under different
linux users, such as $USER, root, or anotheruser.

Resolution
----------

1.	Stop and Kill all Kex sessions

.. code-block:: Bash

	# As regular user
	kex stop
	kex kill
	# As root
	sudo kex stop
	sudo kex kill

2.	Restart WSL

.. code-block:: Powershell

	# Run as admin
	Get-Service LxssManager | Restart-Service

Troubleshooting
===============
:URL: https://ostechnix.com/fix-sub-process-usr-bin-dpkg-returned-an-error-code-1-in-ubuntu/
:Status:
:Summary: Need to complete WSL installation steps before d/l add'l apts

**ERROR1:**

Errors were encountered while processing:
 /var/cache/apt/archives/kali-win-kex_2.0_amd64.deb
E: Sub-process /usr/bin/dpkg returned an error code (1)

.. code-block:: Bash

	# remove the cached package
	sudo rm /var/cache/apt/archives/kali-wen-kex_2.0_amd64.deb

	# Clean the package cache folder:
	sudo apt-get clean
	sudo apt-get autoremove

	# Update the source lists:
	sudo apt-get update

	# Upgrade your system:
	sudo apt-get upgrade

	# Get the fresh package from official repositories and reinstall it
	sudo apt-get install eog

**ERROR2:**

Errors were encountered while processing:
/tmp/apt-dpkg-install-4gnUNC/341-kali-win-kex_2.0_amd64.deb
E: Sub-process /usr/bin/dpkg returned an error code (1)

.. code-block:: Bash

	sudo apt dist-upgrade -y
	sudo apt autoremove && sudo apt clean


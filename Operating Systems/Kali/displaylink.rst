Triple Monitors w/ DisplayLink Driver
#####################################
:Author: David Boyd
:Date: 2021-03-15

Steps
*****

1. Uninstall previous versions of DisplayLink
=============================================

`sudo displaylink-installer uninstall`

2. D/l displaylink-debian.sh
============================
:URL: https://github.com/AdnanHodzic/displaylink-debian

.. code-block:: Bash

        sudo apt-get install git

        git clone https://github.com/AdnanHodzic/displaylink-debian.git

        cd displaylink-debian/ && sudo ./displaylink-debian.sh

3. Modify displaylink-debian.sh
===============================

The script needs a minor modification for Kali-rolling.

Open the shell script named "displaylink-debian.sh" with any text editor.

Check line 173 and replace "Debian" with "Kali" elif [ "$lsb" == "Kali" ];

Check line 175 and replace "sid" with "kali-rolling" [ $codename == "kali-rolling" ];

Save and run script as superuser // DISCONNECT YOUR HUBS AND MONITORS

A reboot may need to be required.

4. Follow the Post-Installation Guide
=====================================
:URL: https://github.com/AdnanHodzic/displaylink-debian/blob/master/post-install-guide.md

Connect your hub and/or monitors.

.. code-block:: Bash

   # Display detection
   xrandr --listproviders
   
   # Connect all the DisplayLink providers to the main power
   for i in {1..4}; do xrandr --setprovideroutputsource $i 0; done

**Your monitor should now be working!!!**

[BUG-01] No persistence in connecting providers after reboot.


5. Persistence
==============

.. code-block:: Bash

    # Check the status
    service displaylink-driver status

    # Enable your displaylink-driver service to run at startup
    sudo systemctl enable displaylink-driver.service

    # Other useful commands
    sudo service displaylink-driver restart/start/stop

[BUG-01] No persistence in connecting providers after reboot.

Unresolved Issues
*****************

[BUG-01] No persistence in connecting providers after reboot.


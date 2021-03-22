printers
########
:Author: David Boyd
:Date: 2021-03-21

Install Through:
****************
:URL: https://support.brother.com/g/b/downloadlist.aspx?c=us&lang=en&prod=dcpl2540dw_us_as&os=128

Then follow instructions.  Say yes for URI location.  Use DNS network then
input IP address.

Error still lies in vim--not printing.

	- :hardcopy says sent to printer but doesn't print.  Idk why...

Notable Errors
**************

[ERROR-01] Add <userName> to lpadmin
====================================
:Status: [Resolved]

Description
-----------

Can't access admin Web Interface page.


Solution
--------

	`sudo useradd <userName> lpadmin`

[ERROR-02] Can't Print Test Page
================================
:Status: [Resolved]

Description
-----------

CUPS adds printer location through DNS name, but doesn't use local DNS to
locate the printer after installing... wtf.

Solution
--------

Reconfigure DNS location to static IP address.

.. code-block:: Bash

	# Stop CUPS service
	sudo systemctl stop cups

	# Open to edit printer configuration file
	sudo vim /etc/cups/printers.conf

	# Replace <dnsName> with the printer's <IPAddr>
	DeviceURI lpd://<IPAddr>/BINARY_P1

	# Restart CUPS service
	sudo systemctl start cups

[ERROR-03] Vim :hardcopy not printing
=====================================
:Status: NOT resolved

Description
-----------

Error: E365 Failed to print PostScript file
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
:Resolved: https://support.brother.com/g/b/downloadlist.aspx?c=us&lang=en&prod=dcpl2540dw_us_as&os=128

Solution
--------

Set default printer.
Check default printer: `lpr file.ext`

OPTION 1
^^^^^^^^
Gnome GUI > Settings > Printer > Options > [check] Set as Default printer

OPTION 2
^^^^^^^^
:Note: NOT Tested

**Below allows you to print from command line:**

`lp -d HP_LaserJet_P1005 main.c`

or

`lpr -P HP_LaserJet_P1005 main.c`

Replace the printername by your printer name

**Below sets the default printer (not sure if it's persistent)**

`lpoptions -d HP_LaserJet_P1005`

and now you can use lpr (or lp) without additional parameters.

`lpr main.c`

Install and run CUPS
********************

.. code-block:: Bash

	# Install CUPS, CUPS-Client, driver-db
	sudo apt install cups cups-client "foomatic-db"

	# Add user to lpadmin for printing rights
	sudo adduser root lpadmin
	sudo adduser <userName> lpadmin			# ERROR-01:RESOLVED
	# Check if user is added to lpadmin group
	groups <userName>

	# Restart CUPS
	sudo service cups restart
	# If 'service command not found error':
	PATH=/usr/sbin:$PATH

	# Enable CUPS
	sudo systemctl enable cups

	# Start the CUPS service
	sudo systemctl start cups

Configure Printer
*****************
:UI: Web Interface

1. http://127.0.0.1:631/ > Administration > Printers > Add Printer

2. Discovered Network Printers > <printerName> > Continue

3. Configure TCP/IP address				# ERROR-02:RESOLVED

.. code-block:: Bash

	# Stop CUPS service
	sudo systemctl stop cups

	# Open to edit printer configuration file
	sudo vim /etc/cups/printers.conf

	# Replace <dnsName> with the printer's <IPAddr>
	DeviceURI lpd://<IPAddr>/BINARY_P1

	# Restart CUPS service
	sudo systemctl start cups

4. Print Test Page from Web Interface


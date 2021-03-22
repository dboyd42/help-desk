printers
########
:Author: David Boyd
:Date: 2021-03-21

Notable Errors
**************

1. [Resolved] ERROR-01: Add <userName> to lpadmin

2. [Resolved] ERROR-02: CUPS adds printer location through DNS name, but
doesn't use local DNS to print... wtf.

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


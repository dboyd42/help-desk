bluetooth-support
#################
:Author: David Boyd
:Date: 2022-01-23

The bluetooth service on the Raspberry Pi 400 needs a uart helper service
before it works. To enable and start the bluetooth service run the following
commands:

.. code-block:: bash

	sudo systemctl enable --now hciuart.service
	sudo systemctl enable --now bluetooth.service


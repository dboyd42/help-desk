Github Troubleshooting
**********************

Github SSH via public WIFI, port 22 blocked
===========================================

.. code-block:: bash

	# Open your SSH config file
	vim ~/.ssh/config

	# Add GitHub host to HTTPS
	Host github.com
	Hostname ssh.github.com
	Port 443

	# Add BitBucket host to HTTPS
	Host bitbucket.org
	Hostname altssh.bitbucket.org
	Port 443


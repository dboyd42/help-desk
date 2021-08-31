Grub Rescue
***********
:Reference URL: Grub_Rescue_
:Status: Sometimes works, sometimes doesn't.

This article references a multi-OS troubleshooting with a grub rescue shell.

.. code-block:: Grub-Rescue

	# Find the partition with the boot files
	ls
	ls (hd0,8)
	ls (hd0,8)/boot/grub
	#...etc, etc, etc

	# While ( output != ext* )
	grub-rescue> ls (hd0,#)

	# Once you find the partition with boot files,
	# Set Grub to boot that partition
	grub-rescue> set prefix=(hd0,#)/boot/grub
	grub-rescue> set root=(hd0,#)
	grub-rescue> insmod normal
	grub-rescue> normal					// should boot to GUI grub/bootloader

Once you're able to boot into Linux, update your Grub.

	.. code-block:: Bash

	# In Linux terminal
	sudo update-grub
	sudo grub-install /dev/sda

.. Hyperlinks

.. _Grub_Rescue: https://www.linux.com/training-tutorials/how-rescue-non-booting-grub-2-linux/


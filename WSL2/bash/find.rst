find
####
:Author: David Boyd
:Date: 2020-11-10

[ISSUE] Recursively Searches C:\ Drive
**************************************
:Status: Solved
:Reason: The C drive is in the root '\' directory

Fix #1
=======

Use "-mount" (don't descend directories on other filesystems)

Solution
--------

.. code-block:: Bash

	find / -mount -perm 4000

Fix #2
======

Use "-prune" in conjuction with "-print"

	- "path" defines the next argument as a directory
	- "prune" tells the prgm what event/action to perform on the prev->arg
	- "print" tells the prgm to run the output to std0
		- also can use "print0" to be more precise

.. code-block:: Bash

	find / -path /mnt -prune -perm 4000 -print




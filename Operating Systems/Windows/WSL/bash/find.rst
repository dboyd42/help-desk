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

Use "-prune" in conjuction with "-o" && "-print"

	- "path" defines the next argument as a directory
	- "prune" tells the prgm what event/action to perform on the prev->arg
	- "print" tells the prgm to run the output to std0
		- also can use "print0" to be more precise

.. code-block:: Bash

	find / -path /mnt -prune -perm 4000 -o -print

Reference
=========
:URL: https://www.liamdelahunty.com/tips/linux_find_prune_directory.php

Linux Find Exclude Directory
find . -path './media' -prune -o -print

Find all files in this directory (.)
-prune (ignore) the proceding path of
'./media'
Then if no match print (prune or print)
Linux Find Modified with certain time period with excluded directory
find . -path './media' -prune -o -mtime -30 -print

Find all files in this directory (.)
-prune (ignore) the proceding path of
'./media'
Modified within the last 30 days
print the results.

Linux Find Exclude Multiple Directories
=======================================
:URL: https://www.liamdelahunty.com/tips/linux_find_exclude_multiple_directories.php

find . -type d \( -name media -o -name images -o -name backups \) -prune -o -print

find . - Find all files in this directory (.)

-type d - directory or folder

-prune - ignore the proceding path of ...

\( -name media -o -name images -o -name backups \) - The -o simply means OR

-o -print - Then if no match print the results, (prune the directories and print the remaining results)

As always in Linux there are many ways to achieve the same result, and the patient may prefer to build up the find command using the path attribute. Please note that you may need to specify the path with a prefix of "./" and no trailing slash.
find . -path './media' -prune -o -path './images' -prune -o -path './backups' -prune -o -print

An important difference here is that the first command will prune ANY directory in the path that matches the name, such as './media' and './public/media', where as the second format will only prune the explict path './media'.

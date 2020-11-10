find
####
:Author: David Boyd
:Date: 2020-11-10

[ISSUE] Recursively Searches C:\ Drive
**************************************
:Status: Solved
:Reason: The C drive is in the root '\' directory
:Fix: "modularize" the 'find' command with '-type'

Solution:

.. code-block:: Bash

	find / -path "/mnt" -prune -type f -iname "*whatever*"


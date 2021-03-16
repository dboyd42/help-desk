find
####
:Author: David Boyd
:Date: 2020-11-10

[ISSUE] Recursively Searches C:\ Drive
**************************************
:Status: Solved
:Reason: The C drive is in the root '\' directory
:Fix: -mount (don't descend directories on other filesystems)

Solution:

.. code-block:: Bash

	find / -iname "*whatever*" -mount


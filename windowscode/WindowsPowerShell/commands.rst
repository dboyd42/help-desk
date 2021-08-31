Powershell Commands
###################

Warnings
========

**Remove-Item** does not work when working with cloud files, aka, OneDrive.

Code
====

.. code-block :: Powershell

	# Create a series of dirs 'section{01..18}
	for ($i=0;$i -lt 19;$i++) {
		mkdir section$i
	}
	for ($i=0;$i -lt 10;$i++) {
		mv section0$i
	}



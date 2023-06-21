Outlook: Importing Contacts
###########################
:Author: David Boyd
:Date: 2020-12-16

Normal Process
**************

Gmail
=====

1. Gmail > [9-dots Grid] > Contacts
2. (top-left) [3 Bars] Menu > Export > Export as Outlook CSV > Export

Outlook
=======

1. File > Open & Export > Import/Export
2. Import from another program or file > Next
3. Comma Separated Value -> Next
4a. Browse <filename>
4b. Options > Replace duplicates with items imported > Next
5. Select destination folder: <name>@outlook.com/Contacts
6. Import "my outlook contacts.CSV" into folder > Finish

Errors
******
:Status: Resolved

Translation Error Message
=========================
:Status: Resolved
:Quick Fix: Open contacts.csv, save file, close file; reimport file in Outlook.
:Reason: DOS vs Linux line endings.

.. code-block::

	"A file error has occurred in the CSV translator .......
	Outlook was unable to retrieve the data ........
	Verify that you have the correct file ... permissions .... not open .....

Reason
------

Text files created on DOS/Windows machines have different line endings than
files created on Unix/Linux. DOS uses carriage return and line feed ("\r\n") as
a line ending, which Unix uses just line feed ("\n"). You need to be careful
about transferring files between Windows machines and Unix machines to make
sure the line endings are translated properly.

Solution
--------

1. Open the file in Excel (or any program that can open csv files).
2. Save (or Save As) the file; then close the file.
3. Reimport the file using the `Normal Process`_.


printers-vim
############
:Author: David Boyd
:Date: 2021-03-21

Issue
******

Vim is not printing using the :hardcopy method in Kali.

Workaround
**********

Convert to black and white html and print through Firefox.

In Vim
======

.. code-block: Vim

	# Colorscheme and Syntax translates to html colors --bad for B&W printers
	:syntax off
	:colorscheme default
	# Set the LineNumber colors
	:highlight LineNr ctermfg=black
	# [OPTIONAL] Set the background of the linenumbers --not recommended
	:highlight LineNr ctermbg=<color>

	# Convert to HTML and save files
	:bufdo TOhtml
	:bufdo w

	# Open files in Firefox
	:!Firefox *.html

In Firefox
==========

Print each tab.


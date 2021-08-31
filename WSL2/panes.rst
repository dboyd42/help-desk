WSL Panes
#########

Create
======

alt+shift+plus
alt+shift+minus

.. code-block :: Windows Terminal

	{ "command": { "action": "splitPane", "split": "vertical" }, "keys": "alt+shift+plus" },
	{ "command": { "action": "splitPane", "split": "horizontal" }, "keys": "alt+shift+-" },
	{ "command": { "action": "splitPane", "split": "auto" }, "keys": "alt+shift+|" }

Switching
=========

.. code-block :: Windows Terminal

	{ "command": { "action": "moveFocus", "direction": "down" }, "keys": "alt+down" },
	{ "command": { "action": "moveFocus", "direction": "left" }, "keys": "alt+left" },
	{ "command": { "action": "moveFocus", "direction": "right" }, "keys": "alt+right" },
	{ "command": { "action": "moveFocus", "direction": "up" }, "keys": "alt+up" }

Resizing
========

alt+shift

.. code-block :: Windows Terminal

	{ "command": { "action": "resizePane", "direction": "down" }, "keys": "alt+shift+down" },
	{ "command": { "action": "resizePane", "direction": "left" }, "keys": "alt+shift+left" },
	{ "command": { "action": "resizePane", "direction": "right" }, "keys": "alt+shift+right" },
	{ "command": { "action": "resizePane", "direction": "up" }, "keys": "alt+shift+up" }

Closing
=======

ctrl+shift+w

.. code-block :: Windows Terminal

	{ "command": "closePane", "keys": "ctrl+shift+w" }


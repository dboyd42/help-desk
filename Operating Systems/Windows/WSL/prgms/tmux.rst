tmux
####
:Author: David Boyd
:Date: 2020-11-10

[ISSUE] Copying & Pasting
=========================
:Status: Solved
:Issue: Copying and Pasting between sessions and system clipboard
:Reference: https://mitchellt.com/2020/04/01/copying-from-tmux-wsl-windows-terminal.html

Althought Windows Terminal offers <C-S-c> and <C-S-v> methods, they don't
always work from TMUX --especially the copying from TMUX to Windows system
clipboard.  Read the reference site for explanation on the code.  Otherwise,
copy and paste the following into your .tmux.conf file:

.. code-block:: Tmux

	set -g mouse on
	if-shell -b 'test -n "$WSLENV"' 'bind-key -T copy-mode-vi Enter send-keys -X copy-pipe-and-cancel clip.exe'
	if-shell -b 'test -n "$WSLENV"' 'bind-key -T copy-mode-vi MouseDragEnd1Pane send-keys -X copy-pipe-and-cancel clip.exe'


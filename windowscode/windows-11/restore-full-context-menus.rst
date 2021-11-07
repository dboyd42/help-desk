Restore Full Context Menus
##########################
:Date: 2021-11-07
:Reference: https://www.pcgamer.com/windows-11-context-menu-fix-right-click/

Purpose
=======

Restores the right-click context menu to Windows 10 with more options.

:image: ./pics/full-context-menu.png

Procedure
=========

1. Open Registry Editor
2. Navigate to HKEY_CURRENT_USER\Software\Classes\CLSID
3. Right-click > New > Key and paste this in the name: {86ca1aa0-34aa-4e8b-a509-50c905bae2a2}
4. With the new key you just created highlighted, again right-click > New > Key, and paste in this name: InprocServer32
5. Double-click the (Default) registry entry and then hit Enter without typing anything to set its value to blank. Before making this change, you'll see under the Data column that it says (value not set), but once you hit Enter it'll show nothing.

	5b. If Data doesn't show anything, manually type: (value not set)

6. Close Registry Editor. To see your new (classic) context menu, either restart your computer or open Task Manager, scroll down to the Windows Explorer process, and right-click > End task. Then File > Run new task and type explorer.exe to restart the Windows explorer process. And there you go: context menus changed!

	6b. If explorer doesn't properly restart, then reboot computer.


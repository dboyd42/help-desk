Windows COMMANDS
################

runAs admin | privilege escalation
==================================
:Summary: Open PowerShell as Administrator from running PowerShell as User
:Example: Start-Process Powershell -Verb runAs

certUtil.exe
============
:URL: https://www.shellhacks.com/windows-md5-sha256-checksum-built-in-utility/
:Checksum a file
:Syntax: certutil -hashfile <inFile> <encryption>
:Example: certutil -hashfile tmp.txt sha256
:Example2: certutil -hashfile tmp.txt sha256 | findstr /v "hash"
:Explanation: findstr /v -> print lines that DO NOT match #inVert

chkdsk
======
:Desc: chkdsk fix bad sectors
:Example: chkdsk z: /f

convert
=======
:Desc: Converts fs whilst keeping data
:Syntax: convert <drvie>:/<fileSystem>:ntfs
:Example: convert z:/fs:ntfs

echo
====
:Desc: 'echo' command
:Desc2: 'touch' files
:Man: help echo
:Alias: write
:Parameters: '>' (redirection)
:Example1: echo > temp01.txt <Enter><Enter>	// Creates new/empty file
:Example2: echo > temp02.txt <Enter><input><Enter>  // " file w/ text/line
:Example3: echo "random text" > temp02.txt 	// " file w/ text/line

gci | Get-ChildItem
===================
:Desc: 'find' command
:Alias: gci, ls, dir
:Man: help gci
:Parameters: -Recurse -Filter
:Example1: gci -r -fi *.jar
:Example2: gci -r -fi *vim*
:Regex: GOTO URL
:URL: https://jessitron.com/2020/04/23/powershell-equivalent-of-find/

fsutil (File System Utility)
============================
:Descr: 'touch' command (see: echo)
:Requirements: Admin privileges
:Man: fsutil /h
:Parameters: fsutil file createnew filename requiredSize
:Example: fsutil file createnew test1.tmp 0

Invoke-Item <dir>
=================
:Descr: Open File Explorer (2 methods)
:Example1: ii .
:Example2: Invoke-Item .

rmdir | Remove-Item -Recurse -Force <dir>
=========================================
:Desc: rmdir /s'ubtree' = recursively
:Note: command.exe != powershell.exe
:Example: rmdir /s <foldername>

Set-ExecutionPolicy
===================
:Summary: Dis/allow scripts to be ran
:Example: Set-ExecutionPolicy Restricted (Default)

Execution Policies (4)
----------------------

Restricted
	stops any script from running

RemoteSigned (Recommended)
	allows scripts created on the device, but scripts created on another computer won't run unless they include a trusted digital signature.

AllSigned
	all the scripts will run, but only if a trusted publisher has sign them.

Unrestricted
	runs any script without any restrictions.


type
====
:Descr: 'cat' command
:Descr2: display files, concatenate files
:Example: type f1.txt f2.txt > result.txt // concatenate files1,2 > result.txt
:Example2: type result.txt		  // cat result.txt

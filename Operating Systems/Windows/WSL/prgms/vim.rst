Vim
###

Copy to System Clipboard
************************
:Status: Resolved

Issue
=====

Can't copy from inside vim to system clipboard

Quick Fix
=========

Inside Vim, turn off mouse visual selection

`:set mouse -=a`

Location
========

Windows Terminal > Kali-linux > Vim

Reason
======

Windows Terminal copy paste feature is overwritten by Vim's visual `set
mouse=a` settings.


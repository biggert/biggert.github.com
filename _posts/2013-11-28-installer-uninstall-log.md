---
layout: post
title: "Installer uninstall log"
description: ""
category: ""
tags: [Installshield]
---
{% include JB/setup %}

http://community.flexerasoftware.com/showthread.php?t=187683

\*\*\* This method can be used when you have not the possibility to generate an install log via the commandline, as we normally do. \*\*\*


Open the registry with Regedit.exe and create the following path and keys:
HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Installer
Reg_SZ: Logging
Value: voicewarmupx
The letters in the value field can be in any order. Each letter turns on a different logging mode. Each letter's actual function is as follows for MSI version 1.1:
v - Verbose output
o - Out-of-disk-space messages
i - Status messages
c - Initial UI parameters
e - All error messages
w - Non-fatal warnings
a - Start up of actions
r - Action-specific records
m - Out-of-memory or fatal exit information
u - User requests
p - Terminal properties
+ - Append to existing file
! - Flush each line to the log
x - Extra debugging information. The "x" flag is available only on Windows Server 2003 and later operating systems, and on the MSI redistributable version 3.0, and on later versions of the MSI redistributable.

"\*" - Wildcard, log all information except for the v and the x option. To include the v and the x option, specify "/l\*vx".

Note This should be used only for troubleshooting purposes and should not be left on because it will have adverse effects on system performance and disk space. Each time you use the Add/Remove Programs tool in Control Panel, a new Msi\*.log file is created.
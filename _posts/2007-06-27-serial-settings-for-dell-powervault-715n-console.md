---
id: 97
title: Serial Settings for Dell Powervault 715n Console
date: 2007-06-27T10:23:59+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/06/27/serial-settings-for-dell-powervault-715n-console/
permalink: /2007/06/27/serial-settings-for-dell-powervault-715n-console/
categories:
  - Troubleshooting
  - Windows
---
If your Powervault NAS loses network connectivity or won&#8217;t boot into the OS, you&#8217;ll need to physically access it via the console port at the back. From there you can edit and upgrade the BIOS, run a recovery boot (boots the OS from another drive) and perform hardware diagnostics.

Here&#8217;s the settings you&#8217;ll need for HyperTerminal:

Bits per second: 115200  
Data bits: 8  
Parity: None  
Stop bits: 1  
Flow Control: Xon / Xoff

[![Serial Settings for Dell Powervault 715n Console](http://www.kabri.uk/wp-content/uploads/2007/06/powervault-715n-serial-port-settings.thumbnail.png)](http://www.kabri.uk/wp-content/uploads/2007/06/powervault-715n-serial-port-settings.png "Serial Settings for Dell Powervault 715n Console")
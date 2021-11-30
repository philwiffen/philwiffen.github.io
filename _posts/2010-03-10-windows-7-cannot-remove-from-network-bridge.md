---
id: 606
title: 'Windows 7 &#8211; Cannot remove from network bridge'
date: 2010-03-10T11:04:24+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2010/03/10/windows-7-cannot-remove-from-network-bridge/
permalink: /2010/03/10/windows-7-cannot-remove-from-network-bridge/
categories:
  - Miscellaneous
---
Just had a very weird issue on Windows 7, where I was unable to remove a network connection from a network bridge I&#8217;d setup.

The normal way of doing it is described on the [Microsoft website](http://windows.microsoft.com/en-US/windows-vista/Remove-a-connection-from-a-network-bridge). However, right clicking on the network connection had the &#8220;Remove from bridge&#8221; option greyed out, meaning I couldn&#8217;t remove it. I was also unable to delete the Bridge miniport itself from within Manage network connections.

To fix this, we can brute force the removal:

  1. Open up Device Manager
  2. Expand &#8220;Network Connections&#8221;
  3. Right click on the MAC bridge miniport
  4. Uninstall it

As your bridge has been uninstalled, your connections should now be removed from the network bridge 🙂
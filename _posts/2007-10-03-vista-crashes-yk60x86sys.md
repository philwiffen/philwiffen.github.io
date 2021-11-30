---
id: 153
title: 'Vista Crashes: yk60x86.sys'
date: 2007-10-03T12:59:14+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/10/03/vista-crashes-yk60x86sys/
permalink: /2007/10/03/vista-crashes-yk60x86sys/
ratings_score:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
ratings_users:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
ratings_average:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
categories:
  - Device Drivers
  - Troubleshooting
  - Windows
tags:
  - marvell yukon
  - sony vaio
  - vista
  - yk60x86.sys
---
### Problem

Vista Crashes (Blue Screens) with an error message mentioning yk60x86.sys.

### Solution

We&#8217;ve got a bunch of Sony Vaio VGN-SZ5MN laptops at work and a lot of them are blue screening (<acronym title="Blue Screen of Death">BSOD</acronym>) as soon as you plug in the Ethernet cable. If that&#8217;s not enough of a clue (hehe), the problem is the Marvell Yukon Ethernet Controller driver. 

**To fix the problem, download the updated driver** from the [Marvell Driver page](http://www.marvell.com/drivers/).

Or try this direct link to the [Driver Installer for Windows 2000/XP/Vista](http://www.marvell.com/drivers/driverDisplay.do?dId=175&pId=39)
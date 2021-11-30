---
id: 63
title: 'Asus System Recovery Error: &#8220;No partition selected&#8221;'
date: 2007-04-17T20:18:13+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/04/17/asus-system-recovery-error-no-partition-selected/
permalink: /2007/04/17/asus-system-recovery-error-no-partition-selected/
categories:
  - Troubleshooting
  - Windows
---
This is a guide for anyone who receives the &#8220;No partition selected&#8221; error when trying to run a system recovery on their Asus Laptop.  
<!--more-->

### The symptoms

  1. When you try to recover your OS you get the error: &#8220;No partition selected&#8221;
  2. You converted your partitions from FAT32 to NTFS (via the little short-cut Asus kindly put on your Desktop)

### The cause

The software used to recover your OS only recognises FAT32 partitions. How wonderful of you PowerQuest. It&#8217;s no wonder I use Acronis for everything now&#8230;

### The solution

You need to format your target partition to FAT32. There&#8217;s a nice [Open-Source boot-cd](http://gparted.sourceforge.net/livecd.php) that can do that. Or you can use Acronis Disk Director or something similar.

Did this help you at all? Any questions? Feel free to leave me a comment below 🙂
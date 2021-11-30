---
id: 688
title: MDT 2010 and WinPE 3.1 Reboot issue
date: 2011-03-24T16:21:42+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=688
permalink: /2011/03/24/mdt-2010-and-winpe-3-1-reboot-issue/
categories:
  - Desktop Deployment
---
If you&#8217;ve recently updated your WinPE from 3.0 to 3.1, you may notice an annoying reboot issue.

It looks like this: after you&#8217;ve rebuilt the .wim image, and booted from it via WDS (Windows Deployment Services), WinPE boots up and shows the Solution Accelerator background, but after a short period of time, it reboots the PC without having done anything.

This happens if:

  1. You&#8217;ve got Microsoft Deployment Toolkit (MDT) 2010 Update 1.
  2. You&#8217;ve upgraded WinPE from 3.0 to 3.1, using the supplemental update ISO.

To fix this problem, Michael Niehaus has [some instructions to follow](http://blogs.technet.com/b/mniehaus/archive/2011/03/12/issue-with-mdt-2010-update-1-and-windows-aik-for-windows-7-sp1-supplement.aspx).

Fortunately we don&#8217;t use WinRE, so we can use the workaround and still make use of WinPE 3.1. Had we needed WinRE, I would have restored the backup of the WinPE 3.0 files I&#8217;d made before copying over the 3.1 files. I&#8217;ve been bitten by MDT issues too often to not make backups of stuff I&#8217;m overwriting! 😉
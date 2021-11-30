---
id: 117
title: Install smartctl on Ubuntu
date: 2007-08-06T17:59:40+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/08/06/install-smartctl-on-ubuntu/
permalink: /2007/08/06/install-smartctl-on-ubuntu/
ratings_users:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
ratings_score:
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
  - Linux
---
To install smartctl (and smartd with it):

    sudo apt-get install smartmontools

Why would you want SmartMonTools?

> The smartmontools package contains two utility programs (smartctl and smartd) to control and monitor storage systems using the Self-Monitoring, Analysis and Reporting Technology System (S.M.A.R.T.) built into most modern ATA and SCSI hard disks. It is derived from the smartsuite package, and includes support for ATA/ATAPI-5 disks. It should run on any modern Linux system.

<cite><a href="http://packages.ubuntu.com/feisty/utils/smartmontools">Ubuntu smartmontools page</a></cite>

Very handy; especially as the OS drive just died in the RAID5 box 🙁 I&#8217;m now taking extra precautions!
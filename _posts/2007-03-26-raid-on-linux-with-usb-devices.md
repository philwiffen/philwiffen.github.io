---
id: 39
title: RAID on Linux with USB devices
date: 2007-03-26T19:36:03+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/03/26/raid-on-linux-with-usb-devices/
permalink: /2007/03/26/raid-on-linux-with-usb-devices/
categories:
  - Hardware
  - Linux
---
Whilst studying for the Linux+ Exam just now, something hit me. If you ever run out of SATA/PATA ports on a system, you could just add more drives on the USB bus. this would be nice for the [new RAID5 set up](http://www.kabri.uk/2007/03/14/raid-5-in-ubuntu-with-mdadm/). Granted there&#8217;s the physical space/storage issues, but it&#8217;s still properly accessible storage. I wonder if mdadm would support the hot-plugability of USB in a RAID array. Hmmm&#8230; that would be very cool.
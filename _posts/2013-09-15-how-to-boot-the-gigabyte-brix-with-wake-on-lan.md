---
id: 997
title: How to boot the Gigabyte Brix with Wake-On-LAN
date: 2013-09-15T21:54:55+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=997
permalink: /2013/09/15/how-to-boot-the-gigabyte-brix-with-wake-on-lan/
categories:
  - Home Lab
tags:
  - Gigabyte Brix
  - homelab
---
I&#8217;ve been playing with getting the Gigabyte Brix to Wake-On-LAN.

Most Windows-based tools didn&#8217;t work out of the box for me; but after some experimentation with the [Depicus Wake on LAN cmd tool](http://www.depicus.com/wake-on-lan/wake-on-lan-cmd.aspx), I worked out the information required to wake it up generally.

> `wolcmd <mac of target> <ip of target> <network subnet mask> <port 8900 or port 7>`

For my system, the command was:

> `wolcmd <mac without punctuation> 192.168.1.10 255.255.255.0 8900`

Hopefully this is useful for other people to WOL their Gigabyte Brix from any OS 🙂

Note that you must have Erp in the BIOS disabled for this to work. If you enable Erp in the BIOS (which enables super-low power usage) Wake-on-LAN doesn&#8217;t function from a powered-off state.
---
id: 866
title: 'NetApp &#8211; Check Shelf Firmware Version'
date: 2013-05-06T21:48:25+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=866
permalink: /2013/05/06/netapp-check-shelf-firmware-version/
categories:
  - NetApp
---
This post covers how to check the current firmware version of your disk shelves in a NetApp FAS storage system

<!--more-->

# From the filer console

> `sysconfig -v`

Then look for &#8220;Shelf <number>&#8221;. The firmware revision should be on that line:

<p style="padding-left: 30px;">
  <img loading="lazy" class="alignnone size-full wp-image-870" alt="netapp shelf firmware console" src="http://www.kabri.uk/wp-content/uploads/2013/05/netapp-shelf-firmware-console.png" width="709" height="93" />
</p>

# From a Trusted Linux host

> `rsh <filer hostname> sysconfig -v | grep Shelf`

<p style="padding-left: 30px;">
  <img loading="lazy" class="alignnone size-full wp-image-869" alt="netapp shelf firmware rsh" src="http://www.kabri.uk/wp-content/uploads/2013/05/netapp-shelf-firmware-rsh.png" width="709" height="82" />
</p>

# Compare

Then head off to support.netapp.com to check out if you need an upgrade 🙂
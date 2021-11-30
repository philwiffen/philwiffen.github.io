---
id: 162
title: 'Vista: The specified print monitor is unknown'
date: 2007-10-29T21:19:03+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/10/29/vista-the-specified-print-monitor-is-unknown/
permalink: /2007/10/29/vista-the-specified-print-monitor-is-unknown/
ratings_users:
  - "1"
  - "1"
  - "1"
  - "1"
  - "1"
ratings_score:
  - "5"
  - "5"
  - "5"
  - "5"
  - "5"
ratings_average:
  - "5"
  - "5"
  - "5"
  - "5"
  - "5"
categories:
  - Device Drivers
  - Troubleshooting
  - Windows
tags:
  - Troubleshooting
  - vista
  - Windows
---
![The specified print monitor is unknown](http://www.kabri.uk/wp-content/uploads/2007/10/the-specified-print-monitor-is-unknown.png)

### Symptoms

When trying to install a shared network printer in Windows Vista, you get an error which states:

> Windows cannot connect to the printer.  
> The specified print monitor is unknown.

### The Cause

This is a bug in Vista. If you disable the UAC, Vista is seemingly unable to add a network printer.

### The Fix

To fix this, you&#8217;ll need to install a &#8220;Performance and Reliability Update&#8221;, [KB938979](http://support.microsoft.com/kb/938979). Bizarrely, this update is listed as Optional by Windows Update, and so you may not have installed it. I shall refrain from commenting further on the lunacy of this 😉
---
id: 685
title: MDT 2010, IE9, offlineServicing error
date: 2011-04-05T10:20:44+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=685
permalink: /2011/04/05/mdt-2010-ie9-offlineservicing-error/
categories:
  - Desktop Deployment
  - Miscellaneous
---
Came across this the other day and didn&#8217;t see anything come up in a Google search so figured I&#8217;d blog it.

If you&#8217;ve recently added Internet Explorer 9 (IE9) to your MDT deployment, and you&#8217;re getting an offlineServicing error when deploying an OS, you may want to check this out.

The problem seems to occur when:

  * You&#8217;re running Microsoft Deployment Toolkit 2010
  * You&#8217;re deploying Windows 7 with SP1 integrated
  * You&#8217;ve added IE9 in .cab format to the deployment via Packages
  * When deploying an OS, you get a fatal error saying: &#8220;Windows could not apply unattend settings during pass [offlineServicing]&#8221;

To fix the problem, I removed the IE9 .cab from Packages and instead, integrated it into the install.wim image, using these instructions: [Windows 7 &#8211; Add or Remove Packages Offline](http://technet.microsoft.com/en-us/library/dd744559(WS.10).aspx)

I will attempt to write up proper instructions when I can, but the above link should provide you with enough information to work it out 🙂
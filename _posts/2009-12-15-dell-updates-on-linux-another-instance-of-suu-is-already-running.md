---
id: 578
title: 'Dell Updates on Linux &#8211; Another instance of SUU is already running'
date: 2009-12-15T13:45:15+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2009/12/15/dell-updates-on-linux-another-instance-of-suu-is-already-running/
permalink: /2009/12/15/dell-updates-on-linux-another-instance-of-suu-is-already-running/
categories:
  - Miscellaneous
tags:
  - Dell SUU
---
If you&#8217;re trying to run Dell&#8217;s SUU on a Linux box and get the error &#8220;Another instance of SUU is already running&#8221;, check out [this FAQ](http://support.euro.dell.com/support/edocs/software/smsuu/1.6/en/ug/html/faq.htm)

I have summarised the steps below:

chattr -i /var/log/dell/suu/suu.lck  
rm -f /var/log/dell/suu/suu.lck

You can then run SUU 🙂
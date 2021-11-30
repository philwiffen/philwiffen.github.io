---
id: 696
title: Finally, a management tool for Bitlocker
date: 2011-04-15T12:53:31+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=696
permalink: /2011/04/15/finally-a-management-tool-for-bitlocker/
categories:
  - Security
tags:
  - BitLocker
  - FDE
  - full disk encryption
  - windows 7
---
I first deployed Bitlocker and AD integration with Windows 7 Enterprise back before it was publicly released (that gap between when it gets released to Volume Licence customers, but not to the public). It wasn&#8217;t easy, and I had to use some interesting hacks and self-discovered cludges gleaned from old Vista documentation, as the Win 7 documentation hadn&#8217;t been released by Microsoft at the time. I had meant to document and release it as a quick-fix blog entry but the time passed and everything can be done properly now.

Since deployment, Bitlocker has been fantastic. The only issue we&#8217;ve had with Bitlocker since we deployed it is that of ensuring that end-users don&#8217;t suspend it or disable it, and that we most definitely have a good backup of the recovery key.

Effectively, without a management tool, you fly a bit blind until a problem comes up, or a Bitlockered laptop ends up in your lap with it disabled. Ignorance shouldn&#8217;t be bliss when it comes to full disk encryption and protecting your company&#8217;s data.

The AD backup of keys is a particular pain, as we&#8217;ve found that sometimes, Bitlocker just forgets to back itself up to AD when it&#8217;s enabled. To mitigate this, we&#8217;ve just instructed Bitlocker to also copy the key to a secure fileshare when it&#8217;s enabled during the MDT task, as well as backing it up to AD.

Fortunately, Microsoft have started to build a Bitlocker management tool called Microsoft Bitlocker Administration and Management. You can read more about it on the [Windows Team Blog](http://windowsteamblog.com/windows/b/springboard/archive/2011/02/09/microsoft-announces-microsoft-bitlocker-administration-and-monitoring-mbam.aspx).

It&#8217;s still in Beta, but I&#8217;m looking forward to trying this out!
---
id: 539
title: 'Can&#8217;t install BitLocker Recovery Password Viewer on Server 2008 SP2?'
date: 2009-08-13T15:24:10+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2009/08/13/cant-install-bitlocker-recovery-password-viewer-on-server-2008-sp2/
permalink: /2009/08/13/cant-install-bitlocker-recovery-password-viewer-on-server-2008-sp2/
categories:
  - Miscellaneous
tags:
  - BitLocker
  - microsoft
  - Server 2008
---
If you can&#8217;t install the &#8220;BitLocker Recovery Password Viewer for Active Directory Users and Computers tool&#8221; on Server 2008, it&#8217;s probably because you&#8217;re running SP2. Sigh.

When you try to run the Windows6.0-KB928202-x64.msu or Windows6.0-KB928202-x86.msu file you&#8217;ll get the error message:

&#8220;The update does not apply to your system&#8221;

This is because it doesn&#8217;t seem to support Server 2008 with SP2.

[Full details here](http://social.technet.microsoft.com/Forums/en-US/winservergen/thread/ec9bbfa6-68e4-463e-b36d-c91b50523bea)

Oh, and sorry for the lack of posts. Life&#8217;s a bitch ain&#8217;t it 😉
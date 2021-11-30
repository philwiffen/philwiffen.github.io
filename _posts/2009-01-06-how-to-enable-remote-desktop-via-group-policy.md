---
id: 499
title: How to enable Remote Desktop via Group Policy
date: 2009-01-06T17:14:01+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=499
permalink: /2009/01/06/how-to-enable-remote-desktop-via-group-policy/
aktt_notify_twitter:
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
categories:
  - General IT
tags:
  - group policy
  - RDC
  - RDP
  - remote desktop
  - Troubleshooting
---
This one had me stumped, but it&#8217;ll teach me to search the internet properly before blundering through. Even if you allow the Windows Firewall to accept Remote Desktop Connections you still need to enable Terminal Services elsewhere in the GP hierarchy. D&#8217;oh!

Here&#8217;s what you need to enable Remote Desktop remotely:

Computer Configuration > Administrative Templates > Network > Network Connections > Windows Firewall > Domain Profile > Windows Firewall: Allow Remote Desktop Exception

Computer Configuration > Administrative Templates > Windows Components > Terminal Services > Allow users to connect remotely using Terminal Services

Enable both of those options and you&#8217;ll be Remote Desktop-ing into PCs by the next day 🙂 (or rather, until your Domain clients refresh their Group Policy settings ;))

<noscript>
  <A href="http://ws.amazon.co.uk/widgets/q?rt=ss_ssw&ServiceVersion=20070822&MarketPlace=GB&ID=V20070822%2FGB%2Fmincir0e-21%2F8003%2F87c3eba7-98d6-4c50-86a8-8113a5fb0a11&Operation=NoScript" _mce_href="http://ws.amazon.co.uk/widgets/q?rt=ss_ssw&ServiceVersion=20070822&MarketPlace=GB&ID=V20070822%2FGB%2Fmincir0e-21%2F8003%2F87c3eba7-98d6-4c50-86a8-8113a5fb0a11&Operation=NoScript">Amazon.co.uk Widgets</A>
</noscript>
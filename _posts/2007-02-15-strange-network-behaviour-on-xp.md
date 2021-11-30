---
id: 24
title: Strange network behaviour on XP
date: 2007-02-15T14:42:37+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://kabri.uk/?p=24
permalink: /2007/02/15/strange-network-behaviour-on-xp/
categories:
  - Networking
  - Windows
---
This is a curiousity rather than a true solution. This morning, on booting his PC, a colleague found his PC refused to browse websites and (apparently) would not connect to any network shares, yet it could FTP to an external website and ping/tracert google.com. After booting XP, and entering user details (&#8220;loading your personal settings&#8230;&#8221;) the system would idle until the network cable was pulled from the NIC. The only thing which changed is that I installed VMWare Server Console on the system the day before (not the server itself, so it shouldn&#8217;t have added virtual NICs or messed with settings).

I solved the problem by uninstalling the NIC driver and letting it re-install after a reboot, but I&#8217;d love to know what may have caused the issue!
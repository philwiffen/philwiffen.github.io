---
id: 559
title: Making Windows 7 and Vista play nice with SAMBA
date: 2009-10-20T17:44:53+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=559
permalink: /2009/10/20/making-windows-7-and-vista-play-nice-with-samba/
categories:
  - Miscellaneous
---
If Windows 7 and Vista won&#8217;t work &#8220;properly&#8221; with your SAMBA servers, give this a try:

  1. <span style="background-color: #ffffff;">Create a new Group Policy Object in GPMC, and give it a name. I chose &#8220;Samba Compatibility&#8221;.</span>
  2. <span style="background-color: #ffffff;">Edit the GPO&#8230;</span>
  3. <span style="background-color: #ffffff;">Navigate to : Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options > Network Security</span>
  4. <span style="background-color: #ffffff;">Now edit the setting &#8220;Network security: LAN Manager Authentication level&#8221;, and change it to &#8220;Send LM & NTLM &#8211; use NTLMv2 session security if negotiated&#8221;.</span>
  5. <span style="background-color: #ffffff;">Apply that GPO to the appropriate OU, and you&#8217;re away* 🙂</span>

* People will probably need to reboot for the changes to take effect.

Key symptoms we saw were Vista/Win7 rejecting the initial connection, prompting for a username and password, then rejecting the domain credentials you just entered. This fixes those issues!
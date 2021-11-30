---
id: 156
title: 'Windows XP Service Pack 2 Halts on &#8220;Checking Product Key&#8221;'
date: 2007-10-15T13:33:40+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/10/15/windows-xp-service-pack-2-halts-on-checking-product-key/
permalink: /2007/10/15/windows-xp-service-pack-2-halts-on-checking-product-key/
ratings_users:
  - "3"
  - "3"
  - "3"
  - "3"
  - "3"
ratings_score:
  - "13"
  - "13"
  - "13"
  - "13"
  - "13"
ratings_average:
  - "4.33"
  - "4.33"
  - "4.33"
  - "4.33"
  - "4.33"
categories:
  - Troubleshooting
  - Windows
---
If you&#8217;re installing Windows XP Service Pack 2 and it halts or hangs on you while it is allegedly &#8220;Checking Product Key&#8221;, you can fix it like so:

> 1) Please go into the CMD prompt (Start/Run &#8211;> cmd.exe )
> 
> 2) Then type cd /d %windir%\inf and make sure we are in that  
> directory.
> 
> 3) Then type ren oem\*.inf oem\*.old, it will go back to the prompt  
> after giving you some error (Do not worry about it)
> 
> 4) Then type ren oem\*.pnf oem\*.old1, it will go back to the prompt  
> after giving you some error (Do not worry about it)
> 
> 5) Then goto start &#8211; run &#8211; type &#8220;%windir%\inf&#8221; and you will see  
> the files in the folder.
> 
> 6) Then find the file by name INFCACHE.1 and take a backup of it  
> to desktop (by copying it to desktop) and delete the INFCACHE.1  
> from c:\windows\inf.
> 
> 7) Close all windows and reboot the computer to safe mode and  
> start the installation of SP2 and it should go fine. 

This solution is dotted all around the internet, but I can&#8217;t find it&#8217;s original source. If you know the source, let me know and I&#8217;ll credit it correctly.
---
id: 110
title: '&#8220;My computer is running slow&#8221;'
date: 2007-07-20T13:55:23+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/07/20/my-computer-is-running-slow/
permalink: /2007/07/20/my-computer-is-running-slow/
categories:
  - Troubleshooting
  - Windows
---
In an interview a while back, I was asked to troubleshoot a Windows XP Laptop. The scenario was pretty simple: A client had reported that their Laptop had begun to run very slowly, particularly when booting; and it was my job to find the problem.

I thought I&#8217;d write down my usual procedure for this kind of scenario. Let&#8217;s go!

#### Check for Virii and Malware

Virii and Malware often consume large amounts of CPU time while going about their nefarious business, so let&#8217;s check those first:

  * Check Anti-virus is installed and up-to-date. Perform a manual check just in case.
  * Check Anti-Malware / Anti-Spyware is installed and up-to-date. Again, perform a manual check.
  * Spybot S&D, HijackThis, CWShredder, and Rootkit Revealer are tools that I find incredibly useful. 
  * [Filehippo](http://www.filehippo.com) is a great, centralised, place to find free and open-source apps for general troubleshooting.

#### Check your Startup programs and Services

Some useless, and damaging, things can get into your system Startup and Services areas. For example, do you really need to have QuickTime load every time your PC boots? This is another good place to check for Malware, and weird names like &#8220;fke38282gje.exe&#8221; should immediately flag your attention.

  * Check the Startup tab in the System Configuration Utility for anything suspect (Start > Run&#8230; > <kbd>msconfig</kbd>). 
  * While you&#8217;re there, check in the Services tab for anything out of place. 
  * Google anything you find, and you&#8217;ll usually find out if it&#8217;s malicious or not.

[![System Configuration Utility](http://www.kabri.uk/wp-content/uploads/2007/07/2007-07-20_132922.thumbnail.png)](http://www.kabri.uk/wp-content/uploads/2007/07/2007-07-20_132922.png "System Configuration Utility")

#### Defrag and RAM

There are of course, perfectly natural reasons for a system&#8217;s slow down. The two main ones being a fragmented hard drive, and a lack of sufficient RAM.

  * Check Hard Drive fragmentation (Right click My Computer > Manage > Storage > Disk Defragmenter).
  * Check your RAM (Right click My Computer > Properties). XP really should have at least 512MB of RAM.

[![Disk Defragmenter](http://www.kabri.uk/wp-content/uploads/2007/07/2007-07-20_132457.thumbnail.png)](http://www.kabri.uk/wp-content/uploads/2007/07/2007-07-20_132457.png "Disk Defragmenter")

#### Less likely causes

In addition, you may want to check a few other things which are much less likely.

As the PC was reported to be slow to boot, check the DHCP Server and also the DHCP settings on the client PC. If a system is set to grab a DHCP address it will often wait a long period of time, for a response from the DHCP server, before timing out. After that it gives itself an AUTO-IP and continues to load. Because nothing really happens for a while, this will appear as though the PC is slow to boot. A time out might occur if the DHCP server is down, or there&#8217;s a problem with your network downstream.

If the PC is reported as being generally slow, check that the Hard Drive is running in DMA Mode, and hasn&#8217;t fallen back to PIO mode. PIO is a slower, and much more CPU intensive, method of accessing Hard Drives than DMA. Often if Windows notices that data is being corrupted in DMA (CRC failures), it&#8217;ll fall back to PIO mode, resulting in a much slower system. Steps: Right click My Computer > Manage > Device Manager > IDE ATA/ATAPI Controllers. Check both Primary and Secondary IDE Channels by right clicking, Properties, then looking in the Advanced Settings tab. 

Check out this [Microsoft KB article](http://support.microsoft.com/kb/817472/) for a lot more detail on the issue.

[![2007-07-16_145631.png](http://www.kabri.uk/wp-content/uploads/2007/07/2007-07-16_145631.thumbnail.png)](http://www.kabri.uk/wp-content/uploads/2007/07/2007-07-16_145631.png "2007-07-16_145631.png")

**  
Did this help you at all? Is there anything I should add? Let me know in the comment section below!**
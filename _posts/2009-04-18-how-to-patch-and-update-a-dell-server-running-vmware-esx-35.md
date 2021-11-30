---
id: 529
title: How to patch and update a Dell Server running VMware ESX 3.5
date: 2009-04-18T13:19:57+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=529
permalink: /2009/04/18/how-to-patch-and-update-a-dell-server-running-vmware-esx-35/
categories:
  - General IT
  - Virtualisation
tags:
  - dell patch updates
---
In this post, we&#8217;re going to run through patching/upgrading the firmware on a Dell PowerEdge 1950 III Server running VMware ESX 3.5.

The procedure should also apply to most recent Dell Servers running ESX 3.5, but your mileage may vary 🙂

**Get your hands on the Software Update Utility DVD ISO and Burn it.**

In terms of time, this is pretty much half the job, believe it or not. You&#8217;ll need to goto support.dell.com, find your Dell Server, and get the Dell Updates DVD ISO. For the PowerVault 1950 III, go [here](http://support.euro.dell.com/support/downloads/driverslist.aspx?c=uk&l=en&s=gen&&SystemID=PWE_1950&os=WNET&osl=en&servicetag=&catid=-1&impid=-1&deviceid=16823&libid=36&releaseid=R217522&formatcnt=3&vercnt=6) and then look under Systems Management for “Dell – DVD iso Images” “applies to: DVD ISO – Dell Server Updates”.

**Patching the Dell Server**

 

  1. Be sure to VMotion off any Guest OSs that you need to keep running. Shut down everything else, and then put the target server into Maintenance Mode.
  2. Insert the Updates DVD into the Server
  3. Bring up a command prompt, as root, on the Server and run the following to mount the CD-ROM: _<span lang="EN-US">mount</span>_<span><span lang="EN-US"><em> </em></span></span><span><span lang="EN-US"><em>/mnt/</em></span></span>_<span lang="EN-US">cdrom</span>_
  4. Now navigate to the CD-ROM: _cd /mnt/cdrom_
  5. Check what&#8217;s upgradeable on your system: _sh suu -c_
  6. If you&#8217;re happy, then run the upgrade: _sh suu -u_
  7. That&#8217;s it, you&#8217;re done 🙂
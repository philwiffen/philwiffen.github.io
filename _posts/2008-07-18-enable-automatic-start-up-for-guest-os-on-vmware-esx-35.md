---
id: 313
title: Enable Automatic Start Up for Guest OS on VMware ESX and ESXi
date: 2008-07-18T14:36:01+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=313
permalink: /2008/07/18/enable-automatic-start-up-for-guest-os-on-vmware-esx-35/
categories:
  - Design and Usability
  - Virtualisation
---
This one had me tearing my hair out. We needed to enable auto startup on some of our Virtual Machines on the VMware ESX server, but I couldn&#8217;t for the life of me work out how. After a stupid amount of Googling around, turning up nothing, I actually [<acronym title="Read The Fracking Manual">RTFM</acronym>](http://www.vmware.com/pdf/vi3_35/esx_3/r35/vi3_35_25_admin_guide.pdf)! Page 177-178 had the answers 😉

Here&#8217;s how to do it:

Launch the Virtual Infrastructure Client. If you don&#8217;t have it, just http:// to your VMware ESX host and grab it from the front page.

Go to the Configuration tab of your ESX Server, then click on Virtual Machine Startup/Shutdown.

[<img loading="lazy" class="alignnone size-full wp-image-315" title="VMware ESX Configuration > VM Start up / Shutdown" alt="" src="http://www.kabri.uk/wp-content/uploads/2008/07/2008-07-17_112136.png" width="500" height="259" />](http://www.kabri.uk/wp-content/uploads/2008/07/2008-07-17_112136.png)

By default (I&#8217;m pretty sure) automatic startup is disabled. To enable it, click on &#8220;Properties&#8230;&#8221; on the far upper right of the window.

You&#8217;ll now see this window:

[<img loading="lazy" class="alignnone size-full wp-image-316" title="VM Automatic Startup/Shutdown Properties" alt="" src="http://www.kabri.uk/wp-content/uploads/2008/07/2008-07-17_112338.png" width="500" height="323" />](http://www.kabri.uk/wp-content/uploads/2008/07/2008-07-17_112338.png)

Check/Tick &#8220;Allow virtual machines to start and stop automatically with the system&#8221;.

Now, this is the bit where I nearly cried&#8230;

[<img loading="lazy" class="alignnone size-full wp-image-319" title="VM auto start - default" alt="" src="http://www.kabri.uk/wp-content/uploads/2008/07/2008-07-17_112839.png" width="499" height="174" />](http://www.kabri.uk/wp-content/uploads/2008/07/2008-07-17_112839.png)

You know you want to &#8220;enable&#8221; your Guest OSes to automatically boot, but how? I tried clicking and dragging, right clicking for a context menu to enable &#8220;Automatic start up&#8221; and gave up.

Turns out, you need to click on the Guest OS you&#8217;d like to enable, and then click &#8220;Move Up&#8221; until it sits underneath the &#8220;Automatic startup&#8221; title. Argh!

[<img loading="lazy" class="alignnone size-full wp-image-318" title="VM auto start - moved up" alt="" src="http://www.kabri.uk/wp-content/uploads/2008/07/2008-07-17_112852.png" width="499" height="174" />](http://www.kabri.uk/wp-content/uploads/2008/07/2008-07-17_112852.png)

I really hope this helps someone out! 🙂
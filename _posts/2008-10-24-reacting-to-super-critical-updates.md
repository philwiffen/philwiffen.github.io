---
id: 447
title: Reacting to Super-Critical Updates (MS08-67)
date: 2008-10-24T15:50:07+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=447
permalink: /2008/10/24/reacting-to-super-critical-updates/
aktt_notify_twitter:
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
categories:
  - Business
  - DisplayLink
  - Security
  - Windows
tags:
  - critical update
  - Security
  - Windows
---
Yesterday evening, at 6pm BST, Microsoft released an &#8216;Emergency&#8217; [Security Update](http://support.microsoft.com/?kbid=958644) MS08-67, for Windows-based Operating Systems. The update plugs a hole in Windows that could allow a Virus/Worm to automatically infect a Windows PC without any user intervention.

I thought I&#8217;d document what actions I took, in case it helps out anyone in the future. I&#8217;d also be interested to hear how _you_ handled the situation, particularly if you did something I missed, or if you think I could have done things better!

**History repeating&#8230;**

Although I remember the impact of Sasser and MyDoom, I&#8217;ve never been in the trenches when such a critical update has been launched for Windows.

No-one likes working late at night, but I didn&#8217;t fancy the chances that a 0-day exploit may be released and in the wild before we can patch our mission critical servers; so as soon as I found out, I started working on a plan.

**The Plan**

The plan was relatively simple: Get the update to as many PCs as possible, as soon as possible; with an emphasis on any Servers that provide business-critical services.

Simple enough, but what next?

**WSUS**

About a month back we setup an internal [WSUS](http://en.wikipedia.org/wiki/Windows_Server_Update_Services) server to centralise Windows Updates &#8211; quite handy for this type of scenario! The main thing here is to ensure that WSUS has the updates downloaded and approved, ready for deployment. Fortunately it had, as it performs a sync every evening, and automatically approves Critical Updates.

**Group Policy**

To ensure PCs get the update as fast as possible, we needed to open up GPMC and re-configure all existing Group Policy Objects (GPOs) that address Windows Update configuration.

The Windows Updates settings are under Computer Configuration > Administrative Templates > Windows Components > Windows Update.

Note that, if you don&#8217;t have WSUS, you can still make the changes outlined below in order to minimise Time-to-Patch. If you haven&#8217;t set &#8220;Specify intranet Microsoft update service location&#8221;, PCs will automatically ask Microsoft&#8217;s update servers on the internet.

What we&#8217;re looking to do is:

&#8211; Set all PCs to download and schedule updates. This is abnormal for us as we allow our Engineers to dictate when to install updates as it can interfere with Software development and testing.

&#8211; Make sure each PC checks for updates with our WSUS server every hour, as opposed to every 22 hours.

&#8211; Set PCs to install the updates at 11am. This gives time for people to turn on their PCs, for the PCs to update their Group Policy settings and pick up the new settings, and then to check in with the WSUS server for the new update.

&#8211; If the PC missed the 11am deadline (e.g. it wasn’t on) it’ll check whether or not it has updates, and then install the updates after 30 minutes.

**Informing End-users**

A notification email was crafted to all employees, informing them of the severity of the update, what was being done, and what actions they should take. I&#8217;ll include a copy of the email I sent out at the [end of the post](#emailnotification)

**Protecting the business**

Last night, we couldn&#8217;t wait for WSUS to &#8220;offer&#8221; the update to our servers so I grabbed the Update and manually installed it on each business-critical server, rebooting them promptly.

**This morning**

That was last night out of the way. This morning and this afternoon I&#8217;ve been checking WSUS&#8217;s reports to see which PCs have the update installed. As of 1pm, at least 90% of PCs had installed and rebooted. I&#8217;ll be chasing the rest later 😉

**The notification**

As promised, here&#8217;s the Email notification sent out to employees:

>    
> Hi all,
> 
> Microsoft has just released a very serious critical security update for Windows operating systems.
> 
> To see how this affects you, please see below.
> 
> **Cambridge Employees**
> 
> Tomorrow we will be rolling out an essential security update to all Domain-connected Windows PCs. **This update is mandatory**. If you press Control+Alt+Delete to log in, you are on the domain. If you do not press Ctrl+Alt+Del to log in you should follow the advice for Non-Cambridge employees below.
> 
> Although we will be trying our best to force this update out. It’s advisable that if you see the “Yellow shield” in your Task Bar, you should click it and install all updates **reboot as soon as possible**.
> 
> Not doing so poses a serious risk to DisplayLink’s networks.
> 
> **Non-Cambridge Employees **
> 
> If you are not based in Cambridge, you should visit [Windows Update](http://www.windowsupdate.com/) as soon as possible and install all updates, specifically [this one](http://www.microsoft.com/downloads/results.aspx?pocId=&freetext=KB958644&DisplayLang=en).
> 
> **DisplayLink Servers**
> 
> **<span style="font-weight: normal;">Servers in the UK will have the update installed and be rebooted as soon as possible to ensure we’re protected.</span>**
> 
> **Further information**
> 
> Further information on this Critical update can be found on [Microsoft’s KB article](http://support.microsoft.com/?kbid=958644).
> 
> Thanks go to Dave Hill for spotting this one on [The Register](http://www.theregister.co.uk/2008/10/23/windows_emergency_update/)!
> 
> Cheers,  
> Phil Wiffen  
> IT Engineer
> 
>  

**How did you handle it?**

As I said earlier, I&#8217;d also be interested to hear how you handled the situation, particularly if you did something I missed, or if you think I could have done things better! Let me know in the comments 🙂
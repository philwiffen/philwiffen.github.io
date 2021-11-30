---
id: 103
title: Network policy stops you from using Windows Update
date: 2007-07-02T13:44:42+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/07/02/network-policy-stops-you-from-using-windows-update/
permalink: /2007/07/02/network-policy-stops-you-from-using-windows-update/
categories:
  - Security
  - Troubleshooting
  - Windows
---
After re-installing the OS on a Dell Powervault 715n, I remembered that out of the box, it won&#8217;t connect to Windows Update (which is of course really, _really_ stupid for a Windows 2000 Server based NAS).

If you RDC into the box, and then try to connect to Windows Update, you&#8217;ll see a message like this:

> Access Denied
> 
> Network policy settings prevent you from using Windows Update to download and install updates on your computer.
> 
> If you believe you have received this message in error, please check with your system administrator.

### Solution

To get around this on the 715N, follow these instructions:

  1. Log in as Administrator
  2. Go _Start_ > _Run&#8230;_ > gpedit.msc
  3. In the Left pane: Open _User Configuration_, _Administrative Templates_, and then click _Start Menu and Taskbar_
  4. In the Right pane: Double-click on _Disable and remove links to Windows Update_
  5. Choose &#8216;Disable&#8217; and click OK
  6. You can now get Windows Updates via the Start Menu
  7. Don&#8217;t forget to Enable Automatic Updates! (_Control Panel_ > _Automatic Updates_)

For any other Operating System, have a look at the [Microsoft KB article](http://support.microsoft.com/kb/326686)
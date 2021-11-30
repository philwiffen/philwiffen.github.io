---
id: 982
title: Manage Hyper-V Server 2012 remotely from Windows 7 with PowerShell
date: 2013-08-09T15:31:19+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=982
permalink: /2013/08/09/manage-hyper-v-server-2012-remotely-from-windows-7-with-powershell/
categories:
  - Hyper-V
  - PowerShell
  - Windows
---
I&#8217;ve been looking into Hyper-V Server 2012 recently, as it has some very nice Enterprise-grade capabilities for free; and the zero cost makes it very attractive for Labs that simply don&#8217;t have the budget for VMware. The only downsides I can see currently are that remote management is a pain from Windows 7.

# Remote Management from Windows 7

Here&#8217;s the situation:

  * Much of the management of Hyper-V Server 2012 is via PowerShell 3.0 Hyper-V cmdlets, or the Hyper-V Manager GUI available in Windows 8/Server 2012.
  * PowerShell 3.0 can be installed on Windows 7, but it does **not** include the Hyper-V cmdlets that would enable you to manage Hyper-V remotely
  * The general consensus is to &#8220;Use Windows 8 or Server 2012&#8221; to manage Hyper-V Server 2012 remotely, as they include the Hyper-V cmdlets. Unfortunately, this doesn&#8217;t work in all scenarios and organisations.

# Hello, PowerShell Remoting

A potential solution I found is to leverage PowerShell Remoting. You can use Enter-PSSession to &#8220;jump onto&#8221; the Hyper-V server from Windows 7, and then interact with PowerShell as though you were directly on the remote Hyper-V host.

<p style="padding-left: 30px;">
  <img loading="lazy" class="alignnone size-full wp-image-986" alt="screenshot-hyperv-remoting-from-windows7-2" src="http://www.kabri.uk/wp-content/uploads/2013/08/screenshot-hyperv-remoting-from-windows7-2.png" width="509" height="79" />
</p>

Here&#8217;s an example:

> `Enter-PSSession -ComputerName hyperv-server-01`

To get a list of available Hyper-V cmdlets:

> `Get-Command -Module Hyper-V`

&nbsp;

Admittedly, this might make scripting a bit more difficult, but I imagine it&#8217;s possible to do if you really can&#8217;t use Windows 8 or Server 2012.

Hope this is useful! 🙂
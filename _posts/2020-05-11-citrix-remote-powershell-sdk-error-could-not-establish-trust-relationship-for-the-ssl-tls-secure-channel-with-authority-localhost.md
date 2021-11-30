---
id: 1760
title: 'Citrix Remote PowerShell SDK error: &#8220;Could not establish trust relationship for the SSL/TLS secure channel with authority &#8216;localhost&#8217;.&#8221;'
date: 2020-05-11T19:56:08+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: https://kabri.uk/?p=1760
permalink: /2020/05/11/citrix-remote-powershell-sdk-error-could-not-establish-trust-relationship-for-the-ssl-tls-secure-channel-with-authority-localhost/
categories:
  - Citrix
  - PowerShell
---
If you see the following error when trying to run cmdlets from the Citrix Remote PowerShell SDK

<pre class="entry-title single-title">“Could not establish trust relationship for the SSL/TLS secure channel with authority ‘localhost’.”</pre>

Check and make sure you are running PowerShell in its 64-bit flavour, and not 32-bit (x86).

## WTF?

I had this issue recently when automating some tasks with Jenkins talking to Citrix Cloud, using the Citrix Remote PowerShell SDK:

<blockquote class="twitter-tweet">
  <p dir="ltr" lang="en">
    Jenkins has defeated me this evening. I can make the exact same script run on the jenkins host in its own powershell window, but it fails inside jenkins saying &#8220;Get-BrokerSession : Could not establish trust relationship for the SSL/TLS secure channel with authority &#8216;localhost&#8217;.&#8221;
  </p>
  
  <p>
    — Phil Wiffen (@phil_wiffen) <a href="https://twitter.com/phil_wiffen/status/1259606414277906433?ref_src=twsrc%5Etfw">May 10, 2020</a>
  </p>
</blockquote>



On the same host as Jenkins, if I ran a PowerShell shell, and ran the exact same script, it&#8217;d work fine.

If I ran it in Jenkins, it would fail with an error like this:

<pre class="">Get-BrokerServiceInstance : Could not establish trust relationship for the SSL/TLS secure channel with authority 'localhost'.
At C:\WINDOWS\TEMP\jenkins297054977088542623.ps1:66 char:3
+ Get-BrokerServiceInstance
+ ~~~~~~~~~~~~~~~~~~~~~~~~~
+ CategoryInfo : InvalidOperation: (:) [Get-BrokerServiceInstance],SdkOperationException
+ FullyQualifiedErrorId : Citrix.XDPowerShell.Broker.NoServerErrorId,Citrix.Broker.Admin.SDK.GetBrokerServiceInstanceCommand</pre>

## Root Cause

The root cause is there&#8217;s something up with 32-bit PowerShell and the Citrix Remote PowerShell SDK.

Jenkins runs the 32-bit version of PowerShell because Jenkins itself is 32-bit. The reason the script worked in a PowerShell shell on the Jenkins host, was because the default on Windows is 64-bit PowerShell. As soon as I forced PowerShell 32-bit, I could reproduce the problem.

## The Fix

The fix is to force Jenkins to use PowerShell 64-bit. There&#8217;s two options I found:

  1. You can workaround it with some good tips here: <https://adamtheautomator.com/jenkins-powershll-64bit/#method-3-using-the-sysnative-powershell>
  2. Or you can fix it fully by making Jenkins run on 64-bit Java: <https://stackoverflow.com/questions/28331924/jenkins-powershell-plugin-is-running-32-bit-powershell-and-i-need-64bit>
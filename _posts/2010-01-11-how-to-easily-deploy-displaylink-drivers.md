---
id: 583
title: How to easily deploy DisplayLink drivers
date: 2010-01-11T10:01:32+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=583
permalink: /2010/01/11/how-to-easily-deploy-displaylink-drivers/
categories:
  - Miscellaneous
tags:
  - autoit
  - automated
  - DisplayLink
  - Driver
  - msi
  - silent install
---
Some quick notes on how we deploy DisplayLink drivers internally here at DisplayLink. Due to our unique requirements, we don&#8217;t deploy our software via GPSI, as our Developers need to use bleeding-edge drivers, rather than the publicly released ones!

Instead we deploy them manually when setting up a PC. DisplayLink IT uses the publicly available Corporare Install files, which are distributed as MSIs. This allows you to do silent, automated installs of our software without having to accept a EULA each time. For ease, I  use AutoIT to do the actual installation as it&#8217;s nice and flexible, and we tend to buy laptops on an ad-hoc/purpose specific basis, so Drive Imaging would consume more time than it would save!

  1. Get the DisplayLink Corporate Install files from here: http://www.displaylink.com/corporateinstall/ (You&#8217;ll need to register, but it&#8217;s a one-time thing)
  2. Extract the both the 32-bit and 64-bit MSIs in the zip file to somewhere useful. If you want to deploy them via GPSI, check out the PDF (I wrote it, and welcome any comments/suggestions, as I have a lot to learn about GPSI!)
  3. For silent installations, I put the MSIs all in one directory and just rename the files as appropriate for each architecture (see below for the naming I use)

The main command lines you need are:

32-bit:

> msiexec /i \\server\share\DisplayLinkCore-32bit.msi /norestart /passive
> 
> msiexec /i \\server\share\DisplayLinkSetup-32bit.msi /norestart /passive

64-bit:

> msiexec /i \\server\share\DisplayLinkCore-64bit.msi /norestart /passive
> 
> msiexec /i \\server\share\DisplayLinkSetup-64bit.msi /norestart /passive

Here&#8217;s the AutoIT code, should you need it:

    
    <div id="_mcePaste">If @OSArch = "X86" Then</div>
    <blockquote>
    <div id="_mcePaste">$PID = Run('msiexec /i \\server\share\DisplayLinkCore-32bit.msi /norestart /passive')</div>
    <div id="_mcePaste">ProcessWaitClose($PID)</div>
    <div id="_mcePaste">$PID = Run('msiexec /i \\server\share\DisplayLinkSetup-32bit.msi /norestart /passive')</div>
    <div id="_mcePaste">ProcessWaitClose($PID)</div></blockquote>
    <div id="_mcePaste">ElseIf @OSArch = "X64" Then</div>
    <blockquote>
    <div id="_mcePaste">$PID = Run('msiexec /i \\server\share\DisplayLinkCore-64bit.msi /norestart /passive')</div>
    <div id="_mcePaste">ProcessWaitClose($PID)</div>
    <div id="_mcePaste">$PID = Run('msiexec /i \\server\share\DisplayLinkSetup-64bit.msi /norestart /passive')</div>
    <div id="_mcePaste">ProcessWaitClose($PID)</div></blockquote>
    <div id="_mcePaste">EndIf</div>
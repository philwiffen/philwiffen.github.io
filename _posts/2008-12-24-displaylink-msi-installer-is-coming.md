---
id: 489
title: 'DisplayLink MSI Installer is coming&#8230;'
date: 2008-12-24T12:02:19+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=489
permalink: /2008/12/24/displaylink-msi-installer-is-coming/
aktt_notify_twitter:
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
categories:
  - Business
  - DisplayLink
  - Time Saving
  - Windows
tags:
  - corporate install
  - DisplayLink
  - gpsi
  - group policy
  - msi
---
The cat&#8217;s out of the bag 🙂 If you&#8217;re geeky enough to read release notes, you may have spotted this in our [4.6 release notes](http://www.displaylink.com/downloads/DisplayLink-ReleaseNotes-4.6.16208.txt):

> Support for corporate deployment of DisplayLink software  
> &#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;  
> It is now possible to obtain a DisplayLink software installation solution that supports automated and remote installation scenarios. This kind of installation requires specific installation steps, detailed in the User Guide that is part of the Corporate Installer.

Yup, it&#8217;s true: we&#8217;re releasing an MSI installer very soon.

I&#8217;m excited about this news on two fronts. Firstly, this is the first time that I&#8217;ve contributed directly to a software release; I wrote the Deployment User Guide, gave advice on what IT Administrators want from a corporate installer, and helped steer testing scenarios. Secondly, this feature will allow IT Administrators to deploy DisplayLink&#8217;s software onto thousands of PCs simply and easily, further strengthening our ease-of-use message. And I don&#8217;t need to tell you how awesome GPSI+MSI is for us IT admins! 🙂

The &#8220;Corporate Install&#8221; package is different to the standard software release and will require you to register with DisplayLink in order to obtain the MSI files and sign the EULA. Once obtained, you can then deploy DisplayLink software to all the computers in your network via Group Policy Software Installation. Of course, you can perform silent/unattended installs manually via msiexec if you wish as well.

It&#8217;s worth mentioning again that the MSI installer has not been released yet, but it is coming. 

Stay tuned for more info! 🙂
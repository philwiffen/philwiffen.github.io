---
id: 503
title: How to boot 64-bit Boot Image from WDS PXE when only 32-bit will show
date: 2009-01-09T15:55:59+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=503
permalink: /2009/01/09/how-to-boot-64-bit-boot-image-from-wds-pxe-when-only-32-bit-will-show/
aktt_notify_twitter:
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
categories:
  - Desktop Deployment
  - Windows
tags:
  - BDD
  - MDT
  - MDT 2008
  - PXE
  - Vista 64
  - WDS
---
This is something that has beeen bugging me ever since I set up our BDD 2007 + WDS setup almost a year ago. Even though I was able to create a 64-bit WIM boot image via MDT and load it onto the WDS server, the 64-bit Boot Image was never shown to me when PXE booting from a 64-bit capable PC. All I could see and boot, was the 32-bit boot images. Argh!

After fruitless searching I resigned myself to the fact that if I wanted to deploy Vista 64 I&#8217;d just burn an ISO of the 64-bit WinPE Boot Image and install from there. Fortunately, we rarely need to deploy 64-bit Vista, but this may change soon.

However, just now, I found the solution&#8230;

To enable 64-bit Boot Images via PXE with WDS, you need to run this command on the WDS Server:

> wdsutil /set-server /architecturediscovery:yes

Why this was never mentioned in the Documentation that I read for MDT/BDD I&#8217;ll never know (maybe I just missed it), but finally I can boot to 64-bit WinPE and deploy 64-bit Vista from the network, hooray! 😀

I found the answer on [EggHeadCafe](http://www.eggheadcafe.com/software/aspnet/32833682/deploing-64bits-on-server.aspx) by searching for: &#8220;mdt 2008 deploy 64-bit vista pxe&#8221;. Roughly half way down the hard-to-read page was the nugget I needed.

For reference, there&#8217;s a proper [Microsoft KB article](http://support.microsoft.com/kb/932447) explaining the solution.

Really hopes this helps someone out!
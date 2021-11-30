---
id: 542
title: How to apply MSP patch files to Adobe 9.1 MSI installer
date: 2009-08-26T15:39:30+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2009/08/26/how-to-apply-msp-patch-files-to-adobe-9-1-msi-installer/
permalink: /2009/08/26/how-to-apply-msp-patch-files-to-adobe-9-1-msi-installer/
categories:
  - Miscellaneous
tags:
  - Adobe Reader 9.1
  - deployment
  - gpsi
  - msi
---
To apply the MSP patch file to an Adobe 9.1 MSI installer, try this:

  1. <span style="background-color: #ffffff;">Download Adobe 9.1 MSI from here: <a href="ftp://ftp.adobe.com/pub/adobe/reader/win/9.x/9.1/enu/">ftp://ftp.adobe.com/pub/adobe/reader/win/9.x/9.1/enu/</a></span>
  2. <span style="background-color: #ffffff;">Download the latest 9.1 MSP patch file from here (currently 9.1.3): <a href="ftp://ftp.adobe.com/pub/adobe/reader/win/9.x/9.1.3/misc/">ftp://ftp.adobe.com/pub/adobe/reader/win/9.x/9.1.3/misc/</a></span>
  3. <span style="background-color: #ffffff;">Put these files in the same directory.</span>
  4. <span style="background-color: #ffffff;">Open up a command prompt, then navigate to that directory.</span>
  5. <span style="background-color: #ffffff;">Run the following command:<br /> <em>msiexec /p AdbeRdrUpd913_all_incr.msp /a AdbeRdr910_en_US.msi /qb</em></span>

This will apply the 9.1.3 patch directly to the 9.1 MSI file, ready for deployment. You can now deploy Adobe Reader 9.1 safe in the knowledge that it&#8217;s already patched to 9.1.3 😀
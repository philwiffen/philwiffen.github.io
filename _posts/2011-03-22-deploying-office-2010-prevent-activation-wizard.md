---
id: 658
title: 'Deploying Office 2010 &#8211; Prevent Activation Wizard'
date: 2011-03-22T11:45:52+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=658
permalink: /2011/03/22/deploying-office-2010-prevent-activation-wizard/
categories:
  - Desktop Deployment
  - Miscellaneous
---
If you&#8217;re deploying Microsoft Office Professional Plus 2010 with a MAK key, and you want to avoid the user seeing the Microsoft Office Activation Wizard when they first start up an Office application, follow these instructions:

  1. Run the Office 2010 Customization Tool (OCT)
  2. Open up your customised MSP file
  3. Go to: Setup > Add installations and run programs > Add&#8230;
  4. Then enter the information as seen in the image below. 
      1. Target: [SystemFolder]\cscript.exe
      2. Arguments: &#8220;C:\Program Files (x86)\Microsoft Office\Office14\ospp.vbs&#8221; /act  
        [](http://www.kabri.uk/wp-content/uploads/2011/03/Office-2010-Post-Activation.png)[](http://www.kabri.uk/wp-content/uploads/2011/03/Office-2010-Post-Activation1.png)[[<img loading="lazy" class="alignnone size-full wp-image-682" title="Office 2010 Post Activation" src="http://www.kabri.uk/wp-content/uploads/2011/03/Office-2010-Post-Activation3.png" alt="" width="502" height="497" />](http://www.kabri.uk/wp-content/uploads/2011/03/Office-2010-Post-Activation3.png)](http://www.kabri.uk/wp-content/uploads/2011/03/Office-2010-Post-Activation2.png)
  5. Don&#8217;t forget to save your MSP!

This will activate Office immediately after it is installed, so that it won&#8217;t pop up the Activation Wizard when the user first runs Office. Think of this as either a kind of pre-activation or post-activation of Office 2010.

This guide makes the following assumptions:

  1. You know how to load OCT (Office Customization Toolkit)
  2. You are deploying 32-bit Office onto 64-bit Windows
  3. You deploy Office 2010 at Deployment time using Microsoft Deployment Toolkit (although, for this to work, you don&#8217;t have to).
  4. You deploy Office 2010 using a MAK key.
  5. You store your MSP file in the \Updates\ within the Office 2010 installation files on the MDT share (again, for this to work, you don&#8217;t have to).

I found this info after hopelessly searching around, finally coming across this page on Microsoft [Technet](http://social.technet.microsoft.com/Forums/en-US/officevolact/thread/a3bc0396-f0bb-4060-a86e-f8575f0df34e/?prof=required).
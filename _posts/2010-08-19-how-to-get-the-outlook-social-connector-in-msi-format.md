---
id: 630
title: How to get the Outlook Social Connector in MSI format
date: 2010-08-19T16:42:47+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=630
permalink: /2010/08/19/how-to-get-the-outlook-social-connector-in-msi-format/
categories:
  - Miscellaneous
---
If you need to Deploy the Outlook Social Connector via GPSI, you&#8217;ll need to get your hands on the MSI files.

To do so, follow these instructions&#8230;

  1. [Download the OSC file](http://www.microsoft.com/downloads/details.aspx?displaylang=en&FamilyID=b638cc14-11e5-448a-b5a6-4f553ce81b94) from Microsoft
  2. Run the following command from a command prompt: outlooksocialconnector-x86-en-us.exe /extract:C:\osc\
  3. This will extract the msi files to c:\osc\
  4. You can then use the MSI file to deploy OSC! 🙂

If you want to integrate the MSP Patch files are well, just do this:

<div id="_mcePaste">
  <ol>
    <li>
      msiexec /p c:\osc\osc-x-none-en-us.msp /a \\yourserver\share\osc.msi
    </li>
    <li>
      msiexec /p c:\osc\oscintl-en-us.msp /a \\yourserver\share\osc.msi
    </li>
  </ol>
</div>

Then you&#8217;ll be deploying the MSI fully patched 🙂
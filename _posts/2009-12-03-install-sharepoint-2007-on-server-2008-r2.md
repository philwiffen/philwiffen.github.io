---
id: 573
title: Install SharePoint 2007 on Server 2008 R2
date: 2009-12-03T12:01:48+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=573
permalink: /2009/12/03/install-sharepoint-2007-on-server-2008-r2/
categories:
  - General IT
---
Currently playing with Sharepoint 2007 to enable our Execs to collaborate on documents and ran into this PITA 😉

**Problem:**

You can&#8217;t install SharePoint 2007 with SP1 on to a fresh copy of Server 2008 R2. You get a &#8220;This program is blocked due to compatibility issues&#8221; message, and asked to look at KB Article 962935 (which doesn&#8217;t actually exist at the time of writing!)

**Solution:**

You&#8217;ll need to slipstream Sharepoint 2007 SP2 into the Setup file. Brief summary is below:

Download the following&#8230;

[Microsoft Office SharePoint Server 2007 Trial Version (x64)](http://www.microsoft.com/downloads/details.aspx?displaylang=en&FamilyID=3015fde4-85f6-4cbc-812d-55701fbfb563)

[Sharepoint 2007 Service pack 2 (x64)](http://www.microsoft.com/downloads/details.aspx?displaylang=en&FamilyID=b7816d90-5fc6-4347-89b0-a80deb27a082)

Perform the following&#8230;

  1. Extract OfficeServerwithSP1.exe by executing &#8220;OfficeServerwithSP1.exe /extract:C:\Sharepoint2007\&#8221;
  2. Delete all the files inside C:\Sharepoint2007\Updates\
  3. Extract officeserver2007sp2-kb953334-x64-fullfile-en-us by executing &#8220;officeserver2007sp2-kb953334-x64-fullfile-en-us /extract:C:\Sharepoint2007\Updates\&#8221;
  4. Run C:\Sharepoint2007\setup.exe

Now you can install Sharepoint 2007 on Server 2008 R2!

Full instructions/references:

[MSDN Blog](http://blogs.msdn.com/sharepoint/archive/2009/10/02/install-sharepoint-server-2007-on-windows-server-2008-r2.aspx)  
[Technet Social](http://social.technet.microsoft.com/Forums/en/sharepointgeneral/thread/c7091bda-867e-49a1-9bc8-c2ef847c92e7)
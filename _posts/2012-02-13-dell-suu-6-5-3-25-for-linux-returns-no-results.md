---
id: 731
title: Dell SUU 6.5.3.25 for Linux returns no results
date: 2012-02-13T17:48:28+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=731
permalink: /2012/02/13/dell-suu-6-5-3-25-for-linux-returns-no-results/
categories:
  - Servers
tags:
  - dell
  - Linux
  - SUU
---
Bit of an odd one this, but I felt worth blogging about.

The latest Dell SUU (6.5.3.25) doesn&#8217;t seem to be able to detect applicable updates when it&#8217;s run on a Linux system.

You get the message:

> <pre>"bash-3.2# ./suu -c</pre>
> 
> <pre>------------------------------------------------
Welcome to the Dell OpenManageServer Update Utility.
Copyright (c) 2003-2011 Dell Inc. All Rights Reserved.
SUU Version: 6 .5 .3 .25</pre>
> 
> <pre><span style="color: #ff0000;"><strong>There are no software updates applicable to this system.</strong></span>
Please refer to the User Guide for more information about
prerequisites and supported systems."</pre>

Now, I know this isn&#8217;t true; because the current BIOS version is 3.0.0 and the one in the SUU repository is 6.0.7. Also, normally you get a comparison list of results, even if none of the updates can be applied.

If I downgrade SUU to 6.5.2.20, it works as expected.

## How do we fix this?

If you want to replace SUU 6.5.3 with a working SUU 6.5.2 you&#8217;ll need to:

  1. Download SUU [6.5.2](http://ftp.euro.dell.com/FOLDER00205240M/1/SUU_652.cab)
  2. Delete SUU_653.cab from C:\Users\<username>\AppData\Local\RepositoryManager\Payloads\
  3. Copy the SUU_652.cab that you just downloaded into C:\Users\<username>\AppData\Local\RepositoryManager\Payloads\
  4. Re-export your repository/SUU via Dell Repository Manager

Let me know how you get on!
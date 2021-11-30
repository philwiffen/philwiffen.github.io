---
id: 514
title: Automatically install Windows Updates / Hotfixes when installing Vista
date: 2009-02-25T10:12:43+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=514
permalink: /2009/02/25/automatically-install-windows-updates-hotfixes-when-installing-vista/
categories:
  - Desktop Deployment
  - Windows
tags:
  - updates
  - vista
---
If, like us, you run a <acronym title="Business Desktop Deployment">BDD</acronym> or <acronym title="Microsoft Deployment Toolkit">MDT</acronym> setup in order to install your Operating Systems, this might be useful 🙂

If you&#8217;d like to pre-install Vista updates and hotfixes while Vista is installing:

  1. Go to your Distribution Share (C:\Distribution)
  2. Go into Operating Systems, then find your Vista OS (C:\Distribution\Operating Systems\Windows Vista Business SP1 &#8211; 32bit\)
  3. Create a new folder in this directory called &#8220;update&#8221;
  4. Copy all of your Vista Update files (.msu) into this directory
  5. That&#8217;s it 🙂 The next time you run a Vista deployment, the updates will be pre-installed!

<div>
  The same concept applies to installing from a Vista DVD.
</div>

## Extra tip

<div>
  If you&#8217;d like a list of updates released since Vista SP1, check out this site: <a href="http://aaron-kelley.net/downloads/hotfix/">http://aaron-kelley.net/downloads/hotfix/</a>
</div>
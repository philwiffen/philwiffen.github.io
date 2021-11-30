---
id: 12
title: Asus W3V won’t resume from Hibernate
date: 2006-05-08T09:46:53+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://kabri.uk/?p=12
permalink: /2006/05/08/asus-w3v-wont-resume-from-hibernate/
categories:
  - Device Drivers
  - Hardware
  - Windows
---
Problem: After installing Hardware drivers from Windows Update I found my W3V would not boot up from a hibernated state. The progress bar appears to finish, but windows never loads the GUI.

Solution: Turns out, the LAN drivers Windows Update installs mess with the power management features on the W3V, preventing it from successfully booting from a hibernated state. You should re-install the Asus LAN Drivers from here: <http://support.asus.com/download/download.aspx?SLanguage=en-us>
---
id: 203
title: Automatically download every hotfix released for Windows XP since SP2
date: 2008-01-23T23:07:42+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2008/01/23/automatically-download-every-hotfix-released-for-windows-xp-since-sp2/
permalink: /2008/01/23/automatically-download-every-hotfix-released-for-windows-xp-since-sp2/
ratings_users:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
ratings_score:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
ratings_average:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
categories:
  - General IT
  - Time Saving
  - Windows
tags:
  - hotfix
  - integration
  - sp2
  - windows xp
---
![Automatically downloading hotfixes since XP SP2](http://www.kabri.uk/wp-content/uploads/2008/01/2008-01-23_213028-2.png "Automatically download every post Windows XP SP2 hotfix")

To automatically download every hotfix released for Windows XP post Service Pack 2, just [run this script](http://smithii.com/files/xpsp2local.cmd). [[Source site](http://smithii.com/slipstream_xpsp2)]. 

You&#8217;ll probably want to drop [wget](http://users.ugent.be/~bpuype/wget/#download) into your system32 directory before running the command, otherwise it&#8217;ll try to use your browser to individually download the files.

Once the script has finished, you can then integrate the hotfixes into your XP SP2 source and burn a bootable ISO using something like [nLite](http://www.nliteos.com/). I&#8217;ll cover more options for integrating hotfixes in a later post.

The reasons for wanting to integrate post-SP2 hotfixes are numerous; but mainly, it saves time (using both WSUS and Microsoft Update take a while), and, overall, makes for a cleaner install.

It took me ages to find this via Google, so much kudos to Ross Smith for creating such a useful script. Thanks Ross!
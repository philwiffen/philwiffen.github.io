---
id: 27
title: 'Windows XP won’t hibernate: Insufficient System Resources Exist to Complete the API'
date: 2007-02-22T12:59:09+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://kabri.uk/?p=27
permalink: /2007/02/22/windows-xp-wont-hibernate-insufficient-system-resources-exist-to-complete-the-api/
categories:
  - Operating Systems
  - Troubleshooting
  - Windows
---
After upgrading my laptop to 1.5GB of RAM, it began to frequently refuse to Hibernate, giving an error message in the system tray reading: &#8220;Insufficient System Resources Exist to Complete the API&#8221;.

Digging around, I found this [Microsoft Knowledgebase article](http://support.microsoft.com/kb/909095), along with a patch, which, insanely, isn&#8217;t available on Windows Update. Grr!

It seems the problem is caused due to the fact that when instructed to hibernate, XP has to find contiguous free space equal to the amount of RAM installed in the system. Naturally, as RAM increases, this becomes harder. Why on earth it&#8217;s incapable of using non-contiguous space is beyond me&#8230;but maybe that&#8217;s what the patch solves 🙂
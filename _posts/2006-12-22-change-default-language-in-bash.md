---
id: 18
title: Change default language in bash
date: 2006-12-22T13:03:48+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://kabri.uk/?p=18
permalink: /2006/12/22/change-default-language-in-bash/
categories:
  - Linux
---
To change the default language in the bash console (shell, terminal, command line &#8211; whatever you want to call it), go to your user home (e.g. /home/username/) edit or make a .bash_profile, and add this line to it:

export LANG=en

For some bizarre reason, our new dedicated server from 1and1 defaults to German feedback, which is really handy when you&#8217;re trying to work on the shell!

**Update &#8211; 2007-02-27**: If you have a 1and1 server stuck in German, this solution above doesn&#8217;t work properly (it breaks some stuff). I&#8217;ve written up a much [more elegant solution](/2007/02/27/1and1-dedicated-server-change-german-language-to-english/) which does actually work (thanks to Scott from [ART](http://www.atomicrocketturtle.com/)).
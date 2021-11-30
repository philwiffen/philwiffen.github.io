---
id: 28
title: '1and1 dedicated server: change German language to English'
date: 2007-02-27T10:54:30+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://kabri.uk/?p=28
permalink: /2007/02/27/1and1-dedicated-server-change-german-language-to-english/
categories:
  - Linux
---
Our 64-bit 1and1 Dedicated Server shipped with German as the default language on the CLI. Dead handy when you&#8217;re trying to troubleshoot&#8230;

<div class="highlight">
  See the comments section for a much more elegant solution to this problem.
</div>

I thought I&#8217;d found a solution by [changing the Bash language](/2006/12/22/change-default-language-in-bash/) but it broke some stuff (including yum) so I went back to the default and put up with it. By chance, whilst browsing around [atomicrocketturtle.com](http://www.atomicrocketturtle.com/), I found [Scott had fixed the same problem](http://www.atomicrocketturtle.com/Joomla/content/view/156/1/) _far_ more elegantly:

Here a quick step-by-step guide for FC4, on the 64-bit systems:

  1. Login as root (or su)
  2. Backup your yum.conf file: `cp /etc/yum.conf /etc/yum.conf.YYYY-MM-DD`
  3. Edit your /etc/yum.conf file
  4. Comment out the entries in your yum.conf which feature &#8216;update.onlinehome-server.info&#8217;. That server doesn&#8217;t work right now, and by commenting them out, yum will resort to the defaults in /etc/yum.repo.d
  5. Save yum.conf
  6. Run: `yum install system-config-language`
  7. You&#8217;ll be asked to confirm. Now, let it install&#8230;
  8. To change the language, run this from the command line: `system-config-language`
  9. Scroll up and choose English (British) (or whatever language you want).
 10. Hit the Tab key to switch to &#8220;OK&#8221;
 11. Hit return.
 12. Ta-da, English language feedback 🙂

For reference, your yum.conf should look something like this: [yum.conf.txt](/wp-content/uploads/2007/03/yumconf.txt "yum.conf.txt")
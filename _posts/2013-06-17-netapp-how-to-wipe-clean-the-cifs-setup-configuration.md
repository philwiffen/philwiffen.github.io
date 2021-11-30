---
id: 951
title: 'NetApp: How to wipe clean the cifs setup configuration'
date: 2013-06-17T17:49:52+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=951
permalink: /2013/06/17/netapp-how-to-wipe-clean-the-cifs-setup-configuration/
categories:
  - NetApp
---
Sometimes you need to completely wipe the &#8220;cifs setup&#8221; configuration. For example, I&#8217;m currently writing some documentation and need a clean cifs setup to start from scratch.

# Steps

> `cylon> cifs terminate<br />
cylon> priv set advanced<br />
cylon*> mv /etc/cifsconfig_setup.cfg /etc/cifsconfig_setup.cfg.bak<br />
cylon*> priv set<br />
cylon> cifs restart<br />
CIFS not configured. Use "cifs setup" to configure<br />
cylon> cifs setup`

I found the steps via a search on NetApp&#8217;s forums. Here&#8217;s the thread for more background: [How to Remove CIFS from a Filer?](https://communities.netapp.com/thread/23670)

User [aborzenkov](https://communities.netapp.com/people/aborzenkov)&#8216;s post has the answer I was looking for 🙂
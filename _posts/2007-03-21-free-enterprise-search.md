---
id: 33
title: Free Enterprise Search
date: 2007-03-21T12:35:46+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://kabri.uk/2007/03/21/free-enterprise-search/
permalink: /2007/03/21/free-enterprise-search/
ratings_score:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
ratings_users:
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
  - Business
  - General IT
  - Linux
  - Windows
---
If you follow this blog, you&#8217;ll know that I recently setup an Ubuntu box running Samba with [a 2.7TB Raid5 array](http://kabri.uk/2007/03/14/raid-5-in-ubuntu-with-mdadm/). Its job is to replace one of our 300GB Dell PowerVault 715N NAS boxes which has become full.

Finding files on our previous 300GB PowerVault was nothing short of a nightmare and, with such a vast amount of data on the new system, we have to ensure that information won&#8217;t get &#8216;lost&#8217; as easily. Obviously proper structuring of directories through a bit of Information Architecture will help, but what we really need is a search facility.

As a small company with a limited budget, the search facility has to be affordable. In addition, it needs to be easily accessible to everyone in the network, preferably without installing extra applications onto client systems&#8230;

<!--more-->

After a bit of digging around, and discounting the costly Google Appliance and Google Desktop Enterprise (Unfortunately, we don&#8217;t run an Active Directory network), I stumbled across [IBM&#8217;s OmniFind Yahoo! Edition](http://omnifind.ibm.yahoo.net/). It&#8217;s a free edition of their OmniFind software &#8211; which retails for thousands of dollars &#8211; and installs on both Linux (with a GUI) and Windows. Key features for us are that:

  1. It&#8217;s free.
  2. It&#8217;s simple to setup.
  3. It provides a search interface to users through a browser. (http://hostname:8080/)

As my Ubuntu system is purely command line, OmniFind wouldn&#8217;t install, so I&#8217;ll be reusing the old 300GB PowerVault that this 2.7TB Linux system will replace. I&#8217;m playing with it right now and it&#8217;s incredibly easy to use. Setting up indexing is a doddle and there&#8217;s plenty of customisation options for the web interface that users will see when searching, including:

  * Logo replacement, allowing you to re-inforce corporate branding.
  * Featured links, drawing attention to essential information.
  * Ranking modification

Once it&#8217;s indexed all of our data, I&#8217;ll play with it, see how it performs, and update the blog 😀
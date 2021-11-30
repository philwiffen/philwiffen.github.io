---
id: 79
title: 'Windows XP: Missing Authentication tab'
date: 2007-05-17T14:32:59+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/05/17/windows-xp-missing-authentication-tab/
permalink: /2007/05/17/windows-xp-missing-authentication-tab/
categories:
  - Networking
  - Troubleshooting
  - Windows
---
If you&#8217;re setting up 802.1x on your Network connection but can&#8217;t see the Authentication tab, make sure the &#8220;Wireless Zero Configuration&#8221; service is running.

  1. Start > Run&#8230; > <kbd>services.msc</kbd>
  2. Find the Wireless Zero Configuration service.
  3. Right click on it, and choose &#8220;Start&#8221;.

The Authentication tab will then appear on your Network connection properties.

Yes, I know. But apparently, to get 802.1x support, you need to enable a Wireless service, even though you may well be using it on a wired connection. Intuitive, eh?
---
id: 17
title: 'Apache &#8211; Redirect all requests to a single page'
date: 2006-12-18T18:03:28+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://kabri.uk/?p=17
permalink: /2006/12/18/apache-redirect-all-requests-to-a-single-page/
categories:
  - Apache
  - Linux
---
We&#8217;re migrating servers at work, and I needed to show a single &#8220;We&#8217;re moving&#8221; page no matter what URL was requested. Here&#8217;s how to do it permanently, and temporarily:

> `RedirectMatch permanent .*       http://yoursite.com/migration.html`

> `RedirectMatch temp .*       http://yoursite.com/migration.html`

Make sure you point to a different domain than the one you&#8217;re migrating! 😉
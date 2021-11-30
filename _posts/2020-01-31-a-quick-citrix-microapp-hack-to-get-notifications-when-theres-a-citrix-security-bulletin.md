---
id: 1732
title: 'A quick Citrix microapp hack to get notifications when there&#8217;s a Citrix Security Bulletin'
date: 2020-01-31T17:16:26+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: https://kabri.uk/?p=1732
permalink: /2020/01/31/a-quick-citrix-microapp-hack-to-get-notifications-when-theres-a-citrix-security-bulletin/
categories:
  - Citrix
  - Security
---
> Credit to [Gabe Carrejo](https://twitter.com/CitrixGabe) and the Patrick Quinlan for their work on this.

It&#8217;s possible to use the Citrix Support Security Bulletin RSS feed with Citrix microapps to notify you (or a group) when there&#8217;s a new Security Bulletin from Citrix

[<img loading="lazy" class="alignnone size-large wp-image-1739" src="https://kabri.uk/wp-content/uploads/2020/01/security-bulletin-feed2-1-1024x351.png" alt="" width="640" height="219" />](https://kabri.uk/wp-content/uploads/2020/01/security-bulletin-feed2-1.png)

Rough Steps:

  1. Copy this RSS URL: <https://support.citrix.com/feed/products/all/securitybulletins.rss>
  2. If you want to narrow the feed down to a specific product or category, look for the category tags in the RSS feed and add them when you add the RSS integration in step 3 
      * Some examples, in case they help: <pre class="">access-gateway
citrix-adc
citrix-gateway
citrix-sd-wan-wanop
netscaler</pre>

  3. Follow the RSS microapp guide here and replace the blogs RSS URL with the Security Bulletin URL: <https://kabri.uk/2019/12/18/building-a-simple-citrix-microapp-that-shows-blog-posts-from-a-wordpress-rss-feed/>

Of course, you don&#8217;t need to use microapps to get Security Bulletins (you could just use an RSS reader) but it&#8217;s a very neat use case &#8211; and combined with Push Notification with Workspace, means you get a notification to your phone when there&#8217;s a new Bulletin. Great idea, Gabe!

A full list of feeds available from Citrix Support are here: <https://support.citrix.com/feeds>
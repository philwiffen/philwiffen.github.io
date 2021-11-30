---
id: 120
title: Log rotation on Plesk 8
date: 2007-08-08T12:17:54+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/08/08/log-rotation-on-plesk-8/
permalink: /2007/08/08/log-rotation-on-plesk-8/
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
  - Apache
  - Linux
---
A few of our websites receive high traffic and, as a result, the apache log files grow very large, very quickly. By default, Plesk rotates logs every 2,025,139 KB (2GB). This is way too large for a virtualised server such as ours, which provides 10GB of precious disk space. 

To combat this, I set up a regular log rotation in Plesk like so:

  * Log in to Plesk.
  * Domains > yourdomain.com > Log Manager > Log Rotation
  * Choose the log rotation condition.

[![Plesk log rotation](http://www.kabri.uk/wp-content/uploads/2007/08/2007-08-08_115759.thumbnail.png)](http://www.kabri.uk/wp-content/uploads/2007/08/2007-08-08_115759.png "Plesk log rotation")

I choose monthly, but if you&#8217;re rapidly running out of disk space you might want to set a shorter time span, or set a low size limit. Don&#8217;t forget to enable compression to save on disk space!
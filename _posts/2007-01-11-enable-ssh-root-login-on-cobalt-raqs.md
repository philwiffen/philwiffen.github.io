---
id: 21
title: Enable ssh root login on Cobalt RAQs
date: 2007-01-11T12:06:58+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://kabri.uk/?p=21
permalink: /2007/01/11/enable-ssh-root-login-on-cobalt-raqs/
categories:
  - Linux
---
To enable root logins via SSH on a Cobalt RAQ, edit /etc/ssh/sshd_config and change &#8220;PermitRootLogin&#8221; to &#8220;yes&#8221;.

I needed to do this to allow Plesk to login to our old servers during the big migration, as it can&#8217;t login as admin, then su to root 🙁
---
id: 240
title: Control user access to SSH
date: 2008-03-19T15:25:38+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2008/03/19/control-user-access-to-ssh/
permalink: /2008/03/19/control-user-access-to-ssh/
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
  - Linux
tags:
  - Linux
  - ssh
---
Got a shiny new Linux box on your network but don&#8217;t want all your users connecting to it via SSH? Control access by editing the SSH configuration file and using the AllowUsers directive like so:

    AllowUsers joeuser
    

To add multiple entries, either separate users with a space, or write an entirely new line:

    AllowUsers joeuser philwiffen
    

    AllowUsers joeuser
    AllowUsers philwiffen
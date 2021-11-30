---
id: 666
title: Got problems deploying .Net Framework 4.0 on MDT 2010?
date: 2011-03-24T11:13:41+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=666
permalink: /2011/03/24/got-problems-deploying-net-framework-4-0-on-mdt-2010/
categories:
  - Desktop Deployment
---
Recently I&#8217;ve been having really weird issues getting the Microsoft .Net Framework 4.0 to be deployed as an Application via Microsoft Deployment Toolkit.

It would install perfectly if I installed it as a local admin user with the /q /norestart command, but doing the same thing through MDT resulted in the app hanging (and thus, the entire deployment).

After a quick search, it seems I&#8217;m not alone. Check out this [thread on Technet](http://social.technet.microsoft.com/Forums/en-US/mdt/thread/d71e088e-f7b8-41fe-80f3-ccba0e8173ea/) for how to solve it! 😀
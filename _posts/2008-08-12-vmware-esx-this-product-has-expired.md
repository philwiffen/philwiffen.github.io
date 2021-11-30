---
id: 348
title: 'VMware ESX: This product has expired'
date: 2008-08-12T18:48:57+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=348
permalink: /2008/08/12/vmware-esx-this-product-has-expired/
categories:
  - Virtualisation
tags:
  - esx 3.5
  - Virtualisation
  - vmware
  - vmware esx
---
If you find you can&#8217;t Power On a virtual machine on ESX 3.5, and you&#8217;re seeing this in your error logs:

Message from esxserver.yourdomain.com: This product has expired. Be sure that your host machine&#8217;s date and time are set correctly. There is a more recent version available at the VMware Web site: &#8220;http://www.vmware.com/info?id=4&#8221;.

Then you can find the solution at [this blog](http://www.vmhero.com/2008/08/12/esx-product-has-expired/).

Thanks Todd, you just saved me from pulling an all-nighter. I thought I was going crazy!

**Update**: The first signs of this problem occuring are that, when you try to Power On a virtual machine, you get the error message: “A General System error occurred: Internal error”. After checking the Events log, you&#8217;ll see the more verbose error message earlier on in the post.
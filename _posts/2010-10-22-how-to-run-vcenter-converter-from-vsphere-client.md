---
id: 641
title: How to run vCenter Converter from vSphere Client
date: 2010-10-22T13:37:49+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=641
permalink: /2010/10/22/how-to-run-vcenter-converter-from-vsphere-client/
categories:
  - Miscellaneous
  - Virtualisation
tags:
  - converter
  - vcenter
  - vmware
  - vsphere
---
Yet another &#8220;not entirely obvious&#8221; VMware thing 🙂

If you want to use the VMware vCenter Converter from within the vSphere Client you need to:

  1. Install vCenter Converter on the vSphere vCenter Server (It&#8217;s an option on the vSphere vCenter installer)  
    [<img loading="lazy" class="alignnone size-full wp-image-648" title="vcenter converter -install" src="http://www.kabri.uk/wp-content/uploads/2010/10/vcenter-converter-install.png" alt="" width="300" height="231" />](http://www.kabri.uk/wp-content/uploads/2010/10/vcenter-converter-install.png)
  2. Now log onto your vSphere Client and go to: 
      1. Plugins > Manage Plugins > Install vCenter Converter Client
  3. Once installed, right click on any ESX host, or ESX Cluster and choose &#8220;Import Machine&#8230;&#8221; from the bottom of the context menu.  
    [<img loading="lazy" class="alignnone size-full wp-image-647" title="vcenter converter - import machine" src="http://www.kabri.uk/wp-content/uploads/2010/10/vcenter-converter-import-machine.png" alt="" width="298" height="77" />](http://www.kabri.uk/wp-content/uploads/2010/10/vcenter-converter-import-machine.png)
  4. That&#8217;s it. The vCenter Converter wizard will then pop up 🙂

Note: This is tested and working on VMware vSphere 4.1. Let us know how you get on with other versions of vSphere! 🙂
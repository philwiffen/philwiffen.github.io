---
id: 1089
title: Installing VMware ESXi 5.5 on the Gigabyte Brix
date: 2013-09-23T21:27:17+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=1089
permalink: /2013/09/23/installing-vmware-esxi-5-5-on-the-gigabyte-brix/
categories:
  - Gigabyte Brix
  - Home Lab
  - Virtualisation
tags:
  - Brix
  - ESXi
  - Gigabyte Brix
  - RTL8111E
  - RTL8168
  - vmware
---
# Scope

This article covers the steps required to install VMware ESXi 5.5 on the [Gigabyte Brix](http://www.amazon.co.uk/s/?_encoding=UTF8&camp=1634&creative=19450&linkCode=ur2&pageMinusResults=1&suo=1390854648867&tag=mincir0e-21&url=search-alias%3Daps#/ref=nb_sb_noss_1?url=search-alias%3Daps&field-keywords=gigabyte%20brix&sprefix=gigabyte+br%2Caps&rh=i%3Aaps%2Ck%3Agigabyte%20brix&sepatfbtf=true&tc=1390854652008), and a few other systems that use non-supported NICs that worked in ESXi 5.1.

<img loading="lazy" class="alignnone size-full wp-image-1098" alt="brix running esxi 5.5" src="http://www.kabri.uk/wp-content/uploads/2013/09/brix-running-esxi-55.jpg" width="542" height="300" /> 

<!--more-->

# Background

The driver for the Realtek RTL8111E gigabit NIC was included in the default ESXi 5.1 install ISO. Sadly, with the release of ESXi 5.5, the driver is no longer included, so we have to add it ourselves.

The good news is that this is fairly easy, and should also allow anyone with an RTL8111 NIC or a RTL8168 NIC to install VMware ESXi 5.5 successfully. I can confirm it works on the Gigabyte Brix.

# Pre-requisites

You will need [PowerCLI 5.5](https://my.vmware.com/web/vmware/details?downloadGroup=PCLI550&productId=352)

# Steps

Here&#8217;s what I did, using PowerCLI:

<pre>Add-EsxSoftwareDepot https://hostupdate.vmware.com/software/VUM/PRODUCTION/main/vmw-depot-index.xml
New-EsxImageProfile -CloneProfile "ESXi-5.5.0-1331820-standard" -name "ESXi-5.5.0-1331820-GigabyteBrix" -Vendor "TwistedEthics.com"
Add-EsxSoftwarePackage -ImageProfile "ESXi-5.5.0-1331820-GigabyteBrix" -SoftwarePackage "net-r8168"
Export-ESXImageProfile -ImageProfile "ESXi-5.5.0-1331820-GigabyteBrix" -ExportToISO -filepath C:\Users\Phil\Downloads\ESXi-5.5.0-1331820-GigabyteBrix.iso</pre>

Note, you may need to run this command from PowerCLI before running the above (Thanks to Tom for mentioning this in the comments!):

<pre>Add-PSSnapin VMware.ImageBuilder</pre>

> Per Andreas Peetz&#8217;s excellent [post on upgrading](http://www.v-front.de/2013/09/how-to-update-your-standalone-host-to.html), there may be other non-supported driver bundles you&#8217;d like to install in addition to net-r8168, though I have not tested these:
> 
>   * net-r8169
>   * net-sky2
>   * net-s2io
> 
> Update 2013-09-24: Andreas just released a new post that [covers adding support](http://www.v-front.de/2013/09/how-to-add-missing-esxi-50-drivers-to.html) for all the missing unsupported drivers.

After running the commands above PowerCLI will start downloading the offline bundle from VMware.com and then write the ISO file to your selected destination.

Next, I used Unetbootin to write that ISO file to a USB stick, and then booted from the USB stick to install ESXi 5.5.

# What did those PowerCLI commands do?

Here&#8217;s roughly what you just ran:

  1. Add VMware&#8217;s repository
  2. Make a copy of the image called ESXi-5.5.0-1331820-standard and clone that to a new image called ESXi-5.5.0-1331820-GigabyteBrix
  3. Add the net-r8168 driver, which is stilll on VMware&#8217;s servers, but not in the standard ESXi 5.5 install.
  4. Export the custom image to an ISO file

# Bootnote

This took me quite a while to research, as I had no idea at the time that the r8168 driver provided the RTL8111E driver too (and I had no way to double-check as my Brix was at home :)). Fortunately, VMware still seem to provide the net-r8168 VIB on their repository, so while it&#8217;s easy to fix, it&#8217;s a shame that VMware have removed the driver in 5.5.

&nbsp;
---
id: 1043
title: 'Virtualization Home Lab: Setting up VMware ESXi on the Gigabyte Brix'
date: 2013-09-20T13:01:07+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=1043
permalink: /2013/09/20/setting-up-vmware-esxi-on-the-gigabyte-brix/
categories:
  - Gigabyte Brix
  - Home Lab
  - Virtualisation
tags:
  - Brix
  - ESXi
  - Gigabyte Brix
  - Home Lab
  - Virtualisation
  - Virtualization
---
<span style="color: #999999;">2013-09-23 00:27: Added information about ESXi 5.5 not including RTL8111E support</span>  
<span style="color: #999999;">2013-09-23 22:23: Added a link to <a title="Installing VMware ESXi 5.5 on the Gigabyte Brix" href="http://www.kabri.uk/2013/09/23/installing-vmware-esxi-5-5-on-the-gigabyte-brix/"><span style="color: #999999;">installing ESXi 5.5</span></a> with RTL8111E support</span>

In my [last post](http://www.kabri.uk/2013/09/19/virtualization-home-lab-choosing-a-quiet-low-power-computer-with-nested-virtualization-support/), I covered my journey of finding a small, quiet, low-power virtualisation lab computer that can run nested virtualisation.

# The final system

To summarise, here&#8217;s the system I ended up with, after much consideration:

  * Gigabyte Brix, Core i5 barebones kit (GB-XM11-3337) [[Buy in the UK]](http://www.amazon.co.uk/gp/product/B00CUZPNHS/ref=as_li_ss_tl?ie=UTF8&camp=1634&creative=19450&tag=mincir0e-21&creativeASIN=B00CUZPNHS&linkCode=as2)
  * 16GB (2x8GB) SO-DIMM Crucial RAM
  * Plextor M5M 256GB SSD [[Buy in the UK](http://www.amazon.co.uk/gp/product/B00B5KGGZ2/ref=as_li_ss_tl?ie=UTF8&camp=1634&creative=19450&creativeASIN=B00B5KGGZ2&linkCode=as2&tag=mincir0e-21)]

<img loading="lazy" class="alignnone  wp-image-1070" alt="brix vs xbox controller" src="http://www.kabri.uk/wp-content/uploads/2013/09/brix-vs-xbox-controller.jpg" width="381" height="192" /> 

<!--more-->

Total cost was roughly £575 ($920), but if you opt for a more modest Core i3 with 8GB RAM and a 128GB SSD you can make it as little as £370 ($600), which is much more palatable. Here&#8217;s a [rough shopping list](http://www.kabri.uk/2013/09/19/virtualization-home-lab-choosing-a-quiet-low-power-computer-with-nested-virtualization-support/#shoppinglist "Virtualization Home Lab: Choosing a suitable computer (quiet, low power with nested virtualization support)").

Power consumption idles around 12 watts running VMware ESXi 5.1 and I&#8217;ve seen it go up to 25 watts when I was loading it pretty hard with Turbo Boost at full pelt and the SSD being written to constantly.

I chose a higher-spec, more expensive system than I normally would, as I wanted to run an entire Nested Virtualization lab inside it including:

  * Multiple ESXi hypervisors, to emulate a cluster
  * Virtual router and virtual NAS to provide networking capabilities and shared storage inside the nested lab.
  * Multiple &#8220;Infrastructure&#8221; Virtual machines such as Active Directory, vCenter and vCloud
  * Multiple Hyper-V hypervisors to play with Microsoft&#8217;s offerings

[Read more on nested virtualisation](http://www.kabri.uk/2013/09/19/virtualization-home-lab-choosing-a-quiet-low-power-computer-with-nested-virtualization-support/#whynested).

The Brix GB-XM11-3337 I opted for has an Intel Core i5-3337U 1.8GHz processor with Turbo Boost which supports both Intel VT-x with EPT (Extended Page Tables) for Nested Virtualization and VT-d for directly passing through connected hardware to a VM running on the ESXi hypervisor (The Core i3 doesn&#8217;t support VT-d, so bear that in mind if you fancy it).

In addition, the Gigabit NIC is a Realtek RTL8111E which works out of the box with a standard VMware ESXi 5.1 install. For me, this makes it more attractive than the Intel NUC, which needs some hackery to get the [driver installed](http://www.tekhead.org/blog/2013/01/nanolab-running-vmware-vsphere-on-intel-nuc-part-2-2/). <span style="color: #999999;">I&#8217;m not lazy; I&#8217;m efficient 😉</span>

<img loading="lazy" class="alignnone size-full wp-image-1076" alt="brix rear port connectivity" src="http://www.kabri.uk/wp-content/uploads/2013/09/brix-rear-port-connectivity.jpg" width="556" height="212" /> 

# Putting it together

This is what I love about these barebones systems; they take minutes to put together. The RAM slots in exactly like a laptop, and the mSATA drive is easy to install. Gigabyte even include a screw for you to screw down the mSATA drive after installing it (just make sure to unscrew it before you install the mSATA drive!)

<img loading="lazy" class="alignnone size-full wp-image-1045" alt="mSATA screw" src="http://www.kabri.uk/wp-content/uploads/2013/09/WP_20130916_001.jpg" width="400" height="338" /> 

# Configuration

Now everything&#8217;s installed, let&#8217;s tweak the configuration before installing ESXi.

You&#8217;ll need:

  * A USB keyboard
  * Either a TV or Monitor capable of taking a HDMI source, or a DisplayPort monitor.

I&#8217;ve been struggling to get the Mini-DP port to play nicely with my Dell U2412m, so I&#8217;ve resorted to using my HDMI TV for configuration.

<span style="color: #808080;">Update: I&#8217;ve since found that a <a href="http://www.amazon.co.uk/gp/product/B004S4R5CK/ref=as_li_ss_tl?ie=UTF8&camp=1634&creative=19450&creativeASIN=B004S4R5CK&linkCode=as2&tag=mincir0e-21"><span style="color: #808080;">HDMI to DVI converter</span></a> works well with my monitor. Mini-DP is still troublesome.</span>

## BIOS settings

  * Enable Virtualization
  * If you want lower idle and standby power usage, enable Erp. This does mean you won&#8217;t be able to use [Wake-on-LAN](http://www.kabri.uk/2013/09/15/how-to-boot-the-gigabyte-brix-with-wake-on-lan/ "How to boot the Gigabyte Brix with Wake-On-LAN"), however.

## Upgrade the Plextor M5M SSD firmware

The SSD arrived with Firmware version 1.02. This version appeared to have a power usage issue, which was [picked up in the Anandtech review](http://www.anandtech.com/show/6722/plextor-m5m-256gb-msata-review/8), but their testing method wasn&#8217;t 100% sound due to not being able to accurately measure the 3.3v rail. Either way, version 1.03 says it fixes a power consumption issue, so let&#8217;s upgrade the SSD.

As the Brix doesn&#8217;t have a DVD drive, we need to convert the ISO provided by Plextor to a bootable USB stick. Fortunately, Unetbootin does a great job of this:

  1. Download the [latest version of the firmware](http://www.plextoramericas.com/index.php/download?task=viewcategory&catid=171) in ISO format
  2. Download [Unetbootin](http://unetbootin.sourceforge.net/)
  3. Write the ISO to a USB stick using Unetbootin
  4. Boot the Brix from the USB stick, and at the Unetbootin boot menu, choose the second boot option (the one immediately below Default).
  5. Follow the instructions to update the firmware. It&#8217;s very quick.

# Installing ESXi

This is trivial, as all the components in the Gigabyte Brix are compatible with VMware ESXi 5.1 (woohoo):

  1. First you need to get the ESXi 5.1 ISO. You can [get the Free Edition](www.vmware.com/go/get-free-esxi) from VMware. 
      * Note: Unlike ESXi 5.1, ESXi 5.5 doesn&#8217;t support the RTL8111E NIC out of the box. I&#8217;ve documented [how to get ESXi 5.5 to install on the Brix](http://www.kabri.uk/2013/09/23/installing-vmware-esxi-5-5-on-the-gigabyte-brix/ "Installing VMware ESXi 5.5 on the Gigabyte Brix")
  2. <span style="line-height: 1.714285714; font-size: 1rem;">Download </span><a style="line-height: 1.714285714; font-size: 1rem;" href="http://unetbootin.sourceforge.net/">Unetbootin</a>, if you don&#8217;t have it already.
  3. Use Unetbootin and a spare USB stick to create a bootable USB stick from the ISO you just downloaded. Anything bigger than 1GB is fine.
  4. Boot the Brix from the USB stick
  5. Install ESXi

Note: If you want to install ESXi to the same USB stick you booted from, you can. The install files are in RAM, so you won&#8217;t saw off the branch you&#8217;re standing on 🙂 Running ESXi on a USB stick is perfectly fine in a lab and as far as I&#8217;m aware won&#8217;t degrade performance while it&#8217;s running as the OS is loaded into RAM.  If you don&#8217;t want to run it off the USB stick (it does look a bit untidy), install ESXi to the SSD.

That&#8217;s it! Easy-peasy 🙂

[<img loading="lazy" class="alignnone size-medium wp-image-1068" alt="Brix running ESXi" src="http://www.kabri.uk/wp-content/uploads/2013/09/Brix-running-ESXi-300x215.png" width="300" height="215" />](http://www.kabri.uk/wp-content/uploads/2013/09/Brix-running-ESXi.png)

My next post will cover Enabling and setting up Nested Hypervisors on ESXi

# Fancy Hyper-V instead of ESXi as your base hypervisor?

If you want to install Hyper-V on your Brix as your base hypervisor, check out Jeff Hicks&#8217; articles: [Mini Hyper-V: Setup](http://jdhitsolutions.com/blog/2013/09/mini-hyper-v-setup/)
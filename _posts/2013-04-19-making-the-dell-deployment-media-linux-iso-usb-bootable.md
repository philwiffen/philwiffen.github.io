---
id: 793
title: Making the Dell Deployment Media (Linux) ISO USB bootable
date: 2013-04-19T17:03:38+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=793
permalink: /2013/04/19/making-the-dell-deployment-media-linux-iso-usb-bootable/
categories:
  - Server Management
---
# Scope

This page covers how to make a USB-bootable memory/flash stick from the Deployment Media (Linux) ISO created by [Dell Repository Manager](http://en.community.dell.com/techcenter/systems-management/w/wiki/1767.dell-repository-manager.aspx). You can then use this USB stick to quickly add new System Bundles for offline patching in the future, rather than needing to burn DVDs each time.

<h1 style="padding-left: 30px;">
  <img loading="lazy" class="alignnone size-full wp-image-969" src="http://www.kabri.uk/wp-content/uploads/2013/04/dell-firmware-usb-boot-menu-screenshot-medium.png" alt="dell firmware usb boot menu screenshot- medium" width="432" height="150" />
</h1>

There are two steps to this process:

  1. Create the bootable USB stick (This page)
  2. [Maintaining the USB stick with the latest Dell Firmware and BIOS updates](/2013/04/23/maintaining-a-bootable-usb-stick-with-the-latest-dell-firmware-and-bios-updates/)

# Why would you want this?

Having a USB-bootable version of the offline Dell firmware updater is incredibly useful. Here&#8217;s why I made it:

  * I don&#8217;t need to burn DVDs anymore. 
      * If I need to put the latest Firmware or BIOS updates on to a Dell server, I simply drag and drop the exported system bundle from Dell Repository Manager onto the USB stick and plug it into the target server.
  * USB is universally available on most Dell Servers. 
      * Many of our old systems have CD-ROMs rather than DVD-ROMs, so burning a 2.6GB DVD is a no-go.
      * Many of our newer systems have no Disc-based device at all, so USB is the only option.

# Background

The Dell Deployment Media (Linux) ISO is a bit of a blunt tool, but it gets the job done in a situation where you cannot install [Dell SUU](http://en.community.dell.com/techcenter/systems-management/w/wiki/1764.openmanage-server-update-utility-suu.aspx) updates from an existing OS. An example is installing Dell firmware and BIOS updates onto a server running VMware ESXi. The Deployment Media boot disc/USB stick will run and try to install everything in the SUU bundle repository. It doesn&#8217;t inventory the system for installed devices and then only install relevant/applicable BIN files. This means that often you&#8217;ll see error messages that the package isn&#8217;t applicable or compatible, due to the specific device targeted by the BIN file not being present in the system. This is nothing to worry about.

# Prerequisites

  1. You&#8217;ll need to have used [Dell Repository Manager](http://en.community.dell.com/techcenter/systems-management/w/wiki/1767.dell-repository-manager.aspx) to create a Deployment Media ISO from repository system bundles.
  2. As at 2014-05-15, some DTK versions (710 &#8211; 730) of the Dell DTK break USB boot functionality (see comments). To work around this, you&#8217;ll need to do the following: 
    <li value="1">
      Use the latest <a href="ftp://ftp.us.dell.com/FOLDER02167186M/1/DTK_740.cab">DTK_740.cab</a>, which Dell have confirmed now works (see comments). You can get that by simply using DRM, no need to download directly, but I&#8217;ve linked to it anyway.
    </li>
    <li value="1">
      Alternatively, download either of the older <a href="ftp://ftp.dell.com/sysman/DTK_651.cab">DTK 651.cab </a> or <a href="ftp://ftp.us.dell.com/FOLDER00433543M/1/DTK_700.cab">DTK_700.cab</a> (both confirmed in the comments as working)
    </li>
    <li value="1">
      Put the .cab file in: %USERPROFILE%\AppData\Local\RepositoryManager\Payloads\
    </li>
    <li value="1">
      Delete any other DTK*.cab files in that directory (as newer ones will be used automatically by Dell Repository Manager)
    </li>
  3. Alternatively, you can download a generic ISO I prepared from here: [Download Generic LinuxIso.iso](https://mega.co.nz/#!VpZh2AqB!UZg3jzwIE8e4PCy9u-hqzUki0qk8c310mPZ_VqtIyVU) (226MB). It contains updates for PESC1435, but that can be deleted once on USB.
  4. You&#8217;ll need a USB stick with sufficient capacity. For example, if your Deployment Media ISO is 2.8GB (as some are), you&#8217;ll need a 4GB USB stick.

# Steps

## Obtain Unetbootin

<li value="1">
  Obtain <a href="http://unetbootin.sourceforge.net/">Unetbootin</a> for Windows
</li>
  1. Insert the USB stick. Be aware that it&#8217;ll be wiped!
  2. Run the Unetbootin exe you just downloaded

## Prepare the USB stick

From the Unetbootin interface:

<p style="padding-left: 30px;">
  <img loading="lazy" class="size-full wp-image-799 alignnone" src="http://www.kabri.uk/wp-content/uploads/2013/04/09-04-2013-15-34-10.png" alt="09-04-2013 15-34-10" width="539" height="396" />
</p>

<li value="1">
  Click on the DiskImage radio button
</li>
  1. Click on … and locate the linuxISO.iso file (or whatever your Deployment Media ISO is called)
  2. Choose your target USB stick. In this example, it&#8217;s F:\
  3. Hit OK.

Unetbootin will then prepare the USB stick:

<p style="padding-left: 30px;">
  <a href="http://www.kabri.uk/wp-content/uploads/2013/04/09-04-2013-15-35-17.png"><img loading="lazy" src="http://www.kabri.uk/wp-content/uploads/2013/04/09-04-2013-15-35-17.png" alt="09-04-2013 15-35-17" width="541" height="401" /></a>
</p>

Once complete, choose Exit. Do not reboot:

<p style="padding-left: 30px;">
  <a href="http://www.kabri.uk/wp-content/uploads/2013/04/09-04-2013-15-49-42.png"><img loading="lazy" src="http://www.kabri.uk/wp-content/uploads/2013/04/09-04-2013-15-49-42.png" alt="09-04-2013 15-49-42" width="534" height="394" /></a>
</p>

## Running the firmware/BIOS updates

<li value="1">
  Once complete, safely remove the USB stick from your system and insert it into your target system
</li>
  1. Power on your Dell server and press F11 to bring up the BIOS Boot Manager menu.
  2. Choose Hard Disk, and when the popup menu appears, choose the option relevant to your Flash/Memory/USB stick

<p style="padding-left: 30px;">
  <img loading="lazy" class="alignnone" src="http://www.kabri.uk/wp-content/uploads/2013/04/WP_20130409_007.jpg" alt="WP_20130409_007" width="430" height="200" />
</p>

<li value="4">
  At the boot prompt, scroll down and choose the item labelled &#8220;1&#8221;. It looks like if you leave it as Default, it&#8217;ll just cycle round in circles saying it&#8217;ll auto boot in 10 seconds. To fix that, see &#8220;Extra credit&#8221; at the bottom of the page.
</li>

<p style="padding-left: 30px;">
  <a href="http://www.kabri.uk/wp-content/uploads/2013/04/WP_20130409_009.jpg"><img loading="lazy" src="http://www.kabri.uk/wp-content/uploads/2013/04/WP_20130409_009.jpg" alt="WP_20130409_009" width="408" height="250" /></a>
</p>

<li value="5">
  If you only have one Update Bundle, the script will run straight away. If you have multiple bundles, it will prompt you which one to run
</li>

<p style="padding-left: 30px;">
  <img loading="lazy" class="size-full wp-image-798 alignnone" src="http://www.kabri.uk/wp-content/uploads/2013/04/WP_20130409_013.jpg" alt="WP_20130409_013" width="400" height="236" />
</p>

<li value="6">
  Note that it can take a long time for the updates to run, and all you&#8217;ll see during that time is a bunch of &#8220;dots&#8221; running across the screen.
</li>

<li value="7">
  Once complete, you&#8217;ll be prompted to reboot:
</li>

<p style="padding-left: 30px;">
  <a href="http://www.kabri.uk/wp-content/uploads/2013/04/WP_20130409_004.jpg"><img loading="lazy" src="http://www.kabri.uk/wp-content/uploads/2013/04/WP_20130409_004.jpg" alt="WP_20130409_004" width="400" height="304" /></a>
</p>

<li value="8">
  Reboot the system and remove the USB stick
</li>
  1. That&#8217;s it &#8211; you&#8217;re done! It can take a while to reboot, as BIOS upgrades occur after you&#8217;ve rebooted.

## Extra credit &#8211; Auto-booting the correct boot option

If you wish to make the USB stick boot by default to the &#8220;1&#8221; option:

<li value="1">
  Open up syslinux.cfg in Notepad from the root of the USB drive.
</li>
<li value="2">
  Add  the line: &#8220;menu DEFAULT&#8221; beneath the line &#8220;label ubnentry0&#8221;
</li>
<li value="4">
  Save the file.
</li>

Or, for super extra credit, simply replace the syslinux.cfg file with the one in this zip file:

[zip containing the syslinux.cfg file](http://www.kabri.uk/wp-content/uploads/2013/04/syslinux.zip)

File contents:

> \# modified by Phil Wiffen  
> \# <http://about.me/philwiffen>
> 
> default menu.c32  
> prompt 0  
> menu title Custom Dell USB Bootable Firmware Updater  
> timeout 100
> 
> label bootdfu  
> menu DEFAULT  
> menu label Boot Dell Firmware Updater  
> kernel /isolinux/SA.1  
> append initrd=/isolinux/SA.2 ramdisk\_size=229441 root=/dev/ram0 rw DEBUG=0 share\_type=cdrom quiet loglevel=1 BUILD=668 vmalloc=256M init=/init mem=15G selinux=0 share\_script=drm\_files/apply_bundles.sh

# Next steps

Now you have a working USB-bootable offline firmware updater for Dell, you may want to check out my guide on how to keep it up to date with new Firmware/System Bundles: [Maintaining a bootable USB stick with the latest Dell Firmware and BIOS updates](/2013/04/23/maintaining-a-bootable-usb-stick-with-the-latest-dell-firmware-and-bios-updates/)
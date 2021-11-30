---
id: 835
title: Maintaining a bootable USB stick with the latest Dell Firmware and BIOS updates
date: 2013-04-23T19:55:38+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=835
permalink: /2013/04/23/maintaining-a-bootable-usb-stick-with-the-latest-dell-firmware-and-bios-updates/
categories:
  - Server Management
---
# Scope

This page covers how to maintain and update a bootable USB stick created to apply firmware and BIOS updates to a Dell Server.

This page is a follow on from my previous post: [Making the Dell Deployment Media (Linux) ISO USB bootable](http://www.kabri.uk/2013/04/19/making-the-dell-deployment-media-linux-iso-usb-bootable/ "Making the Dell Deployment Media (Linux) ISO USB bootable").

# Background

The problem with the Bootable ISO that Dell Repository Manager creates is that it&#8217;s a one-time thing. You export your SUU bundles to an ISO and burn it. The next time you need to update a bunch of servers, you download the latest system bundles, update your local SUU repository, and then export the system bundle packages to Bootable Media and burn a brand new ISO again.

Tedious.

Using the method below, you create a bootable USB stick once, and then simply add/update your SUU bundles as time goes on.

Simple 🙂

# Maintaining and updating the USB stick

## Pre-requisites

  * This page assumes that you&#8217;ve already setup a Repository in [Dell Repository Manager](http://en.community.dell.com/techcenter/systems-management/w/wiki/1767.dell-repository-manager.aspx).
  * You must have a USB stick that&#8217;s been prepared per the instructions in [Making the Dell Deployment Media (Linux) ISO USB bootable](http://www.kabri.uk/2013/04/19/making-the-dell-deployment-media-linux-iso-usb-bootable/ "Making the Dell Deployment Media (Linux) ISO USB bootable").

## Updating your repository with the latest System Bundles

<li value="1">
  Open up Dell Repository Manager (Data Center Version)
</li>
  1. Click on &#8220;My Repositories&#8221;, then double click on your repository
  2. Now that your repository is open, click Add

<p style="padding-left: 30px;">
   <img loading="lazy" class="alignnone size-full wp-image-836" alt="23-04-2013 16-15-18" src="http://www.kabri.uk/wp-content/uploads/2013/04/23-04-2013-16-15-18.png" width="283" height="161" />
</p>

<li value="4">
  Follow the Wizard, with the following guidance: <ol>
    <li>
      Choose: Import bundles from an existing repository
    </li>
    <li>
      Choose: Source Repository
    </li>
    <li>
      Uncheck: any brands or server types that you don&#8217;t need
    </li>
    <li>
      Choose: Linux
    </li>
    <li>
      Choose: Select Models, then control+click on the models you want to get system bundles for
    </li>
    <li>
      Choose: ONLY include the most recent and custom bundles.
    </li>
    <li>
      Click Finish at the end of the wizard
    </li>
  </ol>
</li>

<li value="5">
  Dell Repository Manager will then import the bundles you&#8217;ve specified. Click OK to go back to the main repository view.
</li>

## Exporting the latest System Bundles

Now that your repository has the latest system bundles, we need to export them into a format that&#8217;s compatible with the USB stick we currently have.

<li value="1">
  Check each System Bundle that you want to export, then click on Export
</li>

<p style="padding-left: 30px;">
   <img loading="lazy" class="alignnone size-full wp-image-839" alt="23-04-2013 16-22-24" src="http://www.kabri.uk/wp-content/uploads/2013/04/23-04-2013-16-22-24.png" width="657" height="232" />
</p>

<li value="2">
  Follow the Export Bundles wizard: <ol>
    <li value="1">
      Choose: Export to light weight deployment scripts
    </li>
    <li>
      Decide whether you want to force the scripts to apply the firmware/BIOS regardless of the version or date. This is only really desirable if you have a company standard and want to ensure that systems are at this standard regardless of whether the system has a newer firmware installed at present.
    </li>
    <li>
      Regarding the Combine option: Do not use this without checking out my notes at the bottom of the page.
    </li>
    <li>
      Choose a location to write the export to. Note that it&#8217;ll create its own sub-folder so don&#8217;t worry about specifying your Desktop.
    </li>
    <li>
      Once you&#8217;re happy with the summary, click Finish and the System Bundles will be exported. This can take a while, as often the bundles need to be downloaded before they can be exported. You can prevent this happening every time you export by choosing to Save your repository
    </li>
  </ol>
</li>

##  Copying the new System Bundles to the USB stick

<li value="1">
  Navigate to where you exported the System Bundles in the previous section and go inside the folder named LightScripts_*, where * is the date and time of the export.
</li>
<li value="2">
  Inside this folder you&#8217;ll see a list of System Bundles that you exported. For example:
</li>

<p style="padding-left: 30px;">
   <img loading="lazy" alt="23-04-2013 16-52-41" src="http://www.kabri.uk/wp-content/uploads/2013/04/23-04-2013-16-52-41.png" width="250" height="178" />
</p>

<li value="3">
  Next, take a look at your existing USB stick. In my example, I have a USB stick mapped to drive F: and it&#8217;s called &#8220;SUUUPDATER&#8221;.
</li>
  1. Navigate to drm_files, then repository

<li value="5">
  Next, copy over the new System Bundle folders from the exported directory onto your USB stick in the drm_files\repository folder.
</li>

<li value="6">
  Safely eject your USB stick from the OS.
</li>

That&#8217;s it! You&#8217;ve just updated your SUU Updater USB stick. To install the updates, boot from the USB stick and choose the System Bundle you want to apply.

## A note on the &#8220;Combine&#8221; option

The combine bundles option is interesting. One of the big issues I have with Dell Repository Manager and the exports it produces is that it duplicates a lot of components (firmwares, etc). The duplicates happen because although many Dell platforms share common components, they are separate products as far as DRM is concerned.

I&#8217;m still experimenting with the Combine option and thinking about its pros and cons. Thoughts are below.

How it probably works:

The apply_bundles.sh script simply jumps to a subfolder and executes all the .sh files in a folder. If it jumps into a normal System Bundle, there&#8217;s only one .sh file in there, and it&#8217;s only applicable to the platform of the system bundle.

However, when you Combine bundles, you get a single folder with multiple .sh files in (one for each platform). I have a feeling that what will happen is, apply\_bundles.sh is invoked, and it then runs through all of the .sh files inside the Combined bundle directory. Normally, the apply\_components.sh file works by blindly running all the. bin files in the directory. It doesn&#8217;t do an inventory check beforehand, so the application of all the .bin files can be quite lengthy. Due to this process, if we run multiple apply\_component.sh files in the same directory, it&#8217;ll try to install the updates in the directory every single time. So if you have 6 apply\_component.sh files in the same folder, it&#8217;ll take 6 times as long to apply.

So using Combine is a compromise of Speed vs Capacity. If you have a tiny USB stick and lots of time to wait while 6 apply_component.sh scripts run, then go ahead. But if you&#8217;re short on time (like, in a short Outage Windows) and have the capacity on the USB stick, I wouldn&#8217;t use the Combine option.
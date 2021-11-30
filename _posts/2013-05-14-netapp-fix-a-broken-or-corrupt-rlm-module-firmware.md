---
id: 893
title: 'NetApp: Fix a broken or corrupt RLM module firmware'
date: 2013-05-14T18:46:47+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=893
permalink: /2013/05/14/netapp-fix-a-broken-or-corrupt-rlm-module-firmware/
categories:
  - NetApp
  - Storage
  - Troubleshooting
---
## Scope

This guide is written for fixing a corrupt or broken RLM firmware. It is applicable to both 4.x and 3.x versions of the RLM firmware. Although this may help with other corrupt or broken RLM issues, the most common error this fixes is

> `[rlm.firmware.update.failed:warning]: RLM firmware update failed, Error Flashing linux.` 

## <!--more-->

## Overview

  1. Boot the backup RLM firmware
  2. Grab RLM 3.1 from support.netapp.com
  3. Get RLM 3.1 onto the filer
  4. Force install RLM 3.1
  5. Reboot the RLM
  6. [Optional] Upgrade RLM to 4.1

## Instructions

First we need to boot the backup RLM firmware.

From the Filer:

> `rlm reboot backup`

Wait for the rlm to reboot with the backup RLM firmware. Check on progress by running:

> `rlm status`

Once the RLM is shown as online, we can continue

<p style="padding-left: 30px;">
   <img loading="lazy" class="alignnone size-full wp-image-905" alt="screenshot - rlm status after rebooting rlm module" src="http://www.kabri.uk/wp-content/uploads/2013/05/screenshot-rlm-status-after-rebooting-rlm-module1.png" width="584" height="545" />
</p>

Now we need to install the &#8220;hop&#8221; release of the RLM firmware, which is version 3.1.

We will force the install of 3.1 regardless of the current RLM module as it&#8217;s a perfect base-point for either sticking with 3.x or upgrading to 4.1. Note that 3.1 is a requirement before upgrading to 4.1.

> Note:
> 
> Forcing the install allows you to downgrade from a corrupt install of RLM 4.0. This is especially important if you&#8217;ve installed 4.1 from 3.0 and corrupted the RLM. If you see this error message when you upgrade from 3.0 to 4.1, you have a corrupt RLM:
> 
> [rlm.firmware.update.failed:warning]: RLM firmware update failed, Error Flashing linux.

&nbsp;

### Get the RLM firmware onto the filer

Download RLM 3.1 from the [NetApp Support Site](http://support.netapp.com/).

Rename the file to RLM_FW3.1.zip

Copy the RLM 3.1 image to the etc/software folder on the filer. I do this via Linux, but basically you need to get it into vol0/etc/software

Basic example from a Trusted Host:

> `cp ./NetApp/RLM_FW3.1.zip /net/<filer>/vol/vol0/etc/software/`

### Force install RLM 3.1 firmware

Check the software is seen on the filer, then force the install of 3.1.

From the filer console:

> `software list<br />
software install RLM_FW3.1.zip<br />
priv set advanced<br />
rlm update -f`

If the upgrade is successful, you should see:

<img loading="lazy" class="alignnone size-full wp-image-898" alt="screenshot - rlm status showing upgrade complete" src="http://www.kabri.uk/wp-content/uploads/2013/05/screenshot-rlm-status-showing-upgrade-complete.png" width="572" height="264" /> 

### Reboot the RLM

Reboot the RLM module by saying yes (y). Note that rebooting the RLM does not reboot your filer. It only reboots the RLM module.

### [Optional] Upgrade the RLM to v4.1

Next, if you wish to, you can upgrade to RLM 4.1.

After a few minutes, check and confirm that the RLM is back online and that it&#8217;s running 3.1:

> `rlm status`

Download the RLM 4.1 firmware from support.netapp.com and copy it to the filer.

Upgrade the RLM:

> `software list<br />
software install RLM_FW.zip<br />
priv set advanced<br />
rlm update -f<br />
` 

Reboot the RLM when prompted and check it&#8217;s OK:

> `rlm status`

That&#8217;s it! If you need to reconfigure RLM, type:

> `rlm setup`

## Source

The conceptual steps for this were gleaned from: [RLM update to version 4.0 fails after 27 minutes.](https://kb.netapp.com/support/index?page=content&id=2013638)
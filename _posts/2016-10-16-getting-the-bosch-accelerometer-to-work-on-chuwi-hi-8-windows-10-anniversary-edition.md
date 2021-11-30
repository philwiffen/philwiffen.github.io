---
id: 1470
title: Getting the Bosch Accelerometer to work on Chuwi Hi 8 Windows 10 Anniversary Edition
date: 2016-10-16T09:20:39+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://kabri.uk/?p=1470
permalink: /2016/10/16/getting-the-bosch-accelerometer-to-work-on-chuwi-hi-8-windows-10-anniversary-edition/
categories:
  - Miscellaneous
---
# The short version

If you get the error &#8220;Device cannot start&#8221; on your Bosch Accelerometer in Device Manager on a Chuwi Hi 8 after installing Windows 10 Anniversary Edition, try this:

  1. Get the [32-bit Hi 8 Pro and Vi 8 Pro drivers](http://forum.chuwi.com/thread-1157-1-1.html). Look for the text &#8220;Chuwi Hi8 Pro Dualboot driver_32bit download&#8221;
  2. Install the driver in the <span style="font-style: italic; font-family: 'MS Gothic'; font-size: 11.0pt;">??</span>-gravity folder
  3. Double-check that the driver didn&#8217;t get a &#8220;cannot start&#8221; error
  4. Reboot

This device may also be known as:

  * ACPI\VEN\_BOSC&DEV\_0200
  * ACPI\BOSC0200
  * BMA2x2

# The longer version

AKA, how to fix the rotation and orientation feature in Windows 10 Anniversary Edition on Chuwi Hi 8.

I recently wiped my Chuwi Hi 8 tablet so that I could install Windows 10 Anniversary Edition. AE won&#8217;t install via Windows Update, because it requires more disk space than is available on a dual-boot Chuwi Hi 8.

After grabbing the Drivers from the [official source](http://forum.chuwi.com/thread-138-1-1.html) and installing them, I had one &#8220;Unknown Device&#8221; in Device Manager with the Hardware ID BOSC0200. Eventually I managed to force install the G-SENSOR driver provided by Chuwi from the link above, but the device would never start, meaning the auto-rotation feature would never work.

This means that the Rotation/Orientation feature of Windows 10 won&#8217;t work. Your tablet will be stuck in Portrait mode unless you manually rotate it in the Settings > Display.

After a few days and many hours of trying to source a driver that would work, I finally discovered that if you download the Hi8 Pro model&#8217;s drivers labelled Driver: Chuwi Hi8 Pro Dualboot driver_32bit download&#8221; from [here](http://forum.chuwi.com/thread-1157-1-1.html), and install the driver that&#8217;s inside the folder ??-gravity&#8221; &#8211; it works!

<p style="margin: 0in;">
  <img loading="lazy" class="alignleft wp-image-1471 size-full" src="http://kabri.uk/wp-content/uploads/2016/10/chuwi-bosch-fix.png" alt="chuwi-bosch-fix" width="845" height="171" />
</p>
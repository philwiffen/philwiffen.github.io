---
id: 105
title: Securely Erasing Hard Drives
date: 2007-07-06T17:48:43+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/07/06/securely-erasing-hard-drives/
permalink: /2007/07/06/securely-erasing-hard-drives/
categories:
  - Security
---
Every once in a while I need to securely wipe a hard drive before it&#8217;s sold on. To do this I use [Darik&#8217;s Boot and Nuke](http://dban.sourceforge.net/). DBAN is a free, bootable application that allows you to securely erase a hard drive so that no one can recover any of the data that&#8217;s on it.

### Why should you use DBAN?

If you&#8217;re selling your hard drive on eBay, or anywhere else, it&#8217;s vital that the data is completely erased as many buyers are [scouring for personal data](http://www.techweb.com/wire/security/177105302) left on hard drives. A format using <kbd>fdisk</kbd> is not enough, as **a standard format only marks the data as erased** &#8211; it&#8217;s still there, it&#8217;s just been hidden from view; and by using [readily available tools](http://www.recuva.com/), it&#8217;s incredibly easy to un-hide that data and do whatever you want with it. Securely erasing data is especially important if your decommissioned hard drive has any sensitive data on it &#8211; and it&#8217;s safe to say that if you care about your privacy, or you&#8217;re running a business, [most data is sensitive!](http://www.theregister.co.uk/2005/04/07/hard_drive_with_police_info_sold_on_ebay/)

### Using DBAN

You can boot DBAN from a CD/DVD or a USB drive. Once it&#8217;s booted, simply choose a wipe method, and how many rounds of wiping you&#8217;d like to perform. From my research online, I&#8217;ve found that using a PRNG (Pseudo-Random Number Generation) wipe 8 times over, is the most secure for modern hard drives. Apparently the Guttman (35 round wipe) isn&#8217;t as effective on modern drives.

Here&#8217;s the basic steps you need:

  * Burn the .iso file to a CD (you can use something like [ImgBurn](http://www.imgburn.com/))
  * Boot up DBAN, and hit Enter to run in Interactive Mode.
  * Press the M Key to choose the Method: Scroll down to PRNG and hit Space.
  * Press the R Key to choose the Rounds: For high security we need 8 rounds, so replace 1 with 8.
  * Hit F10 to start, and wait until done.

[![Securely Erasing a Hard Drive with DBAN](http://www.kabri.uk/wp-content/uploads/2007/07/2007-07-09_100358.thumbnail.png)](http://www.kabri.uk/wp-content/uploads/2007/07/2007-07-09_100358.png "Securely Erasing a Hard Drive with DBAN")
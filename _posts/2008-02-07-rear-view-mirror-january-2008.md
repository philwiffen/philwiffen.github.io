---
id: 200
title: 'Rear View Mirror: January 2008'
date: 2008-02-07T23:50:56+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2008/02/07/whatchu-up-to-jan-2008/
permalink: /2008/02/07/rear-view-mirror-january-2008/
ratings_users:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
ratings_score:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
ratings_average:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
categories:
  - DisplayLink
  - General IT
tags:
  - DisplayLink
  - IT
  - work
---
Rear View Mirror is my attempt to create a monthly review of what I&#8217;ve been up to at work. While it&#8217;s useful for myself, I hope it&#8217;ll help create some useful conversations and maybe even some post requests for the blog 🙂

### January 2008

#### Streamlining PC deployments

**Working on centralising Microsoft Office control by leveraging Group Policy.**  
Deploying things like setting Free/Busy times, and Workgroup templates is easier than importing .reg files through AutoIT scripts! I bought a book &#8211; Group Policy: Management, Troubleshooting, and Security &#8211; to help me understand Group Policy. Even just casual browsing has turned up some useful pieces of info, and I&#8217;m looking forward to delving deeper into GP, and the book, as I get time 🙂

**Investigating Windows Desktop Deployment (formerly BDD 2007).**  
Again, the aim is to further streamline new PC deployments. It seems pretty complex on first look, but I&#8217;ve checked out a few videos &#8211; discussing BDD 2007 &#8211; by [IT Idiots](http://www.itidiots.com/) which have aided my understanding &#8211; I&#8217;ve even done a Lite touch deployment using WinPE. Kudos to them for providing such useful content!

**Moving the company to a Microsoft Volume Licence infrastructure.**  
We&#8217;re running at around 100 PCs now and up until January, had been operating on an OEM Licence infrastructure. I&#8217;d heard about the advantages of Volume Licensing, so began investigating how we can go about doing it. Understanding the myriad rules and options associated with Volume Licensing is a bit of a black art, but the process has been rewarding, and I&#8217;ve already started rolling out VLK Office and Windows deployments 🙂

**Unattended, Service Pack Slipstreamed, Windows and Office installers**  
Using [AutoIT](http://www.autoitscript.com/) and creating Unattended Install CDs for XP and Vista using [nLite](http://www.nliteos.com/) and vLite. I&#8217;ve also created an unattended, slipstreamed, install for Office 2003 using the Office 2003 Resource Kit. Next on my agenda is Office 2007! 

In combination with everything above, this should massively streamline PC deployments. Expect some posts on these strategies in the future, to see how you can speed up your own deployments.

#### IT Infrastructure planning and upgrades

Working with my colleague, Dave, to plan and upgrade our IT infrastructure, so that it can grow with the company. This includes general stuff like Network Attached Storage and deploying VMware ESX Server to better utilise hardware, rack space and power. Natural Business considerations were things like: How do we back it up? and How do we ensure the solutions are resilient enough to cope with failure and keep the business running?

We took delivery of some new kit towards the end of the month &#8211; after much planning and research!

**[HP DL320s NAS](http://h10010.www1.hp.com/wwpc/us/en/sm/WF05a/15351-15351-3328412-241644-241475-3232017.html)** &#8211; 6TB raw storage to, hopefully, meet our storage needs for the next year or so. Naturally, to comply with our objectives above, it runs RAID-6 and has redundant PSUs.

**[HP DL360](http://h10010.www1.hp.com/wwpc/us/en/sm/WF05a/15351-15351-3328412-241644-241475-1121486.html)** &#8211; with 4 x 10K 72GB SAS drives and 2 x quad core Xeons, for running VMware Infrastructure 3 /ESX 3.5. The DL360s come barebones so you have to install the extra processor/drives/redundant PSU/RAM yourself, but it was all easy as pie. The thing runs stupidly fast.

**[VMware Infrastructure 3 Foundation](http://www.vmware.com/products/vi/)** &#8211; we&#8217;ll be running this as a test platform to start with but I imagine (from my previous experience with Server and Workstation) that it&#8217;ll hit production with a month or so. The main purpose of this exercise is to consolidate older hardware and reduce both physical and energy footprints.

**Rackmount Tape Chassis plus drive** &#8211; 1U rackmount Tape Drive chassis, with 1 x [LTO-3](http://en.wikipedia.org/wiki/Linear_Tape-Open) drive installed and space for another. LTO-4 is still pretty expensive, so we went for a happy medium 🙂
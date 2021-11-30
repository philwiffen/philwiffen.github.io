---
id: 237
title: Slipstream Project 2003 SP3
date: 2008-03-17T19:10:00+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2008/03/17/slipstream-project-2003-sp3/
permalink: /2008/03/17/slipstream-project-2003-sp3/
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
  - General IT
  - Time Saving
  - Windows
tags:
  - office 2003
  - project
  - slipstream
  - sp3
---
### How to slipstream Service Pack 3 into Microsoft Office Project 2003

These instructions apply to Project 2003 Standard Edition. To slipstream other versions, you&#8217;ll need to replace `PRJSTDE.MSI` with the name of the MSI for your Project Edition.

#### Steps

You&#8217;ll need a Volume Licence Key setup CD.

    D:\setup.exe /a

Save to `C:\project2003\`

Download [Project 2003 SP3](http://download.microsoft.com/download/6/3/3/63322daa-64ba-4b94-8de8-6402f832aa94/Project2003SP3-KB923622-FullFile-ENU.exe)

Extract its contents to `C:\Project2003SP3\` with: 

    Project2003SP3-KB923622-FullFile-ENU.exe /Q /C /T:C:\Project2003SP3\

Perform slipstream with: 

    msiexec /p C:\Project2003SP3\PROJECTSP3.msp /a C:\Project2003\PRJSTDE.MSI SHORTFILENAMES=TRUE /qb

Delete the `C:\Project2003SP3\` folder as you no longer need it 🙂
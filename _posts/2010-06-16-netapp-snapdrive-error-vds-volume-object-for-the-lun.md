---
id: 625
title: 'NetApp SnapDrive Error: VDS volume object for the LUN'
date: 2010-06-16T14:55:15+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=625
permalink: /2010/06/16/netapp-snapdrive-error-vds-volume-object-for-the-lun/
categories:
  - Miscellaneous
tags:
  - netapp
  - SME
  - SnapDrive
---
Earlier today, I was trying  to set up a Remote Verification Server on NetApp SnapManager for Exchange 6.0, but came across this error when the remote verification server tried to mount the snapshot:

[SnapDrive Error]:VDS volume object for the LUN s/n &#8216;<serial>&#8217; has not been found

The error shows up in the Report that SME generates when it runs a snapshot/backup job.

To get around this error, install the latest (apparently not-quite-released-yet) SnapDrive on to your Verification Server. You can get it here: <http://now.netapp.com/NOW/download/software/snapdrive_win/6.2P1/>

This problem appears to happen on Server 2008 R2 servers, and I can confirm that installing the download above fixed the issues for me.

For the record, this is our configuration:

Exchange 2007 SP2 running on a Server 2008 SP2 box, with a Server 2008 R2 box set up for Remote Verification

The full thread discussing this is here: <http://communities.netapp.com/message/24568?tstart=-1>
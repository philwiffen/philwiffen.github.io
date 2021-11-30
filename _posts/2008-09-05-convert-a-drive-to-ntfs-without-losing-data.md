---
id: 379
title: Convert a drive to NTFS without losing data
date: 2008-09-05T14:00:19+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=379
permalink: /2008/09/05/convert-a-drive-to-ntfs-without-losing-data/
aktt_notify_twitter:
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
categories:
  - General IT
  - IT Pro Tools
tags:
  - ntfs
---
An oldie-but-goodie; Converting a drive to NTFS without losing data, provided you have enough free space, and an existing FAT32 partition. Probably works with FAT, too.

Run this from a command-line:

`convert <em>drive_letter:</em> /fs:ntfs`
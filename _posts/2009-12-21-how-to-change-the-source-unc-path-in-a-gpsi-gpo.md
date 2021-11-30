---
id: 579
title: How to change the source UNC path in a GPSI GPO
date: 2009-12-21T14:46:50+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=579
permalink: /2009/12/21/how-to-change-the-source-unc-path-in-a-gpsi-gpo/
categories:
  - Miscellaneous
tags:
  - GPO
  - gpsi
  - group policy
---
Some brief notes on how to change the source UNC path in a GPSI GPO

Instructions are for Server 2008.

Backup the GPO&#8230;

  1. Open up “Group Policy Management” console
  2. Find the GPO with the GPSI source UNC you’d like to change
  3. Right click it, choose “Backup”
  4. Back up the GPO a directory, eg C:\GPOs\

Now we need to edit the GPO and change the UNC&#8230;

  1. In the GPMC left-hand pane, click on Domains
  2. In the GPMC toolbar, click on Actions, then Open Migration Table Editor
  3. In the Migration Table Editor, click on “Tools” then “populate from Backup”
  4. Choose the backup you want to change
  5. In the Table Editor, change the Destination name to the new UNC path
  6. Now we need to save the migration table.
  7. Click File, Save.
  8. Save the file as something meaningful, preferably in C:\GPOs\

Now we need to apply the new settings&#8230;

  1. Go back to the Group Policy Management Console
  2. Find the GPO you need to change and Right-click on it
  3. Choose “Import Settings&#8230;”
  4. Click Next twice.
  5. Browse to your backup folder (C:\GPOs)
  6. Confirm the GPO backup whose settings you want to import, then click next.
  7. After the scan is complete, click Next
  8. Now we need to apply the Migration Table mapping: 
      1. Choose “Using this migration table&#8230;”
      2. Browse to your migration table settings that you saved earlier.
      3. Now click Next, and then Finish
      4. That’s it! 🙂
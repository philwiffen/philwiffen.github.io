---
id: 456
title: Automated Backups for MS SQL Express
date: 2008-11-06T10:31:23+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=456
permalink: /2008/11/06/automated-backups-for-ms-sql-express/
aktt_notify_twitter:
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
categories:
  - General IT
  - Time Saving
tags:
  - automation
  - backup
  - sql
  - sql express
---
If you&#8217;ve ever struggled with configuring automated, scheduled backups for a SQL Express server, then check out Brian Knight&#8217;s [super handy scripts](http://www.whiteknighttechnology.com/cs/blogs/brian_knight/archive/2006/08/13/215.aspx).

> The script contains three files:
> 
>   * BackupExpress.sql &#8211; Does the bulk of the work, backing up every database on the instance other than tempdb.
>   * BackupExpress.cmd &#8211; The batch file that executes the script. Must pass in the instance name.
>   * ScheduleBackups.cmd &#8211; Schedules the job by using AT. Must pass in the instance name to schedule like ScheduleBackups.cmd .\SQLExpress.
> 
> <p style="margin: 10px 0px;">
>   To do this, make sure you have the Task Scheduler service started. Uncompress all three of the files into the root of your C drive and run the schedule file from the command prompt.
> </p>
> 
> <p style="margin: 10px 0px;">
>   I tried to keep the solution simple since most people that have SQL Express on their workstation may not be technical. So with that said, there is very little configuration or options. The backup solution keeps 7 days of history and constantly overwrites the previous week&#8217;s backup.
> </p>

Grab the scripts from the [full blog post](http://www.whiteknighttechnology.com/cs/blogs/brian_knight/archive/2006/08/13/215.aspx).

Don&#8217;t forget to add the _Instance name_ of your SQL Express Server when you run ScheduleBackups.cmd from the command line, like so:

`</p>
<pre>ScheduleBackups.cmd MYSQLSERVER\SQLEXPRESS</pre>
<p>`
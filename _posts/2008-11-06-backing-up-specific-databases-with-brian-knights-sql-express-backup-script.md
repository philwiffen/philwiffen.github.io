---
id: 458
title: 'Backing up specific databases with Brian Knight&#8217;s SQL Express backup script'
date: 2008-11-06T11:29:14+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=458
permalink: /2008/11/06/backing-up-specific-databases-with-brian-knights-sql-express-backup-script/
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
categories:
  - Miscellaneous
tags:
  - backup
  - sql
  - sql express
---
Just a follow up to my previous post, covering the [Automation of SQL Express Backups](http://www.kabri.uk/2008/11/06/automated-backups-for-ms-sql-express/)&#8230;

As [Brian&#8217;s scripts](http://www.whiteknighttechnology.com/cs/blogs/brian_knight/archive/2006/08/13/215.aspx) are aimed at non-techies, he wisely coded them to backup all SQL databases on the host. If you&#8217;d prefer to back up just one specific SQL database, all you need to do is:

  1. Open up BackupExpress.sql in an editor.
  2. Find the line:  
    `</p>
<pre>select name from sysdatabases where name !='tempdb'</pre>
<p>` 
  3. Remove the exclamation mark, and replace tempdb with the name of your database, like so:  
    `</p>
<pre>select name from sysdatabases where name ='MyDatabase'</pre>
<p>` 

Nice and easy 🙂

If you&#8217;re wondering what the exclamation mark does, it means &#8220;exclude&#8221;. So Brian&#8217;s original script backed up every database except tempdb. By removing the exclamation mark, we&#8217;re explicitly choosing a database to backup, and excluding all others.
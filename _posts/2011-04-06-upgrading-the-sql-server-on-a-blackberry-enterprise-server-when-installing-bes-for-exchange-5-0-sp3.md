---
id: 698
title: Upgrading the SQL Server on a BlackBerry Enterprise Server when installing BES for Exchange 5.0 SP3
date: 2011-04-06T12:13:17+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=698
permalink: /2011/04/06/upgrading-the-sql-server-on-a-blackberry-enterprise-server-when-installing-bes-for-exchange-5-0-sp3/
categories:
  - BlackBerry
---
Bit of a long winded title, but this article will attempt to cover the steps you need to take in order to go from a Standalone BES server with the MSDE database to a supported SQL Server Express database; so that you can install BES for Exchange 5.0.3 (or 5.0 SP3). This is a quick and dirty post, so please excuse any typos!

Our situation was this:

  * BES 5.0.2 installed using the default MSDE database (we have less than 100 BES users, so this isn&#8217;t a problem).
  * When trying to install BES 5.0.3 upgrade, it failed, saying you need to upgrade the version of SQL you&#8217;re running before SP3 can be installed.

Here&#8217;s what you need to do in very basic terms:

  * Install a &#8220;New Installation&#8221; of SQL 2008 R2 Express with the management tools on to the BES Server (don&#8217;t try and do the upgrade like I did; it doesn&#8217;t do anything to MSDE ;))
  * Completely stop and disable all BlackBerry services under Administration Tools > Services
  * Open up the SQL Management Studio, connect to the existing MSDE instance, and perform a Full backup of the BESMgmt database to a file location.
  * Now, still in  SQL Management Studio, connect to the new database server instance (should be servername\sqlexpress) and perform a restore of the database you just backed up.
  * Open up the SQL Server Configuration Manager: 
      * Navigate to: SQL Server Network Configuration > Protocols for SQLEXPRESS
      * Enable TCP/IP
      * You may need to restart the SQL Service at this point.
  * Re-enable (but do not start) the BlackBerry services you stopped and disabled earlier.
  * Run the 5.0 SP3 installer, and point it at the new database instance. If you were using MSDE, you&#8217;ll need to change the connection port from the default to &#8220;Dynamic&#8221;.

Bootnotes:

When we first tried it, the installer threw an error at the last install step (after upgrading the DB). For whatever reason, rebooting and trying again fixed the issue and SP3 installed successfully.

In case you&#8217;re wondering, the reason for the full backup/restore step is because SQL express management tools wouldn&#8217;t let us move or copy the database. You may have better luck, however 🙂

Also note that, according to RIM&#8217;s [compatibility matrix](http://us.blackberry.com/support/software/server_compatibility.jsp#tab_tab_compatibility), SQL Express 2008 R2 isn&#8217;t supported for BES 5.0.3. You may wish to download and install SQL Express 2008 SP2  instead.
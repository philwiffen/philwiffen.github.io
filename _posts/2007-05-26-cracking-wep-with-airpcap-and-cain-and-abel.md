---
id: 80
title: Cracking WEP with AirPcap and Cain and Abel
date: 2007-05-26T22:15:22+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/05/26/cracking-wep-with-airpcap-and-cain-and-abel/
permalink: /2007/05/26/cracking-wep-with-airpcap-and-cain-and-abel/
enclosure:
  - |
    http://taz00.com/files/cain/cracking-wep-with-airpcap-packet-injection-and-cain-and-abel.wmv
    7149974
    video/x-ms-wmv
  - |
    http://taz00.com/files/cain/cracking-wep-with-airpcap-packet-injection-and-cain-and-abel.wmv
    7149974
    video/x-ms-wmv
  - |
    http://taz00.com/files/cain/cracking-wep-with-airpcap-packet-injection-and-cain-and-abel.wmv
    7149974
    video/x-ms-wmv
  - |
    http://taz00.com/files/cain/cracking-wep-with-airpcap-packet-injection-and-cain-and-abel.wmv
    7149974
    video/x-ms-wmv
  - |
    http://taz00.com/files/cain/cracking-wep-with-airpcap-packet-injection-and-cain-and-abel.wmv
    7149974
    video/x-ms-wmv
ratings_score:
  - "37"
  - "37"
  - "37"
  - "37"
  - "37"
ratings_users:
  - "8"
  - "8"
  - "8"
  - "8"
  - "8"
ratings_average:
  - "4.63"
  - "4.63"
  - "4.63"
  - "4.63"
  - "4.63"
categories:
  - Security
  - Wi-Fi
---
This video tutorial demonstrates how to crack WEP in Windows using AirPcap and Cain and Abel.

### Preparation

You&#8217;ll need:

  * An [AirPcap Tx adapter](http://www.crownhill.co.uk/product.php?prod=1779&ref=wireless-analysis)
  * [Cain and Abel](http://www.oxid.it/cain.html)

Note: It is possible to get this working by using the cheaper &#8220;Classic&#8221; AirPcap, in conjunction with the old [2.0 Beta Tx Drivers for AirPcap](http://rapidshare.com/files/29501895/setup_airpcap_2_0_beta_tx.exe.html), to enable packet injection capability, but this is entirely unsupported, and is not guaranteed to work. <acronym title="Your Mileage May Vary">YMMV</acronym>.

### Notes

  * To begin ARP injections, AirPcap must capture at least 1 ARP request from a system on the target AP. You can usually force this by sending a Deauth to a connected client.
  * Make sure you have over 250,000 IVs before attempting to crack the WEP key.
  * In my tests, the old AirPcap (silver-grey) appears to perform significantly faster than the new [AirPcap](http://www.crownhill.co.uk/product.php?prod=1779&ref=wireless-analysis) (dark-grey). I think it&#8217;s about 10x faster.

### The Video

**[MEDIA=2]**

Click Play to get things started.

#### Additional

[Download the full resolution video](http://taz00.com/files/cain/cracking-wep-with-airpcap-packet-injection-and-cain-and-abel.wmv) (Thanks to TAz00 from the [Oxid.it forums](http://oxid.netsons.org/phpBB2/) for the hosting!)

[View the video on Youtube](http://www.youtube.com/watch?v=GqleMWzSvUk)
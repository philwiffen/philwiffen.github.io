---
id: 68
title: How to Crack WEP in Windows with Aircrack-ng and AirPcap
date: 2007-05-04T19:09:56+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/05/04/how-to-crack-wep-in-windows-with-aircrack-ng-and-airpcap/
permalink: /2007/05/04/how-to-crack-wep-in-windows-with-aircrack-ng-and-airpcap/
ratings_users:
  - "4"
  - "4"
  - "4"
  - "4"
  - "4"
ratings_score:
  - "14"
  - "14"
  - "14"
  - "14"
  - "14"
ratings_average:
  - "3.5"
  - "3.5"
  - "3.5"
  - "3.5"
  - "3.5"
categories:
  - Security
  - Wi-Fi
  - Windows
---
This guide demonstrates how to crack WEP in Windows using the [AirPcap](http://www.wireless-analysis.co.uk/#airpcap) Wireless Capture Adapter. <!--more-->

To do this, you&#8217;ll need the useful [AirPcap USB Wireless Capture Adapter](http://www.crownhill.co.uk/product.php?prod=1779&ref=wireless-analysis) from CACE Technologies. It&#8217;s pretty cheap when compared to some of the other Windows hardware solutions, and you&#8217;ll be supporting the makers of [Wireshark](http://www.wireshark.org/)!

## Why Windows?

I adore Linux and the entire Open Source movement, but it&#8217;s important to recognise that many people out there are locked into Windows; and learning an entirely new OS to perform security testing isn&#8217;t cost-effective for their company.

## How is WEP cracked?

<noscript>
  null
</noscript>

  
To crack WEP, you need to exploit a weakness in its implementation, and collect lots of Initialisation Vectors (IVs). In normal WLAN traffic, it would take quite a while to pickup enough IVs &#8211; approximately 1 million &#8211; so we need to generate our own traffic. There&#8217;s two ways we could do this:

  1. Generate your own traffic using iperf.
  2. Use packet injection using aireplay.

<span style="text-decoration: line-through;">At present, the AirPcap Drivers do not support packet injection in Windows. Fortunately, the makers of AirPcap, CACE Technologies, have said packet injection will be included soon. 😀</span>

**Update 2007-06-11:** Packet Injection is now possible in Windows with the AirPcap. Please see my posts: [Cracking WEP with Cain](http://www.kabri.uk/2007/05/26/cracking-wep-with-airpcap-and-cain-and-abel/) and [Cracking WEP with aircrack-ptw](http://www.kabri.uk/2007/06/11/cracking-wep-with-aircrack-ptw-in-windows-with-airpcap-and-cain/) for more information.

## What will you need?

  * An [AirPcap Wireless Capture adapter](http://www.crownhill.co.uk/product.php?prod=1779&ref=wireless-analysis "View information about AirPcap"). This is a great little tool for 802.11 sniffing in Windows. You can even [run Kismet with it](http://www.kabri.uk/2007/04/12/kismet-on-windows-without-a-drone/ "Run Kismet in Windows with AirPcap")!
  * The [Aircrack-ng for AirPcap](http://www.kabri.uk/wp-content/uploads/2007/05/aircrack-ng-0_7_0_beta1-airpcap.zip "Aircrack-ng for AirPcap") release by CACE Technologies.
  * Your own Wireless Access Point, configured with WEP.
  * 3 computers, at least 1 of which should have a Wireless LAN Adapter.
  * Enough traffic to generate over 1 million IVs. For this demonstration, we&#8217;ll use a Windows release of iperf, called [K-perf](http://dast.nlanr.net/projects/Iperf2.0/kperf_setup.exe), to generate lots of traffic.

## Let&#8217;s get cracking

This guide assumes that you are performing this on a WLAN you have permission to use.

OK let&#8217;s do it&#8230;

### Set up Aircrack

Plug in your [AirPcap](http://www.crownhill.co.uk/product.php?prod=1779&ref=wireless-analysis).

Extract the contents of the aircrack-ng release to C:\aircrack (or wherever, I&#8217;m just doing this for tidiness).

Open up the c:\aircrack\bin\ directory and double-click the airodump-ng.exe (this is a specially built release tailored for AirPcap).

Configure it as per your settings [[Screenshot: Configuring Airodump-ng](http://www.kabri.uk/wp-content/uploads/2007/05/configure-airodump-ng.gif "Configuring Airodump-ng")]

### Generate some traffic

Install [K-perf](http://dast.nlanr.net/projects/Iperf2.0/kperf_setup.exe), then run J-perf â€” the Java front-end â€” on the two machines connected to the AP. At least one should be connected via Wireless. Set one up as a server, and the other as a client. Remember, we&#8217;re just doing this to generate enough traffic on our demo WLAN.

On the Server, choose the &#8216;Server&#8217; option, then click Run. [[Screenshot: Server, Configure K-perf using the Java front-end, J-perf.](http://www.kabri.uk/wp-content/uploads/2007/05/jperf-server.png "Server: Configure K-perf using the Java front-end, J-perf.")]

On the Client, type in the Server&#8217;s IP address, configure the time iperf should run to 1200, and click Run. [[Screenshot: Client, Configure K-perf](http://www.kabri.uk/wp-content/uploads/2007/05/jperf-client.png "Client: Configure K-perf")]

### Capture and Crack

Go back to your AirPcap machine and watch the IV frames come in. [[Screenshot: Airodump-ng capturing WEP IVs](http://www.kabri.uk/wp-content/uploads/2007/05/airodump-capturing-packets.gif "Airodump-ng capturing WEP IVs")]

When you&#8217;ve hit over 1,000,000 frames, open up aircrack-ng_GUI.exe in the c:\aircrack\bin\ directory.

Click the Aircrack-ng tab, and locate your crackme.iv file.

Click launch and wait for the cracker to find your WEP key. [[Screenshot: Airocrack-ng cracking WEP](http://www.kabri.uk/wp-content/uploads/2007/05/airocrack-cracking-wep-in-windows.gif "Airocrack-ng cracking WEP")]

If aircrack cannot find your WEP key, you may not have enough IVs. To get more IVs, start up airodump-ng.exe again, and when asked the Output filename prefix, give the same name as you did previously. Airodump-ng will then append packets to the original dump.

## What next?

### Traffic capture

As this is a simulation, now that you have your WEP key, you can continue your penetration testing by using [AirPcap](http://www.crownhill.co.uk/product.php?prod=1779&ref=wireless-analysis) with Wireshark to [capture all the traffic](http://www.kabri.uk/2007/04/14/decrypting-wpa-with-airpcap-in-windows/) flowing over your WPA or WEP-enabled WLAN.

### Educate!

As one of the aims of my blog is to help people, if you have friends/neighbours/co-workers whose WLANs are WEP enabled, you could demonstrate how easy it is to crack WEP, and then help them set up a properly-implemented WPA/WPA2 WLAN 🙂

Did this help you at all? Any questions? Feel free to leave me a comment below!
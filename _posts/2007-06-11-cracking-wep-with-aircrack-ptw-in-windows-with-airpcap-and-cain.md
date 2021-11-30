---
id: 90
title: Cracking WEP with aircrack-ptw in Windows with AirPcap and Cain
date: 2007-06-11T14:22:31+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/06/11/cracking-wep-with-aircrack-ptw-in-windows-with-airpcap-and-cain/
permalink: /2007/06/11/cracking-wep-with-aircrack-ptw-in-windows-with-airpcap-and-cain/
ratings_score:
  - "41"
  - "41"
  - "41"
  - "41"
  - "41"
ratings_users:
  - "12"
  - "12"
  - "12"
  - "12"
  - "12"
ratings_average:
  - "3.42"
  - "3.42"
  - "3.42"
  - "3.42"
  - "3.42"
categories:
  - Networking
  - Security
  - Wi-Fi
  - Windows
---
<div class="highlight">
  <p>
    <strong>Every time you deploy a WEP Access Point, a fluffy kitty dies.</strong></div> 
    
    <h3>
      Primer
    </h3>
    
    <p>
      Recently a team of German cryptography researchers <a href="http://www.cdc.informatik.tu-darmstadt.de/aircrack-ptw/">perfected methods to recover a WEP key</a> faster than ever before. The older Weak IV attacks generally needed between 500,000 and 2,000,000 packets to recover a 128-bit WEP key. In contrast, the new PTW method needs a mere 85,000 packets to have a 95% chance of recovering the WEP key.
    </p>
    
    <p>
      Unlike the Weak IV attack, instead of collecting weak IVs, the PTW method collects ARP requests and responses to attack the encryption. ARP requests can either be collected naturally, or can be generated via packet injection. Until recently, packet injection was only possible in Linux. With the advent of the <a href="http://www.crownhill.co.uk/product.php?prod=1779&ref=wireless-analysis">AirPcap USB adapter</a>, and some unsupported beta drivers, it&#8217;s possible to inject packets in Windows. <em>Update:</em> CACE have released AirPcap Tx, which features fully supported packet injection, for an added premium.
    </p>
    
    <p>
      In this tutorial, I&#8217;ll guide you through the process of recovering a WEP key, via the PTW attack, in Windows. For this you&#8217;ll be using the AirPcap USB adapter, Cain, aircrack-ptw, and the aircrack-ng suite.
    </p>
    
    <p>
    </p>
    
    <p>
      <noscript>
        <a href="http://ws.amazon.co.uk/widgets/q?ServiceVersion=20070822&MarketPlace=GB&ID=V20070822%2FGB%2Fmincir0e-21%2F8010%2Fcccd45be-edcd-4422-a559-d4a7ab1be4d0&Operation=NoScript">Amazon.co.uk Widgets</a>
      </noscript>
    </p>
    
    <h3>
      Legalities
    </h3>
    
    <p>
      It&#8217;s important to point out that these methods should only be applied with permission from the owner of the target AP. You should either be auditing, penetration testing, or demonstrating the weaknesses of WEP in a Test Lab environment. You should not be using these methods to get &#8220;Free internet&#8221;!
    </p>
    
    <h3>
      Preparation
    </h3>
    
    <p>
      You&#8217;ll need:
    </p>
    
    <ul>
      <li>
        An AP configured with WEP
      </li>
      <li>
        At least one client associated with the Access Point (to give us an initial ARP request)
      </li>
      <li>
        A standard <a href="http://www.crownhill.co.uk/product.php?prod=1779&ref=wireless-analysis">AirPcap Adapter</a> with the unsupported <a href="http://rapidshare.com/files/29501895/setup_airpcap_2_0_beta_tx.exe.html">beta packet injection driver</a> <strong>or</strong> a fully-supported <a href="http://www.crownhill.co.uk/product.php?prod=1779&ref=wireless-analysis">AirPcap Tx</a>.
      </li>
      <li>
        <a href="http://www.oxid.it/cain.html">Cain and Abel</a>
      </li>
      <li>
        <a href="http://www.kabri.uk/wp-content/uploads/2007/05/aircrack-ng-0_7_0_beta1-airpcap.zip">aircrack-ng for AirPcap</a>
      </li>
      <li>
        <a href="http://files.tuto-fr.com/aircrack-ptw_win32.rar">aircrack-ptw for Windows</a>
      </li>
    </ul>
    
    <p>
      Now you&#8217;ll need to prepare the environment:
    </p>
    
    <ul>
      <li>
        Install the beta drivers (or if you have AirPcap Tx, install the drivers from the CD-ROM)
      </li>
      <li>
        Plug in the AirPcap
      </li>
      <li>
        Install Cain
      </li>
      <li>
        Extract aircrack-ng to c:\airpcap\
      </li>
      <li>
        Extract aircrack-ptw to c:\airpcap\
      </li>
      <li>
        Move aircrack-ptw.exe to the bin folder (this is no longer required &#8211; <a href="#ptw-notes">see my notes</a>)
      </li>
      <li>
        Optional: To make things easier, move the contents of the bin folder to c:\airpcap\. You&#8217;ll then be able to run aircrack-ptw.exe with just c:\airpcap\aircrack-ptw.exe mycapture.cap
      </li>
    </ul>
    
    <h3>
      Let&#8217;s get cracking
    </h3>
    
    <p>
      I added narration to the video this evening at 20:36. It&#8217;s my first attempt at narration, and a little noisy, but I&#8217;m sure things will improve as time goes on! 🙂
    </p>
    
    <p>
      <strong>[MEDIA=1]</strong>
    </p>
    
    <p>
      <a href="http://www.youtube.com/watch?v=6PjDyJqA6hY">Youtube Video Link</a>
    </p>
    
    <h3>
      Countermeasures
    </h3>
    
    <p>
      The primary counter measure to this WEP attack is to cease using WEP and switch your Access Points to WPA encryption. As you&#8217;ve seen in this video, WEP is just too easy to crack. For further reading, Wikipedia has an excellent entry on <a href="http://en.wikipedia.org/wiki/WPA2">WPA</a>.
    </p>
    
    <p>
      Access Points are so cheap now that, if your AP doesn&#8217;t support WPA via a firmware upgrade, you can easily afford a new one with full WPA or WPA2 support.
    </p>
    
    <h3 id="ptw-notes">
      Notes
    </h3>
    
    <p>
      Note 1: After recording this tutorial, I&#8217;ve become aware that, as of version 0.9, aircrack-ng.exe natively supports the PTW attack by using the -z switch. For example: <kbd>aircrack-ng.exe -z mycapturefile.cap</kbd>. If you want to use this attack, download <a href="http://www.aircrack-ng.org/doku.php#download">aircrack-ng from the authors</a>, and replace aircrack-ng.exe in c:\airpcap with the new one.
    </p>
    
    <p>
      Note 2: The whole process from starting capture to recovering the WEP key takes about 10 minutes.
    </p>
    
    <p>
      Note 3: It is important that you get the Packet Injection drivers and the aircrack-ng release specifically for the AirPcap adapter, or this will not work.
    </p>
    
    <p>
      Note 4: Just to summarise the steps in the video:
    </p>
    
    <ol>
      <li>
        Run Cain and passively scan for the target AP, making a note of the Channel number.
      </li>
      <li>
        Using the channel number, tell AirPcap to inject packets once it has collected an ARP request. (You can sometimes force an ARP by sending Deauth. To do that, right click on the client. Otherwise, repair the Wireless connection on the client connected to the AP)
      </li>
      <li>
        To use the PTW attack, you need to collect all packets. By running airodump-ng you can collect all the packets generated by Cain. The reason we use airodump-ng instead of Cain, is that Cain only collects WEP IVs.
      </li>
      <li>
        Once you&#8217;ve collected enough packets, run aircrack-ptw against the capture file.
      </li>
    </ol>
---
id: 88
title: Aircrack-PTW for Windows
date: 2007-06-11T12:09:55+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/06/11/aircrack-ptw-for-windows/
permalink: /2007/06/11/aircrack-ptw-for-windows/
ratings_users:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
ratings_score:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
ratings_average:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
categories:
  - Networking
  - Security
  - Wi-Fi
  - Windows
---
<div class="highlight">
  <strong>Update</strong></p> 
  
  <p>
    As of version 0.9, the aircrack-ng suite natively supports the PTW attack. <a href="http://www.aircrack-ng.org/doku.php#download">Download it here</a>. To invoke the PTW attack in aircrack-ng, run it with the -z switch: <kbd>aircrack-ng.exe -z mycapturefile.cap</kbd>.</div> 
    
    <p>
      A French chap has compiled Aircrack-PTW for Windows. This is great for anyone using the AirPcap adapter to inject packets in Windows, as the new PTW attack dramatically reduces the amount of packets you need to collect before attempting to crack the WEP key. Notice in the screenshot below, only 83,000 packets were needed to break a 128bit key; as opposed to around 400,000 with the KoreK attack.
    </p>
    
    <p>
      <a href="http://www.kabri.uk/wp-content/uploads/2007/06/2007-06-11_113648.png" title="aircrack-ptw on Windows"><img src="http://www.kabri.uk/wp-content/uploads/2007/06/2007-06-11_113648.thumbnail.png" alt="aircrack-ptw on Windows" /></a>
    </p>
    
    <p>
      The executable is in French but it&#8217;s still perfectly usable; All you&#8217;re looking for is the WEP key!
    </p>
    
    <p>
      Just run it with:
    </p>
    
    <p>
      <kbd>aircrack-ptw.exe yourcapturefile.cap</kbd>
    </p>
    
    <p>
      When I get some time I&#8217;ll try to compile a version in English, but for now you can grab the French version: <a href="http://files.tuto-fr.com/aircrack-ptw_win32.rar">Download Aircrack-PTW for Windows. </a>
    </p>
    
    <p>
      I&#8217;m in the process of writing up and recording a demonstration of cracking WEP in Windows with AirPcap, Cain, and aircrack-ptw. <strike>Expect to see something within a week!</strike> Update: <a href="http://www.kabri.uk/2007/06/11/cracking-wep-with-aircrack-ptw-in-windows-with-airpcap-and-cain/">Check it out here</a>
    </p>
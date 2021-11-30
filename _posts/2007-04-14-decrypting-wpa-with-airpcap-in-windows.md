---
id: 57
title: Decrypting WPA with AirPcap in Windows
date: 2007-04-14T10:58:58+00:00
author: Phil Wiffen
excerpt: |
  
  When AirPcap was first released, only WEP decryption was supported. However, with the release of Wireshark 0.99.5 it is possible to decrypt WPA packets with the AirPcap adapter in Windows. Here's how...
layout: post
guid: http://www.kabri.uk/2007/04/14/decrypting-wpa-with-airpcap-in-windows/
permalink: /2007/04/14/decrypting-wpa-with-airpcap-in-windows/
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
  - Troubleshooting
  - Wi-Fi
  - Windows
---
A step-by-step guide to decrypting WPA with Wireshark and AirPcap in Windows.<!--more-->

When AirPcap was first released, only WEP decryption was supported. However, with the release of Wireshark 0.99.5 it is possible to decrypt WPA packets with the [AirPcap adapter](http://www.crownhill.co.uk/product.php?prod=1779&ref=wireless-analysis) in Windows. Here&#8217;s how:

  1. Install [Wireshark 0.99.5](http://www.wireshark.org/download.html) or above
  2. Run Wireshark
  3. Go: View > Wireless Toolbar
  4. Click on &#8220;Decryption Keys&#8230;&#8221;
  5. Add a new decryption key. In my instance, because I know the Passphrase, I used WPA-PWD. If you&#8217;re doing penetration testing and, you have a 64byte string from something like AirCrack, you should use WPA-PSK.  
    [![2007-04-13_155300.gif](http://www.kabri.uk/wp-content/uploads/2007/04/2007-04-13_155300.thumbnail.gif)](http://www.kabri.uk/wp-content/uploads/2007/04/2007-04-13_155300.gif "2007-04-13_155300.gif")
  6. Capture away. In the screenshots below, I&#8217;ve filtered my own Wi-Fi card to cut down on the volume of &#8216;junk&#8217; and demonstrate that it is, in fact, decrypting the packets on the WLAN.  
    [![2007-04-13_160402.gif](http://www.kabri.uk/wp-content/uploads/2007/04/2007-04-13_160402.thumbnail.gif)](http://www.kabri.uk/wp-content/uploads/2007/04/2007-04-13_160402.gif "2007-04-13_160402.gif") [![2007-04-13_160440.gif](http://www.kabri.uk/wp-content/uploads/2007/04/2007-04-13_160440.thumbnail.gif)](http://www.kabri.uk/wp-content/uploads/2007/04/2007-04-13_160440.gif "2007-04-13_160440.gif")

For a lot more information on getting this set up, check out the [AirPcap Userguide](http://www.cacetech.com/support/downloads.htm).

Did this help you at all? Any questions? Feel free to leave me a comment below!
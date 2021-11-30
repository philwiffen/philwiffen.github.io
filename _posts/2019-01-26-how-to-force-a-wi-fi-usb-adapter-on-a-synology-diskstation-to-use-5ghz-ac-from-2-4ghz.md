---
id: 1582
title: How to force a Wi-Fi USB adapter on a Synology DiskStation to use 5GHz ac from 2.4GHz
date: 2019-01-26T23:09:54+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://kabri.uk/?p=1582
permalink: /2019/01/26/how-to-force-a-wi-fi-usb-adapter-on-a-synology-diskstation-to-use-5ghz-ac-from-2-4ghz/
categories:
  - Linux
  - Troubleshooting
  - Wi-Fi
---
### Useful if your SSIDs are identical for 5GHz and 2.4GHz. Having your SSIDs setup like this seems to confuse Synology DSM, and for me it would always connect to the 2.4GHz network.

I had this particular issue where my TP-Link T4U ac wifi adapter for my Synology kept dropping down to using the 2.4GHz network, which slows it down dramatically.

To fix this, here&#8217;s what I did. Your mileage may vary, and you may end up disconnecting your Synology from the network, so make sure you have another way of getting to it (such as Ethernet) before proceeding with any of this!

SSH to the DiskStation, login as admin.

sudo -s to root account (same password as admin account)

<pre class="wp-block-preformatted">sudo -s</pre>

Make a copy of your existing wifi config file inside /usr/syno/etc/wifi/

For me, I did:

<pre class="wp-block-preformatted">cp
/usr/syno/etc/wifi/wifi_client_00:11:22:33:44:DD:EE
/usr/syno/etc/wifi/wifi_client_00:11:22:33:44:DD:EE.bak</pre>

Edit the original file with vi. If you don&#8217;t know how to use vi, do a web searhc (it&#8217;s not hard, but not easy either). 

<pre class="wp-block-preformatted">vi
/usr/syno/etc/wifi/wifi_client_00:11:22:33:44:DD:EE</pre>

What you need to do is remove reference to the 2.4ghz network, which you can identify from the bssid, which is the MAC address of your router&#8217;s 2.4ghz radio. Once you&#8217;re done, the file should just contain details for the bssid that&#8217;s your 5ghz network. On my router, the MAC address for the 5GHz network was one hex number higher than the 2.4GHz network.

Next, make a copy of the wpa\_supplicant file in /usr/syno/etc. For me, this was called: wpa\_supplicant.conf.wlan0

<pre class="wp-block-preformatted">cp /usr/syno/etc/wpa_supplicant.conf.wlan0 /usr/syno/etc/wpa_supplicant.conf.wlan0.bak</pre>

Now edit the file, and change the bssid (which will be the 2.4ghz bssid MAC address) to the bssid MAC address of the 5ghz network.

<pre class="wp-block-preformatted">vi /usr/syno/etc/wpa_supplicant.conf.wlan0 </pre>

Reboot the Synology diskstation, and when it comes back, it should be on the 5GHz network.
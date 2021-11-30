---
id: 1518
title: Creating a Site to Site Routed VPN using DD-WRT and OpenVPN
date: 2017-11-19T13:19:40+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://kabri.uk/?p=1518
permalink: /2017/11/19/creating-a-site-to-site-routed-vpn-using-dd-wrt-and-openvpn/
categories:
  - Networking
  - Security
tags:
  - dd-wrt
  - Networking
  - openvpn
---
# <span style="color: #1e4e79; font-family: Calibri; font-size: 16pt;">Scenario</span>

I needed to setup a site-to-site VPN between my home and my parent&#8217;s home, so that we can back up our stuff offsite &#8211; mostly documents and precious digital photos.

# <span style="color: #1e4e79; font-family: Calibri; font-size: 16pt;">Requirements</span>

  * I wanted it to be a proper routed VPN network, not a bridged one. By that I mean an OpenVPN tun setup, not an OpenVPN tap setup.
  * I did not want to force the client to use the OpenVPN server as the gateway: I want both homes to use their own ISP for internet traffic. This is often referred to as split-tunnelling.
  * Must run both OpenVPN client and server on same DD-WRT router: For maximum flexibility I wanted to run both an OpenVPN server and client on the same DD-WRT router/gateway.

# <span style="color: #1e4e79; font-family: Calibri; font-size: 16pt;">Equipment</span>

1 x DD-WRT router at my place, acting as an openvpn server  
1 x DD-WRT (technically an ASUSWRT) router at the remote location, acting as an openvpn client

# <span style="color: #1e4e79; font-family: Calibri; font-size: 16pt;">Conceptual setup</span>

Local LAN: 192.168.1.0/24  
Remote LAN: 192.168.0.0/24  
OpenVPN network: 10.8.0.0/24

  * DD-WRT router acts as OpenVPN Server. 
      * LAN IP: 192.168.1.1/24. OpenVPN IP: 10.8.0.1/24

  * Remote DD-WRT router acts as an OpenVPN client. 
      * LAN IP: 192.168.0.1/24. OpenVPN IP: 10.8.0.2/24.

If your LAN/IP setup is different, you should be able to operate a Find/Replace to change all these.

# <span style="color: #1e4e79; font-family: Calibri; font-size: 16pt;">Some technical details</span>

DD-WRT version: DD-WRT v3 &#8211; DD-WRT v3.0-r33679 std (11/04/17)

DD-WRT server assigns tunnel device as tun2  
DD-WRT client assigns tunnel device as tun1  
DD-WRT bridges ethernet and WLAN devices into br0

# <span style="color: #1e4e79; font-family: Calibri; font-size: 16pt;">Considerations and gotchas</span>

## <span style="color: #2e75b5; font-family: Calibri; font-size: 14pt;">Most guides will get you *nearly* there</span>

Most guides I found online for setting up DD-WRT for a site to site VPN with OpenVPN got me _almost_ there, but didn&#8217;t quite finish the job. Many were also written over a year ago, and it seems DD-WRT has changed a bit since they were written. In addition, some threads where people were having issues seemed to give up on tun (routed) and switched to using tap (bridged) which wasn&#8217;t ideal for me.

Guides I found which may be useful to you include:

  1. Happydaddy post: <https://www.dd-wrt.com/phpBB2/viewtopic.php?t=304754>
  2. D0ug has an interesting setup, including kill switches. <https://www.dd-wrt.com/phpBB2/viewtopic.php?t=311904>
  3. Boogalooz guide: <https://dd-wrt.com/phpBB2/viewtopic.php?t=312064>

Note that you&#8217;ll need to register for the DD-WRT forums to see the images/attachments alluded to in the posts.

## <span style="color: #2e75b5; font-family: Calibri; font-size: 14pt;">Open the frontdoor</span>

If your DD-WRT device is also your gateway (that is, it has a modem connected to it, and it acts as your internet gateway) you&#8217;ll need to open up the port for the OpenVPN server using IPTABLES. Some guides seemed to skip this.

## <span style="color: #2e75b5; font-family: Calibri; font-size: 14pt;">You don&#8217;t really need to mess around with IPTABLES with the latest builds of DD-WRT</span>

It looks like in the past you had to do a lot of messing around with IPTABLES on DD-WRT to get OpenVPNs to work &#8211; mostly to pass traffic between the OpenVPN tun+ devices and the Bridged device (br0) on the router. Now you can just use the GUI, as it seems to autoconfigure everything for you.

## <span style="color: #2e75b5; font-family: Calibri; font-size: 14pt;">OpenVPN client with PBR and OpenVPN server don&#8217;t play nice</span>

If you have a VPN client, using Policy Based Routing (PBR) on the same DDWRT router as your OpenVPN server, you&#8217;ll hit this issue: <http://svn.dd-wrt.com/ticket/5690>. Put the suggested script from pastebin into your Startup Script and all will be well.

Symptoms for this issue are that you can ping from the Client network to computers inside the OpenVPN server&#8217;s local network, but not all IPs respond. It&#8217;ll turn out that the IPs that don&#8217;t respond will be in the PBR list for your OpenVPN client setup.

## <span style="color: #2e75b5; font-family: Calibri; font-size: 14pt;">iroutes are important</span>

One of the most common things I found was this symptom: You can ping from the client network to computers on the server&#8217;s network. But you cannot ping from the Server network back through to the Client&#8217;s LAN network. You can ping from the server network to the OpenVPN IP on the remote network (10.8.0.2 in my case) but not the IP on the other side of the router on the LAN interface (192.168.0.1 in my case).

The problem is that some of the guides you&#8217;ll find strewn around the internet don&#8217;t cover adding iroutes. Without adding an iroute to the OpenVPN client, you won&#8217;t be able to ping from the Server LAN to the Client LAN.

# <span style="color: #1e4e79; font-family: Calibri; font-size: 16pt;">General setup</span>

## <span style="color: #2e75b5; font-family: Calibri; font-size: 14pt;">Create server and client keys</span>

Sorting out the keys for the server and client is covered well in this post: [https://openvpn.net/index.php/open-source/documentation/howto.html#pki](https://openvpn.net/index.php/open-source/documentation/howto.html). This part of the setup is outside the scope of this blog post.

## <span style="color: #2e75b5; font-family: Calibri; font-size: 14pt;">Configure the OpenVPN server</span>

### <span style="color: #5b9bd5; font-family: Calibri; font-size: 12pt;">OpenVPN server setup in the DD-WRT GUI</span>

Here&#8217;s how my OpenVPN Server config looks [images below]

  1. I&#8217;m using WAN up, and configuring as a Server instead of Daemon.
  2. Also using Router server mode instead of Bridge.
  3. Don&#8217;t forget to enable &#8220;Allow client to client&#8221; so that the clients can talk to each other.
  4. In additional config add:

<pre style="margin-left: 36pt;"><span style="font-family: Consolas; font-size: 10pt;"># add a route to the client's LAN, and send it to the OpenVPN IP of the client.
</span><span style="font-family: Consolas; font-size: 10pt;">route 192.168.0.0 255.255.255.0 10.8.0.2
</span><span style="font-family: Consolas; font-size: 10pt;">#push a route to the client, which will send traffic for the Server's LAN over the VPN.
push "route 192.168.1.0 255.255.255.0"</span></pre>

[<img loading="lazy" class="wp-image-1528 size-medium alignnone" src="http://kabri.uk/wp-content/uploads/2017/11/2017-11-28-22_12_32-DD-WRT-build-33679-PPTP-300x287.png" alt="" width="300" height="287" />](http://kabri.uk/wp-content/uploads/2017/11/2017-11-28-22_12_32-DD-WRT-build-33679-PPTP.png)

[<img loading="lazy" class="alignnone wp-image-1516 size-medium" src="http://kabri.uk/wp-content/uploads/2017/11/111917_1153_CreatingaSi2-300x275.png" alt="" width="300" height="275" />](http://kabri.uk/wp-content/uploads/2017/11/111917_1153_CreatingaSi2.png)

[<img loading="lazy" class="size-medium wp-image-1517 alignnone" src="http://kabri.uk/wp-content/uploads/2017/11/111917_1153_CreatingaSi3-300x263.png" alt="" width="300" height="263" />](http://kabri.uk/wp-content/uploads/2017/11/111917_1153_CreatingaSi3.png)

Here&#8217;s the server conf file in case it&#8217;s useful:

<pre style="margin-left: 27pt;"><span style="font-family: Consolas;">root@DD-WRT:~# cat /tmp/openvpn/openvpn.conf
 </span><span style="font-family: Consolas;">dh /tmp/openvpn/dh.pem
 </span><span style="font-family: Consolas;">ca /tmp/openvpn/ca.crt
 </span><span style="font-family: Consolas;">cert /tmp/openvpn/cert.pem
 </span><span style="font-family: Consolas;">key /tmp/openvpn/key.pem
 </span><span style="font-family: Consolas;">keepalive 10 120
 </span><span style="font-family: Consolas;">verb 3
 </span><span style="font-family: Consolas;">mute 3
 </span><span style="font-family: Consolas;">syslog
 </span><span style="font-family: Consolas;">writepid /var/run/openvpnd.pid
 </span><span style="font-family: Consolas;">management 127.0.0.1 14
 </span><span style="font-family: Consolas;">management-log-cache 100
 </span><span style="font-family: Consolas;">topology subnet
 </span><span style="font-family: Consolas;">script-security 2
 </span><span style="font-family: Consolas;">port 1194
 </span><span style="font-family: Consolas;">proto udp4
 </span><span style="font-family: Consolas;">cipher aes-256-cbc
 </span><span style="font-family: Consolas;">auth sha256
 </span><span style="font-family: Consolas;">client-connect /tmp/openvpn/clcon.sh
 </span><span style="font-family: Consolas;">client-disconnect /tmp/openvpn/cldiscon.sh
 </span><span style="font-family: Consolas;">client-config-dir /tmp/openvpn/ccd
 </span><span style="font-family: Consolas;">comp-lzo adaptive
 </span><span style="font-family: Consolas;">tls-server
 </span><span style="font-family: Consolas;">ifconfig-pool-persist /tmp/openvpn/ip-pool 86400
 </span><span style="font-family: Consolas;">client-to-client
 </span><span style="font-family: Consolas;">tls-cipher TLS-RSA-WITH-AES-128-CBC-SHA
 </span><span style="font-family: Consolas;">fast-io
 </span><span style="font-family: Consolas;">tun-mtu 1400
 </span><span style="font-family: Consolas;">mtu-disc yes
 </span><span style="font-family: Consolas;">server 10.8.0.0 255.255.255.0
 </span><span style="font-family: Consolas;">dev tun2
 </span><span style="font-family: Consolas;">#additional config
 </span><span style="font-family: Consolas;">route 192.168.0.0 255.255.255.0 10.8.0.2
 </span><span style="font-family: Consolas;">push "route 192.168.1.0 255.255.255.0"
 </span></pre>

Example Client config ovpn file:

<pre style="padding-left: 30px;"><span style="font-family: Consolas; font-size: 10pt;">client</span>
<span style="font-family: Consolas; font-size: 10pt;">dev tun</span>
<span style="font-family: Consolas; font-size: 10pt;">proto udp</span>
<span style="font-family: Consolas; font-size: 10pt;">remote YOURopenvpnserverhostname.yourdynamicdnsservice.blah 1194</span>
<span style="font-family: Consolas; font-size: 10pt;">nobind</span>
<span style="font-family: Consolas; font-size: 10pt;">float</span>
<span style="font-family: Consolas; font-size: 10pt;">persist-key</span>
<span style="font-family: Consolas; font-size: 10pt;">persist-tun</span>
<span style="font-family: Consolas; font-size: 10pt;">remote-cert-tls server</span>
<span style="font-family: Consolas; font-size: 10pt;">auth-nocache</span>
<span style="font-family: Consolas; font-size: 10pt;">comp-lzo no</span>
<span style="font-family: Consolas; font-size: 10pt;">tun-mtu 1400</span>
<span style="font-family: Consolas; font-size: 10pt;">mssfix 1400</span>
<span style="font-family: Consolas; font-size: 10pt;">auth SHA256</span>
<span style="font-family: Consolas; font-size: 10pt;">cipher AES-256-CBC</span>
<span style="font-family: Consolas; font-size: 10pt;">&lt;ca&gt;PASTE CA.crt CERT CONTENTS HERE&lt;/ca&gt;
</span><span style="font-family: Consolas; font-size: 10pt;">&lt;cert&gt;PASTE client.crt CLIENT CERT CONTENTS HERE&lt;/cert&gt;
</span><span style="font-family: Consolas; font-size: 10pt;">&lt;key&gt;PASTE PRIVATE client.key CLIENT KEY CONTENTS HERE&lt;/key&gt;</span></pre>

Putting the contents of the ca, cert and key files into the ovpn files makes it much easier to import into an OpenVPN client. In my case, the ASUSWRT openvpn client wouldn&#8217;t accept these files individually, so I had to combine them in the ovpn profile file as above.

# <span style="color: #1e4e79; font-family: Calibri; font-size: 16pt;">Additional configuration to make it all work as expected</span>

Below are all the things I had to do in addition to general setup to make things work. That is, that both sides of the VPN could contact each other as expected in a site-to-site VPN.

## <span style="color: #2e75b5; font-family: Calibri; font-size: 14pt;">Open the OpenVPN Port</span>

Administration > Commands > Firewall Script

Add the following to the Firewall Script in DD-WRT.

<pre style="padding-left: 30px;"><span style="font-family: Consolas; font-size: 10pt;"># This lets the outside world connect to the port specified using the protocol specified running on the DD-WRT router.</span>
<span style="font-family: Consolas; font-size: 10pt;"># Command assumes you're using the udp protocol for openvpn, and port 1194. </span>
<span style="font-size: 10pt;"># <span style="font-family: Consolas;">Change to tcp if you're using that. And also change the port if you're using something else.</span></span>
<span style="font-family: Consolas; font-size: 10pt;">iptables -I INPUT 1 -p udp --dport 1194 -j ACCEPT</span></pre>

## <span style="color: #2e75b5; font-family: Calibri; font-size: 14pt;">Startup script to fix routing with OpenVPN client and PBR</span>

Administration > Commands > Startup Script

Go here for the overview: <http://svn.dd-wrt.com/ticket/5690> and use the script in the pastebin link to fix the issue. Add it to startup via Administration > Commands.

## <span style="color: #2e75b5; font-family: Calibri; font-size: 14pt;">Client config to provide iroute</span>

Administration > Commands > Startup Script

Add this to the bottom of the PBR fix script text in the Startup Script section

This is what enables you to ping from server network to client network. Without this, you&#8217;ll be able to ping from client LAN to server LAN, but not from Server LAN to Client LAN. The script ensures that on each boot of the router, it re-creates the client configuration file in the /tmp/ directory on the DD-WRT router and adds the iroute command to the config file. When the remote client connects, it&#8217;ll pick up this iroute.

There&#8217;s some really good information on why this works here: <http://backreference.org/2009/11/15/openvpn-and-iroute/> but basically, openvpn doesn&#8217;t quite behave like it should, so even though you may have all the right routes setup, it won&#8217;t work unless you&#8217;ve configured an iroute for the client.

Put this in your Startup Script, just after the PBR fix text:

<pre style="padding-left: 30px;"><span style="font-family: Consolas; font-size: 10pt;">test -d /tmp/openvpn || mkdir /tmp/openvpn</span>
<span style="font-family: Consolas; font-size: 10pt;">test -d /tmp/openvpn/ccd || mkdir /tmp/openvpn/ccd</span>
<span style="font-family: Consolas; font-size: 10pt;"># add the network of the Client's own LAN! Not the openvpn network, or the server's network. </span>
<span style="font-family: Consolas; font-size: 10pt;"># Also make sure that the filename matches that of the client's name. In my case, the client users the client001 cert.</span>
<span style="font-family: Consolas; font-size: 10pt;">echo "iroute 192.168.0.0 255.255.255.0" &gt; /tmp/openvpn/ccd/client001</span></pre>

[Source](https://www.dd-wrt.com/phpBB2/viewtopic.php?t=309251)
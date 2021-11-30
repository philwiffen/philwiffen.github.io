---
id: 332
title: Install and run Wireshark on the command line (CentOS 5.2)
date: 2008-08-06T22:00:11+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=332
permalink: /2008/08/06/install-and-run-wireshark-on-the-command-line-centos-52/
categories:
  - Linux
  - Security
tags:
  - cace
  - centos
  - ethereal
  - Linux
  - network forensics
  - Networking
  - rhel
  - Security
  - wireshark
---
Using CentOS 5.2 or Red Hat Enterprise Linux 5, install and run Wireshark (formerly Ethereal) over the command line.

Install Wireshark:

<pre><kbd>yum install wireshark</kbd></pre>

Run a capture:

<pre><kbd>tethereal -i eth1 -w ~/mycapture.pcap</kbd></pre>

This command will run Wireshark/Ethereal, capture on the eth1 interface and output the data to /yourhomedir/mycapture.pcap

Why would you want to do this? If you want to capture packets from a headless or remote Linux PC and analyse the data elsewhere.

Right now I&#8217;m at home, but I have a headless CentOS box at work that&#8217;s running ntop from a mirrored port, in order to look at network traffic flowing over the router. To increase the capability of the CentOS box, I want to use it to capture packets using Wireshark, then download the .pcap file over WinSCP and look at the data on my laptop using Wireshark for Windows.
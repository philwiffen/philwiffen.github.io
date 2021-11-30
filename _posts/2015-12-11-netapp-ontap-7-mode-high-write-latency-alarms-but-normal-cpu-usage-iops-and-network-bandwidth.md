---
id: 1335
title: 'NetApp ONTAP 7-mode: High Write Latency alarms but normal CPU usage, IOPS and network bandwidth'
date: 2015-12-11T13:37:48+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=1335
permalink: /2015/12/11/netapp-ontap-7-mode-high-write-latency-alarms-but-normal-cpu-usage-iops-and-network-bandwidth/
categories:
  - NetApp
tags:
  - 7-mode
  - netapp
  - ONTAP
---
<p lang="en-GB">
  This report has been written due to a number of write latency related bugs I&#8217;ve witnessed in recent versions on ONTAP 7-mode. It&#8217;s a modified version of an internal report that I wrote up in some free time. I thought I&#8217;d summarise my findings in case others are seeing similar issues.
</p>

<p lang="en-GB">
  <!--more-->
</p>

<h1 lang="en-GB">
  Symptoms
</h1>

<ul type="disc">
  <li lang="en-GB">
    High Write latency alarms being received.
  </li>
  <li lang="en-GB">
    Some write latencies up to 180ms (yes, 180 milliseconds)
  </li>
  <li lang="en-GB">
    CPU usage is not excessive
  </li>
</ul>

<h1 lang="en-GB">
  Diagnostics
</h1>

<li lang="en-GB">
   High write latency is sometimes associated with high CPU usage, but in this case CPU usage is <100% across all cores (priv set diag; sysstat -M)
</li>
<li lang="en-GB">
  IOPS going through the system is not abnormal (as in, it&#8217;s done a similar amount of IOPS, or more, in the past)
</li>
<li lang="en-GB">
  Network throughput on the system is not maxed out
</li>
<li lang="en-GB">
  NetApp perfstat analysis (at first level support) comes back as &#8220;system is being pushed to its limit, it&#8217;s probably time to upgrade&#8221; or &#8220;everything seems fine&#8221;. If you get this response, ask them to check the signature against the bugs below.
</li>

<h1 lang="en-GB">
  Known bugs
</h1>

<p lang="en-GB">
  There are a number of known bugs in ONTAP 7-mode that can cause this, based on experience. I&#8217;ve tried to summarise these below.
</p>

<h2 lang="en-GB">
  ONTAP 8.2.2P2
</h2>

<p lang="en-GB">
  <a href="http://mysupport.netapp.com/NOW/cgi-bin/bol?Type=Detail&Display=855574">Bug 855574</a>: Sequential appends to user file results in excessive write latency
</p>

<p lang="en-GB">
  Details:
</p>

<ul type="disc">
  <li lang="en-GB">
    Present in ONTAP 8.2.2P2
  </li>
  <li lang="en-GB">
    Introduced in 8.2 codebase (8.1 is immune)
  </li>
  <li lang="en-GB">
    Fixed in ONTAP 8.2.3P3 onwards
  </li>
</ul>

<p lang="en-GB">
  Recommendation:
</p>

<ul type="disc">
  <li lang="en-GB">
    Upgrade to ONTAP 8.2.4P6
  </li>
</ul>

<h2 lang="en-GB">
  ONTAP 8.2.3P3, possibly earlier versions too
</h2>

<p lang="en-GB">
  <a href="http://support.netapp.com/NOW/cgi-bin/bol?Type=Detail&Display=647449">Bug 647449</a>: Use of default quota rules can impact I/O latency and throughput
</p>

<p lang="en-GB">
  Details:
</p>

<ul type="disc">
  <li lang="en-GB">
    Present in ONTAP 8.2.3P3
  </li>
  <li lang="en-GB">
    Fixed in ONTAP 8.2.3P4
  </li>
</ul>

<p lang="en-GB">
  Recommendation:
</p>

<ul type="disc">
  <li lang="en-GB">
    Upgrade to ONTAP 8.2.4P6
  </li>
</ul>

<h2 lang="en-GB">
  ONTAP 8.2.3P3, ONTAP 8.2.3P4, ONTAP 8.2.3P6
</h2>

<p lang="en-GB">
  <a href="https://mysupport.netapp.com/NOW/cgi-bin/bol?Type=Detail&Display=928593">Bug 928593</a>: Write operations are not performed resulting in severe write latencies
</p>

<p lang="en-GB">
  Details:
</p>

<ul type="disc">
  <li lang="en-GB">
    First introduced in ONTAP 8.2.3P3. Remains in subsequent 8.2.3 P-releases
  </li>
  <li lang="en-GB">
    Mostly fixed in ONTAP 8.2.4. Waiting on P1 or P2 for more complete fix.
  </li>
  <li lang="en-GB">
    This bug is a direct relation of 855574, so if your workloads were &#8220;tickling&#8221; that bug you may see this bug, too.
  </li>
</ul>

<p lang="en-GB">
  Recommendation:
</p>

<ul type="disc">
  <li lang="en-GB">
    Stay on current version for now. While this bug is fixed in the recently-released 8.2.4, NetApp have asked us to hold off until 8.2.4P1 is released in Q1 2016, as they haven&#8217;t ironed out all the write performance bugs.
  </li>
</ul>
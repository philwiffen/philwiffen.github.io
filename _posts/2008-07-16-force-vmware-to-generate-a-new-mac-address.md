---
id: 312
title: How to force VMware to generate a new MAC address for a virtual machine
date: 2008-07-16T14:13:06+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=312
permalink: /2008/07/16/force-vmware-to-generate-a-new-mac-address/
aktt_notify_twitter:
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
categories:
  - Troubleshooting
  - Virtualisation
---
How to force VMware to regenerate a MAC address for a virtual machine (or guest OS).

  1. Shut down the Guest OS.
  2. Open up the .vmx file.
  3. Delete the following **lines** (that begin with&#8230;):
`
<pre>ethernet0.addressType
uuid.location =
uuid.bios =
ethernet0.generatedAddress =
ethernet0.generatedAddressOffset =</pre>
<p>` 
  4. Boot up the Guest OS again, and it should generate new details in the vmx file (I&#8217;d check afterwards to be doubly sure).



<noscript>
  <a href="http://ws.amazon.co.uk/widgets/q?ServiceVersion=20070822&MarketPlace=GB&ID=V20070822%2FGB%2Fmincir0e-21%2F8010%2F577cd4f2-61cd-4bc0-8cea-a59298323429&Operation=NoScript">Amazon.co.uk Widgets</a>
</noscript> 

The most common scenario for wanting to do this is if you&#8217;ve used a &#8220;template&#8221; Guest OS and copied it to multiple PCs, but accidentally clicked &#8220;I moved this Virtual Machine&#8221; rather than &#8220;I copied this Virtual Machine&#8221; when first booting the Guest OS in something like VMware Player.

If you tell VMware that the Guest OS was copied, it automatically generates new UUID info and MAC addresses. If you tell VMware that you moved the Guest OS, all unique identifiers are left alone (including the MAC address). By performing the steps above, you can get VMware to generate you some new, unique identifiers, and stop weirdness on your network 😉
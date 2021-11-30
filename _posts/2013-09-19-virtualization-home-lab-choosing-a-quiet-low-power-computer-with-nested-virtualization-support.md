---
id: 994
title: 'Virtualization Home Lab: Choosing a suitable computer (quiet, low power with nested virtualization support)'
date: 2013-09-19T19:45:40+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=994
permalink: /2013/09/19/virtualization-home-lab-choosing-a-quiet-low-power-computer-with-nested-virtualization-support/
categories:
  - Gigabyte Brix
  - Home Lab
  - Virtualisation
tags:
  - Brix
  - Gigabyte Brix
  - Home Lab
  - homelab
  - Intel NUC
  - Nested Virtualization
---
Recently, after about 2 years away, I&#8217;ve started to get back into Virtualisation. As part of that, like any true geek, I wanted to build a Home Lab.

I had some criteria for the homelab computer:

  1. Must be quiet
  2. Should be power-efficient/low power. <span style="color: #999999;">Energy in the UK is expensive!</span>
  3. CPU must support Intel VT-x with EPT, and VT-d virtualisation technologies
  4. Under £600 (roughly $1,000)
  5. System must be powerful enough to run nested hypervisors (enough RAM, CPU and Storage capacities)
  6. Minimal self-build. <span style="color: #999999;">I don&#8217;t have the inclination to build a white-box solution. If you do, check out <a href="http://wahlnetwork.com/my-home-lab/resources/"><span style="color: #999999;">Chris Wahl&#8217;s awesome resources</span></a>.</span>

And some nice-to-haves:

  1. Compact physical footprint
  2. Preferably run VMware ESXi without any installer ISO hacks or driver mods
  3. It should have enough Storage capacity to host [AutoLab](http://www.labguides.com/autolab/?) and some Hyper-V instances, too.

<!--more-->

# Why nested virtualisation? {#whynested}

Simplicity, cost, and a lack of a home office.

If you don&#8217;t know already, Nested Virtualisation is the practice of running a bare-metal hypervisor inside another bare-metal hypervisor. For example, you can run ESXi on a physical host, and then run multiple copies of ESXi as Virtual Machines.

Running nested VMs opens up the possibility of creating an _entire virtual lab_ inside a _single computer_, including things like a VM NAS appliance and a VM router. This is very, very cool and eliminates the need for a physical switch/networking infrastructure for the lab. <span style="color: #999999;">And you can also run Hyper-V inside ESXi, if you want to. <span style="color: #333333;">William Lam has some great resources on <a href="http://www.virtuallyghetto.com/2012/10/nested-virtualization-resources.html"><span style="color: #333333;">running Nested Virtualisation</span></a></span><br /> </span>

I don&#8217;t earn enough money to justify spending 2,000 pounds, euros or dollars on a home lab to kit it out with a NAS, VLAN-capable managed switch, and multiple hosts with multiple NICs. If I can run nested hypervisors in a single box, I should save myself a lot of money short-term and I always have the flexibility to expand the lab later. Because I knew I&#8217;d be saving money by not buying so much equipment, I was prepared to spend a little more on a single server.

I also don&#8217;t have a spare room or office to hide this homelab in. It must sit on or under my desk in the living room, next to my head, the TV and the open-plan kitchen.

# Choosing a suitable candidate

## Finding a CPU

When you&#8217;re making a virtualisation home lab, it&#8217;s important to consider the Virtualisation features on the CPU you&#8217;re buying. For server-class hardware, this doesn&#8217;t matter as much as many Xeons support Virtualisation, but for consumer-grade CPUs it&#8217;s important to check.

I found the [Intel ARK website](http://ark.intel.com/) fantastic for this, as it allows you to create comparison tables for CPUs. I made one that compares the CPUs in the i3 and i5 versions of  the Gigabyte Brix, Intel NUC, and the Xeon in the Dell T110 II, which really helped guide my decisions: [Compare Home Lab system CPUs](http://ark.intel.com/compare/72057,72055,65697,64903,65734)

Useful CPU features in a Virtualisation Home Lab:

**Intel VT-x with EPT (Extended Page Tables)**  
These two features, combined, enable you to run Nested Hypervisors with 64-bit Guest OS support.

**VT-d**  
This enables you to directly &#8220;map&#8221; a physical device connected to the PCI bus, such as a USB controller or an external NIC, for exclusive use by a Virtual Machine. This is useful, but not essential for everyone.

## Finding a Suitable Computer

In the sections below, I&#8217;ll cover a general overview of the system and specs relevant to home labs, such as: Physical Size, CPUs, max RAM, Storage options, NICs, Expandability, Power Consumption, Noise, and Cost.

### Server-Class: Dell T110 II

I looked at [Chris Wahl&#8217;s excellent home lab notes](http://wahlnetwork.com/2011/01/26/vmware-home-lab-dell-t110-branded-box/) and took a look at the [Dell T110 II](http://www.dell.com/uk/business/p/poweredge-t110-2/pd), the successor to the T110. It&#8217;s a nice system: Quiet and relatively power efficient, especially considering that it runs a Xeon. It&#8217;s also on the [VMware Hardware Compatibility List](http://partnerweb.vmware.com/comp_guide2/detail.php?deviceCategory=server&productid=20968&vcl=true). The only negative for this system is that it&#8217;s quite large for my requirements. I found some good deals in the Dell Outlet, but I never bit the bullet as the processor was always the older E3-1220.

Here&#8217;s the system spec that nearly won me over:

  * Size: Tower server.
  * CPU: Intel Xeon E3-1220V2. It&#8217;s fairly old, but is on VMware&#8217;s HCL, and supports VT-d and VT-x with EPT
  * Max RAM: 32GB (ECC)
  * NICs: 1, but can add more through expansion slots.
  * Storage: Up to 4 SATA drives, with RAID options if you&#8217;re willing to pay a premium
  * Expansion: Plenty of space and PCIe slots for expansion
  * Power Consumption: [38W at idle](http://www.pcpro.co.uk/reviews/servers/369607/dell-poweredge-t110-ii/specifications), 110W max
  * Noise:  Reviews seem to confirm [the T110 II is quiet](http://www.pcmag.com/article2/0,2817,2394557,00.asp)
  * Cost: Roughly £550 including VAT for a system with 3-year warranty, 8GB RAM, 1 x 500GB HDD and Intel Xeon E3-1220V.

Why I didn&#8217;t go for it:

  * Ultimately, it&#8217;s just a bit too big for my situation (but still requires less floorspace than many rackmount servers)
  * It&#8217;s an 11G server (currently on 12G) and I&#8217;m convinced that Dell may replace it with something better soon
  * While still very good, the power consumption just wasn&#8217;t as good as the compact PCs below (but it is a server-class system, so that&#8217;s to be expected)

### Nano-Class: Intel NUC and Gigabyte Brix

<img loading="lazy" class="alignnone size-full wp-image-1070" alt="brix vs xbox controller" src="http://www.kabri.uk/wp-content/uploads/2013/09/brix-vs-xbox-controller.jpg" width="400" height="200" /> 

From my research, there&#8217;s two main Nano-sized contenders in the Home Lab space: The Intel NUC and the Gigabyte Brix, available in Core i3, i5 and i7 flavours. The i7 was overkill for me &#8211; and prohibitively expensive &#8211; so I left it out of contention.

The Brix and NUC come in barebone kits to which you add your own RAM and mSATA SSD. This makes the total cost flexible to individual needs. Both brands offer roughly the same features for a home lab, and choosing one usually depends on personal preference.

Here&#8217;s the generic specs for the systems:

  * **Size:** Very small (about the size of an Xbox 360 controller)
  * **CPUs:** Core i3 and Core i5, both supporting VT-x with EPT. The i5 systems support VT-d, if you require that
  * **Storage:** The systems take an mSATA HDD. If you have an existing NAS for your VMware datastore, you can get away with a small mSATA drive of 32GB or using a USB stick to boot ESXi. Due to me wanting to run Autolab and not having a NAS, I bought a[ Plextor M5M 256GB](http://www.amazon.co.uk/gp/product/B00B5KGGZ2/ref=as_li_ss_tl?ie=UTF8&camp=1634&creative=19450&creativeASIN=B00B5KGGZ2&linkCode=as2&tag=mincir0e-21) as [reviews](http://www.anandtech.com/show/6722/plextor-m5m-256gb-msata-review) say it&#8217;s pretty quick and it was around the same price-per-gig as a Crucial mSATA drive.
  * **Expansion:** Due to its size, expansion is limited. You won&#8217;t be able to add extra NICs or SATA drives into these diminutive systems
  * **Max RAM:** up to 16GB (2 x 8GB SO-DIMM). The CPUs will take 32GB, but there just aren&#8217;t 16GB SO-DIMMs available yet. I wouldn&#8217;t hold out for them either.
  * **NICs:** 1 Gigabit NIC
  * **Power Consumption:** The i5 version of the NUC apparently uses [10W at idle](http://www.anandtech.com/show/6444/intels-next-unit-of-computing-hands-on), and nearly 20W at load. My i5 Brix uses (measured at power outlet) roughly 12W at idle running ESXi and up to 25W when I push it really hard.
  * **Noise:** Both systems are very quiet. The NUC is [quiet](http://www.pcpro.co.uk/reviews/barebones/379267/intel-nuc). My Brix is incredibly quiet, and sits happily next to me on my desk. Fan speed ramps up under load, but it&#8217;s never loud.
  * **Cost:** Generally the i3 versions of each system are around £250 ($400), and the i5 versions are around £320 ($515). Remember that you&#8217;ll need to add RAM and an mSATA SSD.

Let&#8217;s take a look at the individual merits of each system.

#### Intel NUC

The [Intel NUC](http://www.intel.com/content/www/us/en/motherboards/desktop-motherboards/nuc.html) is a small, low power barebones system. It comes with different CPU offerings, including an i3 and i5 that support VT-x with EPT. The i5 supports VT-d.

For the NUC, in addition to an mSATA SSD and RAM, you will need to add a &#8220;Clover&#8221; or &#8220;Mickey Mouse&#8221; power cable for your country (Yes, really. One doesn&#8217;t come in the box).

Here&#8217;s the two main systems I feel are suitable for a home lab:

  * **NUC Core i3, supporting VT-x with EPT**: 
      * Intel Site: [Intel® NUC Kit DC3217IYE](http://www.intel.com/content/www/us/en/motherboards/desktop-motherboards/desktop-kit-dc3217iye.html "Intel® NUC Kit DC3217IYE")
      * Reviews: [Google search for reviews](https://www.google.com/search?q=DC3217IYE+review)
      * Buy: [Amazon UK](http://www.amazon.co.uk/gp/product/B0093LINVK/ref=as_li_ss_tl?ie=UTF8&camp=1634&creative=19450&creativeASIN=B0093LINVK&linkCode=as2&tag=mincir0e-21) | [Google Shopping](https://www.google.com/search?q=DC3217IYE+buy)

  * **NUC Core i5, supporting VT-x with EPT and VT-d**: 
      * Intel Site: [Intel® NUC Kit DC53427HYE](http://www.intel.com/content/www/us/en/motherboards/desktop-motherboards/desktop-kit-dc53427hye.html)
      * Reviews: [Google search for reviews](https://www.google.com/search?q=DC53427HYE+review)
      * Buy: [Amazon UK](https://www.amazon.co.uk/dp/B00C9KMNUO/ref=as_li_ss_til?tag=mincir0e-21&camp=2902&creative=19466&linkCode=as4&creativeASIN=B00C9KMNUO&adid=17T44RQ64FHM1R48C0NA&) | [Google Shopping](https://www.google.com/search?q=DC53427HYE+buy)

#### Gigabyte Brix

<img loading="lazy" class="alignnone size-full wp-image-1076" alt="brix rear port connectivity" src="http://www.kabri.uk/wp-content/uploads/2013/09/brix-rear-port-connectivity.jpg" width="497" height="189" /> 

I suspected a new NUC might be coming out with a Haswell processor, so I searched The Register. When I did, I saw an [article on the Gigabyte Brix](http://www.theregister.co.uk/2013/04/16/gigabyte_pitches_intel_nuc_rival/), and did some research on it.

The Gigabye Brix has the following advantages over the NUC:

  1. The Realtek RTL8111E Gigabit NIC is natively supported in VMware ESXi 5.1, so no need to mess around with additional drivers. Although thanks to [Alex Galbraith](http://www.tekhead.org/blog/2013/01/nanolab-running-vmware-vsphere-on-intel-nuc-part-1/) this is pretty easy for the NUC.
  2. Comes with a region-specific power cable (unlike the NUC, where you need to buy a laptop/clover/&#8221;mickey mouse&#8221; power cable to plug into the power adapter)
  3. Comes with a Wi-Fi adapter (not that useful for homelabs, though)
  4. 2 x USB3 ports (vs just the 1 on the NUC). The NUC however, does have 3 USB ports in total vs just 2 on the Brix. As I&#8217;ll be running my home lab system headless, and booting ESXi from a USB flash drive, this doesn&#8217;t matter too much, but it may be a consideration for you.
  5. At the time, the Brix was cheaper than the equivalent NUC. Prices have normalised now, though.

The Brix comes in two flavours that may be useful for Virtualisation:

<ul id="shoppinglist">
  <li>
    <strong>GB-XM12-3227: Brix Core i3, supporting VT-x with EPT</strong>: <ul>
      <li>
        Gigabyte Site:  <a href="http://www.gigabyte.com/products/product-page.aspx?pid=4604">GB-XM12-3227 (rev. 1.0)</a>
      </li>
      <li>
        Reviews: <a href="https://www.google.com/search?q=GB-XM12-3227+review">Google search for reviews</a>
      </li>
      <li>
        Buy: <a href="https://www.amazon.co.uk/dp/B00CUZPNKK/ref=as_li_ss_til?tag=mincir0e-21&camp=2902&creative=19466&linkCode=as4&creativeASIN=B00CUZPNKK&adid=158GDXBPSJ1SHAA7THFT&">Amazon UK</a> | <a href="https://www.google.com/search?q=GB-XM12-3227+buy">Google Shopping</a>
      </li>
    </ul>
  </li>
  
  <li>
    <strong>GB-XM11-3337: Brix Core i5, supporting VT-x with EPT and VT-d</strong>: <ul>
      <li>
        Gigabyte Site: <a href="http://www.gigabyte.com/products/product-page.aspx?pid=4603"><span style="line-height: 1.714285714; font-size: 1rem;">GB-XM11-3337 (rev. 1.0)</span></a>
      </li>
      <li>
        Reviews: <a href="https://www.google.com/search?q=GB-XM11-3337+review">Google search for reviews</a>
      </li>
      <li>
        Buy: <a href="http://www.amazon.co.uk/gp/product/B00CUZPNHS/ref=as_li_ss_tl?ie=UTF8&camp=1634&creative=19450&creativeASIN=B00CUZPNHS&linkCode=as2&tag=mincir0e-21">Amazon UK</a> | <a href="https://www.google.com/search?q=GB-XM11-3337+buy">Google Shopping</a>
      </li>
    </ul>
  </li>
</ul>

## Choosing a Hard Drive and RAM for your Intel NUC or Gigabyte Brix

### Hard Drive (mSATA)

The NUC and Brix take mSATA drives, which are smaller versions of standard SSD drives, generally available in Ultrabooks. SSD capacities go up to 256GB, and tend to be a little more expensive than normal 2.5&#8243; SATA SSDs. From the research I did, these two brands were mentioned in good light:

  * Crucial mSATA SSD [M500](ttps://www.google.com/search?q=crucial%20m500%20msata) and the M4 are apparently reliable, and good value for money, and will cost you around £160 ($260, €190) for a 240+ GB SSD. Smaller capacities are cheaper, naturally. 128GB is around £80.
  * <a style="line-height: 1.714285714; font-size: 1rem;" href="https://www.google.com/search?q=plextor+m5m+msata">Plextor M5M mSATA</a><span style="line-height: 1.714285714; font-size: 1rem;">. A 256GB one will cost you around the same price as a Crucial SSD, I went for the Plextor, as the power issues mentioned in the <a href="http://www.anandtech.com/show/6722/plextor-m5m-256gb-msata-review">Anandtech review</a> have now been resolved with the 1.03 version of the firmware. More specs <a href="http://www.plextoramericas.com/index.php/ssd/px-m5m-series?start=1">here</a></span>

### RAM

The NUC and Brix take standard laptop DDR3 1600Mhz non-ECC SO-DIMM RAM, making it cheaper to buy than ECC server RAM.

Rough costs for RAM are around £50 ($80, €60) per 8GB stick, so you&#8217;re looking at £100 for 16GB RAM. I went for [Crucial RAM,](http://www.amazon.co.uk/gp/product/B006YG8X9Y/ref=as_li_ss_tl?ie=UTF8&camp=1634&creative=19450&creativeASIN=B006YG8X9Y&linkCode=as2&tag=mincir0e-21) as I&#8217;ve used them many times over the years and they&#8217;ve always been reliable

## Conclusion

After careful consideration, I opted for the Gigabyte Brix Core i5 GB-XM11-3337 system as it met all my requirements and, at the time, it was 20% cheaper than the NUC. I added 16GB of RAM, and a 256GB SSD.

Total cost was around £575, so only slightly more expensive than a Dell T110 II server.

So far, it&#8217;s running nicely with VMware ESXi 5.1, and I&#8217;ve tested and confirmed that it supports nested virtualisation by following [William Lam&#8217;s Nested guidelines](http://www.virtuallyghetto.com/2012/10/nested-virtualization-resources.html) and am now running Hyper-V Server 2012 R2 nested. I&#8217;m in the process of trying to setup AutoLab on it to run a full nested environment.

I&#8217;m looking forward to putting ESXi 5.5 on it to take advantage of the C-states support for even lower power usage when idle. It currently uses around 10 Watts at idle.

If you found this useful, or have any feedback on this article, let me know 🙂

Share and enjoy 😉
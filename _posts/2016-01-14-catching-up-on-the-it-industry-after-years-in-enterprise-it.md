---
id: 1385
title: Catching up on the IT industry after years in Enterprise IT
date: 2016-01-14T16:20:23+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://kabri.uk/?p=1385
permalink: /2016/01/14/catching-up-on-the-it-industry-after-years-in-enterprise-it/
categories:
  - Career
---
<h1 lang="en-GB">
  Overview and Scope
</h1>

<p lang="en-GB">
  I wrote this after a colleague requested some things they should read to catch up on what&#8217;s been going on in the IT industry over the last few years.
</p>

<p lang="en-GB">
  Enterprise IT often moves at a much slower pace than other IT adopters, and we can be so inwardly focused that we don&#8217;t get a chance to see what&#8217;s going on outside. I imagine many others are in the same boat, so I thought I&#8217;d publish something for both internal and external consumption.
</p>

<p lang="en-GB">
  The intention is to summarise some general observations on the IT industry from a systems administration perspective; comment on where I think things are going; and then provide some links for further learning/research if you&#8217;re that way inclined. My focus of interest is mainly in the Virtualization, Cloud and Storage space so apologies for the lack of Windows-based innovation.
</p>

<h1 lang="en-GB">
  General observations
</h1>

<h2 lang="en-GB">
  Virtualization is commoditized
</h2>

<p lang="en-GB">
  In the last few years, virtualization (hypervisors) as a way of decoupling operating systems from their underlying hardware, has been largely commoditized. Hypervisors are so common as to be taken for granted, and understanding basic virtualization concepts is assumed. In fact, the concept of virtualizing compute is so normal now that vendors are looking to virtualize networking and storage as well as compute.
</p>

<p lang="en-GB">
  In the world of High Performance Compute, virtualization of computers is still fairly &#8220;exotic&#8221;. This is mostly because our main business needs to eke out every last CPU cycle to free up hideously expensive simulation licenses ASAP. Nowadays, when I tell vendors who solve problems caused by virtualization that we barely virtualize, I get funny looks 🙂
</p>

<h2 lang="en-GB">
  All-Flash Storage Arrays
</h2>

<p lang="en-GB">
  The storage industry as a whole is moving away from regular spinning disk to flash memory, fast. AFAs (All Flash Arrays) are everywhere, it seems.
</p>

<h2 lang="en-GB">
  Cloudy cloud cloud
</h2>

<p lang="en-GB">
  Cloud is everywhere, but it&#8217;s not just virtualization done in a data center run by someone else. Cloud is all of the value-add stuff that you want after you gain the flexibility of virtualization. Cloud is automation of workloads, it&#8217;s customer self-service VM deployments, it&#8217;s automated spin up of VMs to meet demands, it&#8217;s automated failover to a DR site in the case of a disaster. Cloud is not having to worry about if server Freddie is going to suffer a disk failure soon, whether I&#8217;m about to run out of storage space, or if I&#8217;m going to run out of network switch ports when I next need to roll out some hardware. It&#8217;s liberating! 🙂
</p>

<h2 lang="en-GB">
  Reduction of friction for developers
</h2>

<p lang="en-GB">
  What&#8217;s the biggest problem for Devs? Pesky IT slowing them down!
</p>

<p lang="en-GB">
  Two things of interest in this area:
</p>

<ul type="disc">
  <li lang="en-GB">
    <a href="https://en.wikipedia.org/wiki/DevOps">DevOps</a>
  </li>
  <li lang="en-GB">
    <a href="https://www.docker.com/what-docker">Docker</a>
  </li>
</ul>

<h1 lang="en-GB">
  Where are things going?
</h1>

<h2 lang="en-GB">
  Hyper-Convergence
</h2>

<p lang="en-GB">
  Managing the Compute, Storage and Networking elements of a Virtualization stack can be bothersome. Some vendors are pushing Hyper-Convergence, which effectively enables compute nodes to cluster together, pool their storage, and then treat that storage as a shared pool. The idea here is that you focus less on managing your hardware stacks and more on managing VMs/adding value elsewhere. A worthy goal.
</p>

<h2 lang="en-GB">
  DevOps
</h2>

<p lang="en-GB">
  Perhaps not as applicable to the Semiconductor industry as others, but still interesting, is the <a href="https://en.wikipedia.org/wiki/DevOps">DevOps</a> movement. DevOps is most common in companies that develop customer-facing web applications or mobile phone apps. Devs create the code and deploy it, Ops make sure the platform (server, OS etc) is stable and running. My take on DevOps is that its aim is to encourage Developers and Ops to co-operate and communicate with each other, rather than pointing the finger at each other, leading to a more stable platform and faster innovation. Magic.
</p>

<h2 lang="en-GB">
  Hybrid Cloud
</h2>

<p lang="en-GB">
  In the last few years, everyone&#8217;s figured out that pure Public Cloud is not necessarily a panacea, and that a blended approach to cloud is needed. Cue: Hybrid Cloud, which is usually a combination of Public cloud and Private cloud with the ability to move workloads between.
</p>

<h2 lang="en-GB">
  Automate or die
</h2>

<p lang="en-GB">
  There&#8217;s a general agreement that our roles as IT Professionals need to change, and that simply being a sysadmin/server hugger isn&#8217;t enough. The idea is to take steps towards automating much of our roles and then for us to focus on adding value to the business elsewhere (like, you know, having a relationship with the business). We should also start treating our resources as <a href="http://www.theregister.co.uk/2013/03/18/servers_pets_or_cattle_cern/">Cattle and not Pets</a>. The adoption of &#8220;the Cloud&#8221; is quickly accelerating this. Scripting languages like Python and/or PowerShell can help to automate common tasks.
</p>

<h1 lang="en-GB">
  Who&#8217;s doing what (vendors)
</h1>

<p lang="en-GB">
  While this list isn&#8217;t exhaustive, I&#8217;ve tried to summarise the main players I&#8217;m aware of in each niche. The likelihood of me missing someone is high.
</p>

<h2 lang="en-GB">
  Cloud platforms
</h2>

<ul type="disc">
  <li lang="en-GB">
    <a href="https://aws.amazon.com/">Amazon Web Services</a> &#8211; the defacto king of cloud. You can play with it <a href="https://aws.amazon.com/free/">for free</a>
  </li>
</ul>

<ul type="disc">
  <li lang="en-GB">
    <a href="https://azure.microsoft.com/en-gb/">Microsoft Azure</a> &#8211; a worthy contender. You can also play with this <a href="https://azure.microsoft.com/en-gb/pricing/free-trial/">for free</a>
  </li>
  <li lang="en-GB">
    <a href="https://www.openstack.org/">OpenStack</a> &#8211; create a private cloud for free* (*requires time and patience)
  </li>
</ul>

<h2 lang="en-GB">
  Hyper-Convergence
</h2>

<ul type="disc">
  <li lang="en-GB">
    <a href="http://www.nutanix.com/">Nutanix</a> &#8211; probably the most well-known in this space. They have a <a href="http://www.nutanix.com/products/community-edition/">Community Edition</a> of their software that you can play with for free.
  </li>
  <li lang="en-GB">
    <a href="https://www.simplivity.com/">Simplivity</a>
  </li>
  <li lang="en-GB">
    <a href="http://www.vmware.com/uk/products/virtual-san">VMware VSAN</a>
  </li>
</ul>

<h2 lang="en-GB">
  Storage Arrays
</h2>

<h3 lang="en-GB">
  Virtualization focused and/or All Flash Arrays
</h3>

<ul type="disc">
  <li lang="en-GB">
    <a href="http://www.solidfire.com/">SolidFire</a> (a recent acquisition for NetApp)
  </li>
  <li lang="en-GB">
    <a href="http://www.purestorage.com">Pure Storage</a>
  </li>
</ul>

<ul type="disc">
  <li lang="en-GB">
    <a href="http://www.nimblestorage.com/">Nimble Storage</a>
  </li>
  <li lang="en-GB">
    <a href="http://www.tegile.com/">Tegile</a>
  </li>
</ul>

<ul type="disc">
  <li lang="en-GB">
    <a href="https://www.tintri.com/">Tintri</a>
  </li>
</ul>

<ul type="disc">
  <li lang="en-GB">
    <a href="http://www.emc.com/storage/xtremio/overview.htm">EMC Xtremio</a>
  </li>
</ul>

<h3 lang="en-GB">
  NAS
</h3>

<ul type="disc">
  <li lang="en-GB">
    <a href="http://www.netapp.com/us/products/storage-systems/all-flash-fas/index.aspx">NetApp FAS</a>
  </li>
</ul>

<ul type="disc">
  <li lang="en-GB">
    <a href="http://www.emc.com/en-us/storage/isilon/index.htm">EMC Isilon</a>
  </li>
</ul>

<h1 lang="en-GB">
  Filling the gaps
</h1>

<h2 lang="en-GB">
  Virtualization
</h2>

In HPC, some of us don&#8217;t get much exposure to virtualization tech, so I&#8217;d recommend checking out [VMware&#8217;s free courses](https://mylearn.vmware.com/mgrReg/plan.cfm?plan=33369&ui=www_edu) such as [<span lang="en-US">Data Center Virtualization</span>](http://mylearn.vmware.com/mgrReg/courses.cfm?ui=www_edu&a=det&id_course=260034)<span lang="en-US">. </span><span lang="en-GB">VMware ESXi (aka vSphere) is pretty much the defacto standard for hypervisors, but Hyper-V, and KVM (featured in OpenStack) are also pretty popular.</span>

<h1 lang="en-GB">
  Where can I learn more?
</h1>

<ul type="disc">
  <li lang="en-GB">
    Check out the links above, and:
  </li>
  <li lang="en-GB">
    I cover a lot of free learning on IT topics in <a href="http://kabri.uk/2014/07/13/completely-free-it-training-resources-to-help-diversify-your-it-career/">Completely free IT training resources to help diversify your IT career</a>. I&#8217;ve fully updated it as part of this write-up so all the links should still be working.
  </li>
</ul>
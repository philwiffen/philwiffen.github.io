---
id: 1171
title: Installing EMC Isilon Virtual Nodes onto VMware ESXi
date: 2014-05-10T15:33:46+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=1171
permalink: /2014/05/10/installing-emc-isilon-virtual-nodes-onto-vmware-esxi/
categories:
  - Home Lab
  - Storage
  - Virtualisation
---
<span style="color: #1e4e79; font-size: 16pt;">Background</span>

Isilon, if you&#8217;re not aware of it, is a clustered Scale-out NAS solution from [EMC](http://www.emc.com/isilon). The article below covers setting up a virtual Isilon cluster suitable for experimenting and testing out Isilon in a VMware ESXi-based lab environment.

<span style="color: #1e4e79; font-size: 16pt;">Scenario and scope<br /> </span>

  * <span style="color: black;">Create a 3-node virtual EMC Isilon storage cluster on VMware ESXi.</span>
  * <span style="color: black;">This guide is written for ESXi Standalone (Free edition) in my home lab, but should be applicable to a &#8220;real&#8221; Virtual Infrastructure setup with vCenter, too.</span>

<!--more-->

<span style="color: #1e4e79; font-size: 16pt;">Obtain EMC Isilon Virtual Machine files<br /> </span>

<span style="color: black;">Download the Isilon OneFS VM files from <a href="http://www.emc.com/getisilon">www.emc.com/getisilon</a> (<a href="http://www.emc.com/products-solutions/trial-software-download/isilon.htm?PID=SWD_isilon_trialsoftware">alternative link</a>)<br /> </span>

<span style="color: black;">You&#8217;ll need to sign up for an EMC account. You <strong>do not</strong> need to be an EMC customer to download the Isilon VM, and I&#8217;ve confirmed this using a personal EMC account rather than my company one. In previous editions of EMC Isilon Virtual Nodes, I believe you needed to be a customer to download the Isilon OneFS Virtual Node.</span>

<span style="color: #1e4e79; font-size: 16pt;">Setup ESXi networking<br /> </span>

<span style="color: black;">Create a new private vSwitch called something like IsilonInternal. By private I mean, it doesn&#8217;t need to be connected to a physical/public facing NIC. This is used for the Isilon nodes to talk to each other on an internal network.</span>

<span style="color: #1e4e79; font-size: 16pt;">Prepare and upload the VMs to the ESXi host<br /> </span>

> <span style="color: black;">Note: Unlike the .pdf instructions, we can&#8217;t use the VMs inside the &#8220;clone*&#8221; folders which you&#8217;d normally use with VMware Workstation. They won&#8217;t convert for some reason, and I can&#8217;t figure out why at the moment.</span>

<span style="color: black;">Extract the .zip file you downloaded from EMC earlier (for example <em>EMC_Isilon_OneFS_7.1.0.1_Simulator.zip</em>)<br /> </span>

<span style="color: black;">You should now have a folder called something like <em>EMC_Isilon_OneFS_7.1.0.1_Simulator</em>. Inside that, will be a folder beginning with b (such as <em>b.7.1.0.34r.vga</em>). Inside that folder, is the VM files we need which we&#8217;ll convert into multiple Isilon VM nodes.<br /> </span>

<span style="color: black;">In particular, make a note of where the .vmx file is:<br /> </span>

<p style="padding-left: 30px;">
  <img src="http://www.kabri.uk/wp-content/uploads/2014/05/051014_1433_Installingt1.png" alt="" />
</p>

<span style="color: #2e75b5; font-size: 14pt;">Convert VMs to be ESXi-compatible<br /> </span>

<span style="color: black;">Next, convert the VMs from Workstation VMs to ESXi-compatible ones.<br /> </span>

<span style="color: black;">It&#8217;s important you do this, because if you simply upload the clone VMs I mentioned earlier to the datastore and &#8220;Add to Inventory&#8221;, the VMs will not boot and you&#8217;ll get nasty errors when powering on the VMs like:</span>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas; font-size: 9pt;">&#8220;VMware ESX cannot find the virtual disk &#8220;/mnt/cribsbiox/machine_templates/onefs_builds/b.7.1.0.34r.vga/isi-nvram.vmdk&#8221;. Verify the path is valid and try again.&#8221;<br /> </span>
</p>

  1. <span style="color: black;">Use <a href="https://www.vmware.com/go/download-converter">VMware vCenter Converter Standalone</a> to convert the VMs and upload them to your ESXi host.<br /> </span>
  2. <div>
      <span style="color: black;">Some quick tips:<br /> </span>
    </div>
    
      1. <span style="color: black;">Repeat the conversion steps for the number of nodes you want. So if you want 3 nodes, convert the same VM 3 times (and give it a new name each time).<br /> </span>
      2. <div>
          <span style="color: black;">The source Virtual Machine File you want is the vmx file highlighted above.<br /> </span>
        </div>
        
          *![](http://www.kabri.uk/wp-content/uploads/2014/05/051014_1433_Installingt2.png) <span style="color: black;"><br /> </span>
      3. <span style="color: black;">Name the VM the same as the hostname. For example: isilon-node-001<br /> </span>
      4. <div>
          <span style="color: black;">Change the VM version to Version 8. You don&#8217;t need anything higher, and you especially do not want to have a Version 10 VM with the free edition of ESXi as v10 VMs can only be managed from vSphere Web Client, which isn&#8217;t available for Free Edition of ESXi.<br /> </span>
        </div>
        
          *![](http://www.kabri.uk/wp-content/uploads/2014/05/051014_1433_Installingt3.png) <span style="color: black;"><br /> </span>
      5. <div>
          <span style="color: black;">Change all the disks to Thin provision if you want to save space (and speed up the conversion)<br /> </span>
        </div>
        
          *![](http://www.kabri.uk/wp-content/uploads/2014/05/051014_1433_Installingt4.png) <span style="color: black;"><br /> </span>
      6. <div>
          <span style="color: black;">Change the network for NIC1 to be the new vSwitch you created (e.g. IsilonInternal)<br /> </span>
        </div>
        
          *![](http://www.kabri.uk/wp-content/uploads/2014/05/051014_1433_Installingt5.png) <span style="color: black;"><br /> </span>

<span style="color: #1e4e79; font-size: 16pt;">Setting up the Isilon nodes<br /> </span>

  1. <div>
      <span style="color: black;">Power on each VM you&#8217;ve just created, and use the vSphere client to look at the Console of the VM itself (click on VM &#8211;> Console tab)<br /> </span>
    </div>
    
      *![](http://www.kabri.uk/wp-content/uploads/2014/05/051014_1433_Installingt6.png) <span style="color: black;"><br /> </span>
  2. <span style="color: black;">For configuring the nodes themselves, there&#8217;s a .pdf inside the .zip you extracted earlier which runs through how to setup the Isilon nodes. If you follow it from around page 9 onwards, you&#8217;ll be able to follow the configuration wizard and add the other nodes afterwards (it talks about formatting the drives). The whole setup of 3 nodes took me about 10 minutes. It&#8217;s really very easy!</span>

<p style="margin-left: 54pt;">
  <img src="http://www.kabri.uk/wp-content/uploads/2014/05/051014_1433_Installingt7.png" alt="" /><span style="color: black;"><br /> </span>
</p>

<span style="color: #1e4e79; font-size: 16pt;">Dashboard<br /> </span>

<span style="color: black;">And here&#8217;s what it looks like when you connect to the Dashboard post-configuration:</span>

<p style="margin-left: 27pt;">
  <img src="http://www.kabri.uk/wp-content/uploads/2014/05/051014_1433_Installingt8.png" alt="" /><span style="color: black;"><br /> </span>
</p>

<span style="color: #1e4e79; font-size: 16pt;">Comments/Feedback?<br /> </span>

<span style="color: black;">Let me know how you get on with this! I always welcome comments and feedback 🙂<br /> </span>

<span style="color: black;"><br /> </span>
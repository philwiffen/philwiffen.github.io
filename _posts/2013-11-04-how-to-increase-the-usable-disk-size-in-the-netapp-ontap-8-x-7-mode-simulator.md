---
id: 1116
title: How to increase the usable disk size in the NetApp ONTAP 8.x 7-mode Simulator
date: 2013-11-04T16:29:02+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=1116
permalink: /2013/11/04/how-to-increase-the-usable-disk-size-in-the-netapp-ontap-8-x-7-mode-simulator/
categories:
  - Home Lab
  - NetApp
  - Virtualisation
tags:
  - Brix
  - homelab
  - netapp
  - sim
  - simulator
  - vmware
---
<h1 style="margin-left: 2pt;">
  <span style="color: #17365d; font-size: 16pt;"><strong>Background</strong></span>
</h1>

<p style="margin-left: 2pt;">
  If you or your company own a NetApp Storage System, you can access and download the <a href="http://support.netapp.com/NOW/download/tools/simulator/ontap/8.0/">NetApp Simulator</a> &#8211; it&#8217;s basically a NetApp filer in a Virtual Machine. Very cool; and great for learning and experimenting in a Lab.
</p>

<h1 style="margin-left: 2pt;">
  <span style="color: #17365d; font-size: 16pt;"><strong>Why increase the disk size?</strong></span>
</h1>

<p style="margin-left: 2pt;">
  The Simulator, by default, presents you with 28 x 1GB disks, giving you a mere 28GB raw disk space.
</p>

<p style="margin-left: 2pt;">
  While this is fine for learning; I wanted to use it as the main SAN provider in my Virtualization home lab; where I plan to run an entire lab including ESXi hosts, a SAN appliance and networking inside a single small form factor computer.
</p>

<h1 style="margin-left: 2pt;">
  <span style="color: #17365d; font-size: 16pt;"><strong>Why not use Nexenta, or Openfiler, or FreeNAS?</strong></span>
</h1>

<p style="margin-left: 2pt;">
  Two reasons:
</p>

  1. I&#8217;m used to NetApp systems, and want to learn more
  2. <div>
      I can use NetApp&#8217;s Deduplication and Compression features to squeeze much more out of the limited SSD space inside my Gigabyte Brix.
    </div>

I tried Nexenta, but found it really slow and it also randomly hogged an entire CPU core for seemingly no reason.

<h1 style="margin-left: 2pt;">
  <span style="color: #17365d; font-size: 16pt;"><strong>Standing on the shoulders of giants</strong></span>
</h1>

<p style="margin-left: 2pt;">
  All of the information below is available and possible thanks to <a href="http://www.cosonok.com/2013/08/clustered-ontap-82-sim-maximizing.html">this post</a> from Vidad Cosonok, which covers how to create new larger disks in Cluster-Mode. The commands are different for 7-mode; hence this post. All credit however, should rest with Vidad Cosonok 🙂
</p>

<p style="margin-left: 2pt;">
  I believe that this method below is much easier and simpler than some of the alternatives, one involving <a href="https://communities.netapp.com/docs/DOC-9579">adding another 28 disks</a> (not enough) and another which <a href="http://www.wooditwork.com/2012/01/04/installing-maximising-the-netapp-ontap-8-1-simulator/">involves tweaking partitions with a FreeBSD boot disk</a>.
</p>

<h1 style="margin-left: 2pt;">
  <span style="color: #17365d; font-size: 16pt;"><strong>Increasing the size of the disks in the NetApp simulator</strong></span>
</h1>

<p style="margin-left: 2pt;">
  Following Vidad&#8217;s instructions, it&#8217;s possible to create a NetApp simulator with up to 400GB of raw disk space. PRetty impressive! In the example below, I only want to use a maximum of 224GB, so I&#8217;m choosing to use 4GB disks rather than 9GB disks. Note that going over 224GB can be a pain in VMware ESXi, as you&#8217;ll need to <a href="http://www.yellow-bricks.com/2012/11/07/resizing-an-ide-virtual-disk-part-two/">increase the size of an IDE disk</a>, which is non-trivial in ESXi.
</p>

<h2 style="margin-left: 2pt;">
  <span style="color: #366092; font-size: 13pt;"><strong>Setup the Simulator</strong></span>
</h2>

  1. Download and extract the ONTAP 7-mode [NetApp Simulator](http://support.netapp.com/NOW/download/tools/simulator/ontap/8.X/) (I went for 8.2, and this is tested working on 8.2).
  2. <div>
      Follow the <a href="http://support.netapp.com/knowledge/docs/simulate_ontap/Simulate_ONTAP_8.2_Installation_and_Setup_Guide.pdf">setup guide</a> to install it into your VMware environment.
    </div>
    
      * I installed it into ESXi using the VMware Converter to ensure that the VMDKs were thin provisioned as they went into the Brix&#8217;s local SSD datastore
  3. Boot the Virtual Machine
  4. Press Ctrl+C when prompted and choose option 4, to wipe the config and initialise the disks.
  5. <div>
      Once done, complete the first time setup (where you give it a hostname , IP, etc)
    </div>

## <span style="color: #366092; font-size: 13pt;"><strong>Delete the disks and re-create new ones</strong></span>

<p style="margin-left: 2pt;">
  Once you&#8217;ve configured the Simulator, follow these steps. I&#8217;d advise doing this from an SSH client, so you can copy/paste easily, rather than using the VMware console.
</p>

<p style="margin-left: 29pt;">
  <span style="font-family: Courier New;">priv set advanced<br /> </span><span style="font-family: Courier New;">useradmin diaguser unlock<br /> </span><span style="font-family: Courier New;">useradmin diaguser password<br /> </span><span style="font-family: Courier New;">systemshell</span><br /> <em>(login as diag, with password you just set)</em>
</p>

<p style="margin-left: 29pt;">
  <span style="font-family: Courier New;">setenv PATH &#8220;${PATH}:/usr/sbin&#8221;<br /> </span><span style="font-family: Courier New;">echo $PATH<br /> </span><span style="font-family: Courier New;">cd /sim/dev/,disks<br /> </span><span style="font-family: Courier New;">ls<br /> </span><span style="font-family: Courier New;">sudo rm v0*<br /> </span><span style="font-family: Courier New;">sudo rm v1*<br /> </span><span style="font-family: Courier New;">sudo rm ,reservations<br /> </span><span style="font-family: Courier New;">cd /sim/dev<br /> </span><span style="font-family: Courier New;">vsim_makedisks -h</span>
</p>

<p style="margin-left: 2pt;">
  Make a note of the options available for -t (type), as you may wish to deviate from what I&#8217;m doing.
</p>

<p style="margin-left: 2pt;">
  <em>To make ~224GB usable disks:</em>
</p>

<p style="margin-left: 29pt;">
  <span style="font-family: Courier New;">sudo vsim_makedisks -n 14 -t 31 -a 0<br /> </span><span style="font-family: Courier New;">sudo vsim_makedisks -n 14 -t 31 -a 1<br /> </span><span style="font-family: Courier New;">sudo vsim_makedisks -n 14 -t 31 -a 2<br /> </span><span style="font-family: Courier New;">sudo vsim_makedisks -n 14 -t 31 -a 3</span>
</p>

<p style="margin-left: 2pt;">
  <em>To make ~550GB of usable disks:</em>
</p>

<p style="margin-left: 29pt;">
  <span style="font-family: Courier New;">sudo vsim_makedisks -n 14 -t 36 -a 0<br /> </span><span style="font-family: Courier New;">sudo vsim_makedisks -n 14 -t 36 -a 1<br /> </span><span style="font-family: Courier New;">sudo vsim_makedisks -n 14 -t 36 -a 2<br /> </span><span style="font-family: Courier New;">sudo vsim_makedisks -n 14 -t 36 -a 3</span>
</p>

<p style="margin-left: 2pt;">
  Check they&#8217;re present, then exit and halt.
</p>

<p style="margin-left: 29pt;">
  <span style="font-family: Courier New;">ls ,disks/<br /> </span><span style="font-family: Courier New;">exit<br /> </span><span style="font-family: Courier New;">halt</span>
</p>

<h2 style="margin-left: 2pt;">
  <span style="color: #366092; font-size: 13pt;"><strong>Configuring the new disks for use</strong></span>
</h2>

  1. Power off the Simulator VM
  2. If you made your total disks larger than 224GB, you need to Edit the VM settings and make Hard Drive 4 550GB (rather than 250GB). If you&#8217;re doing this in vCenter/ESXi it [can be tricky](http://www.yellow-bricks.com/2012/11/07/resizing-an-ide-virtual-disk-part-two/) as the HDD is IDE rather than SCSI.
  3. Power on the Simulator VM
  4. Press Ctrl-C for Boot Menu when prompted
  5. Enter selection 5 &#8216;Maintenance mode boot&#8217;
  6. <div>
      Assign 3 disks for the Clustered ONTAP dedicated root aggregate, and halt
    </div>
    
    <span style="font-family: Courier New;">disk assign v4.16 v4.17 v4.18<br /> </span><span style="font-family: Courier New;">disk show<br /> </span><span style="font-family: Courier New;">halt</span></li> 
    
      * Power-cycle the Simulator
      * Press Ctrl-C for Boot Menu when prompted
      * Enter selection 4 &#8216;Clean configuration and initialize all disks&#8217; and answer &#8216;y&#8217; to the two prompts
      * Wait for the wipe/initialise to complete, then re-do the setup if needed.
      * <div>
          Log in to the system, and assign the disks, so they&#8217;re usable:
        </div>
        
        <span style="font-family: Courier New;">disk assign all</span></li> 
        
          * Now you can create a new aggregate/volume/qtree/LUN etc and use the Simulator to its full potential 🙂
          * At this stage, you may want to add the [Licences](http://support.netapp.com/NOW/download/tools/simulator/ontap/8.2/7Mode_licenses_8.2.0GA.txt), which include iSCSI and NFS. You can&#8217;t use iSCSI or NFS without installing the license (and for iSCSI, [enabling](https://library.netapp.com/ecmdocs/ECMP1196995/html/GUID-40D2EB15-C06A-474C-A073-142B8957EB11.html) and [starting the service](https://library.netapp.com/ecmdocs/ECMP1196995/html/GUID-FB7E308B-B333-42DC-99AB-47AF71B5E091.html)).</ol>
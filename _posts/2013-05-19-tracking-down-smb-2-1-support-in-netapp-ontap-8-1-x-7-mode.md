---
id: 918
title: Tracking down SMB 2.1 support in NetApp ONTAP 8.1.x 7-Mode
date: 2013-05-19T13:49:25+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=918
permalink: /2013/05/19/tracking-down-smb-2-1-support-in-netapp-ontap-8-1-x-7-mode/
categories:
  - NetApp
  - Storage
  - Windows
tags:
  - cifs
  - netapp
  - optimisation
  - optimization
  - smb
  - smb2
  - tuning
---
> **Abstract**
> 
> This blog post covers how I tracked down when SMB 2.1 support was re-enabled in ONTAP 8.1.x 7-mode, having been disabled in the initial release of 8.1.2.

# <!--more-->

# Tracking down SMB 2.1 support in 8.1.x 7-Mode

If you [follow me on twitter](https://twitter.com/phil_wiffen), you&#8217;ll be aware that I&#8217;m <del>relatively obsessed with</del> curious about SMB 2.1 support on NetApp&#8217;s ONTAP operating system. The reason for this is simple: in my benchmarks on ONTAP 8.1.1, SMB 2.1 noticeably outperformed SMB 2.0 when latencies were introduced.

## SMB 2.1 support in ONTAP 7-Mode &#8211; a quick history

**8.1.1**  
[SMB 2.1](http://technet.microsoft.com/en-us/library/ff625695(v=WS.10).aspx) support first arrived in ONTAP 8.1.1 7-mode. The performance over the SMB 2.0 implementation in ONTAP 8.0.x was noticeable over WAN. Sadly, the implementation of SMB 2.1 had some nasty bugs in it.

**8.1.2**  
SMB 2.1 support was [disabled in 8.1.2](https://library.netapp.com/ecmdocs/ECMP1147521/html/GUID-72E3B346-7095-49F2-A79B-3B6086185C5E.html). However, most of the documentation and release notes still alluded to SMB 2.1 features like oplocks leasing.

At this point, I didn&#8217;t know when SMB 2.1 was coming back, but I was keen to find out. After much digging, I found this nugget in a bug report:

> This issue is not present in the Data ONTAP 8.1.2 release even though the fix is not available in that release. That is because the 8.1.2 release has an option that disables the SMB 2.1 dialect, which disables SMB 2.1 leasing. **A subsequent 8.1.2** **release will contain the fix for this bug, and also will re-enable SMB 2.1.**
> 
> <http://support.netapp.com/NOW/cgi-bin/bol?Type=Detail&Display=642218>

From this point onwards, with every new &#8220;P&#8221; release of ONTAP 8.1.2 I was looking for news in the release notes that SMB2.1 has been re-enabled. I never found anything.

**8.1.3RC1**  
When 8.1.3RC1 was released last week, I still couldn&#8217;t find reference to SMB 2.1 being re-enabled. So I decided to start digging and testing.

## Digging for evidence

To find out if/when SMB 2.1 was re-enabled, I ran some tests against various ONTAP 7-Mode releases on my lab FAS3070.

For the tests below, I installed the stated ONTAP version, then ran the &#8220;Directory Copy&#8221; benchmark tests from Intel&#8217;s NASPT.

As far as I can tell, the only way to tell if SMB 2.1 is on, is to look for lease oplocks; a feature which is in SMB 2.1 but not SMB 2.0.

You can look at file lock status in SMB/CIFS by using the following command:

> `lock status -p cifs`

If _durable_handle=_ is shown blank, and _oplock=Lease-*_ then lease oplocks are in place &#8211; meaning SMB 2.1 is enabled. [[Reference](https://library.netapp.com/ecmdocs/ECMP1120826/html/GUID-BFA044CB-639C-4776-90FB-6EC9B9F5CEB6.html)]

### 8.1.1P2

SMB 2.1 is enabled

> `filer1> lock status -p cifs<br />
CIFS path=\NASPT\DirectoryCopyFromNAS\Copy Directory\dir\Templates\Presentation Designs\Watermark.pot(/vol/cifs_testing/cifs_testing/NASPT/DirectoryCopyFromNAS/Copy Directory/dir/Templates/Presentation Designs/Watermark.pot) host= owner= state=GRANTED mode=Oplock-Excl <strong>oplock=Lease-RWH</strong> fsid=0x02af81f5 fileid=0x00019df8 <strong>durable_state=</strong>`

### 8.1.2

SMB 2.1 is disabled

> `filer1> lock status -p cifs<br />
CIFS path=\NASPT\DirectoryCopyFromNAS\Copy Directory\dir\Templates\Presentation Designs\Slit.pot(/vol/cifs_testing/cifs_testing/NASPT/DirectoryCopyFromNAS/Copy Directory/dir/Templates/Presentation Designs/Slit.pot) host=10.0.14.193(W7SMBTEST) owner=philwiffen state=GRANTED mode=Oplock-Excl <strong>oplock=Oplock-Excl</strong> fsid=0x02af81f5 fileid=0x00019df5 <strong>durable_state=DH_GRANTED</strong>`

### **8.1.2P3**

SMB 2.1 is enabled

> `filer1> lock status -p cifs<br />
CIFS path=\NASPT\DirectoryCopyFromNAS\Copy Directory\dir\PROD\SAMPLES\app4\WRONGVER.XML(/vol/cifs_testing/cifs_testing/NASPT/DirectoryCopyFromNAS/Copy Directory/dir/PROD/SAMPLES/app4/WRONGVER.XML) host= owner= state=GRANTED mode=Oplock-Excl <strong>oplock=Lease-RWH</strong> fsid=0x02af81f5 fileid=0x0003f42d <strong>durable_state=</strong>`

### **8.1.2P4 **

SMB2.1 is enabled

> `filer1> lock status -p cifs<br />
CIFS path=\NASPT\DirectoryCopyToNAS\Copy Directory\dir\Templates\Presentation Designs\Digital Dots.pot(/vol/cifs_testing/cifs_testing/NASPT/DirectoryCopyToNAS/Copy Directory/dir/Templates/Presentation Designs/Digital Dots.pot) host= owner= state=GRANTED mode=Oplock-Excl <strong>oplock=Lease-RWH</strong> fsid=0x02af81f5 fileid=0x000281b4 <strong>durable_state=</strong>`

### 8.1.3RC1

SMB2.1 is enabled

> `filer1> lock status -p cifs<br />
CIFS path=\NASPT\DirectoryCopyToNAS\Copy Directory\dir\CLIPART\PUB60COR\PARNT_10.MID(/vol/cifs_testing/cifs_testing/NASPT/DirectoryCopyToNAS/Copy Directory/dir/CLIPART/PUB60COR/PARNT_10.MID) host= owner= state=GRANTED mode=Oplock-Excl <strong>oplock=Lease-RWH</strong> fsid=0x02af81f5 fileid=0x0004a559 <strong>durable_state=</strong>`

# Results

&nbsp;

<table border="1" cellspacing="0" cellpadding="0">
  <tr>
    <td valign="top" width="257">
      <strong><span style="font-size: medium;"><span style="font-family: Calibri;">ONTAP 7-Mode</span></span></strong>
    </td>
    
    <td valign="top" width="257">
      <strong><span style="font-size: medium;"><span style="font-family: Calibri;">SMB 2.1 Supported</span></span></strong>
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="257">
      <span style="font-size: medium;"><span style="font-family: Calibri;">8.1.1P2</span></span>
    </td>
    
    <td valign="top" width="257">
      <span style="font-family: Calibri; font-size: medium;">Yes</span>
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="257">
      <span style="font-size: medium;"><span style="font-family: Calibri;">8.1.2</span></span>
    </td>
    
    <td valign="top" width="257">
      <span style="font-family: Calibri; font-size: medium;">No</span>
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="257">
      <span style="font-size: medium;"><span style="font-family: Calibri;">8.1.2P3</span></span>
    </td>
    
    <td valign="top" width="257">
      <span style="font-family: Calibri; font-size: medium;">Yes</span>
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="257">
      <span style="font-size: medium;"><span style="font-family: Calibri;">8.1.2P4</span></span>
    </td>
    
    <td valign="top" width="257">
      <span style="font-family: Calibri; font-size: medium;">Yes</span>
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="257">
      <span style="font-size: medium;"><span style="font-family: Calibri;">8.1.3RC1</span></span>
    </td>
    
    <td valign="top" width="257">
      <span style="font-family: Calibri; font-size: medium;">Yes</span>
    </td>
  </tr>
</table>

&nbsp;

# Next Steps &#8211; Getting 8.1.2P3 or 8.1.2P4 with SMB 2.1 support

Now we know that SMB 2.1 is enabled in ONTAP 8.1.2P3 onwards, we need to get it.

When you visit support.netapp.com and go to download ONTAP software, you&#8217;ll generally be presented with the original version of 8.1.2, which we now know doesn&#8217;t have SMB 2.1 support.

To get a version with SMB 2.1 support go here:

  * [https://support.netapp.com/NOW/download/software/ontap/8.1.2P3/](https://support.netapp.com/NOW/download/software/ontap/8.1.2P4/)
  * <https://support.netapp.com/NOW/download/software/ontap/8.1.2P4/>

# Why the confusion?

My main confusion around this derives from Release Notes.

  * Release notes for 8.1.1 [specifically mention SMB 2.1 support](https://library.netapp.com/ecmdocs/ECMP1140403/html/GUID-5883ED0E-19F8-4F74-A433-ED1795BFF526.html): 
      * [<img loading="lazy" class="alignnone size-medium wp-image-922" alt="smb 2.1 enabled - 8.1.1" src="http://www.kabri.uk/wp-content/uploads/2013/05/smb-2.1-enabled-8.1.1-300x77.png" width="300" height="77" />](http://www.kabri.uk/wp-content/uploads/2013/05/smb-2.1-enabled-8.1.1.png)
  * Release notes for 8.1.2 [specifically mention](https://library.netapp.com/ecmdocs/ECMP1147521/html/GUID-9B625368-D648-4351-B611-1F9F2368F9AB.html) that SMB 2.1 support is disabled: 
      * [<img loading="lazy" class="alignnone size-medium wp-image-923" alt="smb 2.1 disabled - 8.1.2" src="http://www.kabri.uk/wp-content/uploads/2013/05/smb-2.1-disabled-8.1.2-300x101.png" width="300" height="101" />](http://www.kabri.uk/wp-content/uploads/2013/05/smb-2.1-disabled-8.1.2.png)
  * Release notes for 8.1.3 [make no mention](https://library.netapp.com/ecmdocs/ECMP1196459/html/GUID-D88F9A3E-7A4A-4659-BD62-B89925AA4620.html) of SMB 2.1 being re-enabled (even though this is a new point release, and as SMB 2.1 was disabled in the original 8.1.2 release it should probably mention that SMB 2.1 is back) 
      * [<img loading="lazy" class="alignnone size-medium wp-image-924" alt="ontap 8.1.3RC1 - no mention of smb 2.1" src="http://www.kabri.uk/wp-content/uploads/2013/05/ontap-8.1.3RC1-no-mention-of-smb-2.1-300x153.png" width="300" height="153" />](http://www.kabri.uk/wp-content/uploads/2013/05/ontap-8.1.3RC1-no-mention-of-smb-2.1.png)

Boot notes:

  * Those with sharp eyes may notice that the bug report specifically says &#8220;a subsequent release of 8.1.2 will re-enable SMB 2.1&#8221;. Which makes it relatively obvious that a P-release will re-enable SMB 2.1. However, I am convinced that when I first saw this bug report, it said &#8220;a subsequent release will re-enable SMB 2.1&#8221;, which is somewhat more vague. Wish I&#8217;d screenshotted it now 🙂
  * More information on SMB 2.0 and SMB 2.1 is here: <http://technet.microsoft.com/en-us/library/ff625695(v=WS.10).aspx>
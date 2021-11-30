---
id: 1224
title: Getting Started with the NetApp PowerShell Toolkit
date: 2014-07-12T14:16:33+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=1224
permalink: /2014/07/12/getting-started-with-the-netapp-powershell-toolkit/
categories:
  - NetApp
  - PowerShell
---
<span style="color: #1e4e79; font-size: 16pt;">Scope </span>

<span style="color: #17365d;">This post takes a quick look at the NetApp PowerShell Toolkit: a set of PowerShell cmdlets which can be used to query and change settings on NetApp Storage Systems, paving the way for automation of common tasks or generating regular reports. It runs through installing the PowerShell toolkit, and running a few basic commands against a NetApp storage system.<br /> </span>

<p style="margin-left: 27pt;">
  <img src="http://www.kabri.uk/wp-content/uploads/2014/07/071214_1316_GettingStar1.png" alt="" /><span style="color: black;"><br /> </span>
</p>

<!--more-->

<span style="color: #1e4e79; font-size: 16pt;">Resources<br /> </span>

<span style="color: black;">The following resources will be of use. You&#8217;ll need a NetApp &#8220;NOW&#8221; account to download things. It&#8217;s free to sign up, but according to NetApp you&#8217;ll need to be a customer or a partner to download the Toolkit.<br /> </span>

  * <span style="color: black;">Overview: <a href="https://communities.netapp.com/docs/DOC-8111">NetApp Data ONTAP PowerShell Toolkit overview</a><br /> </span>
  * <span style="color: black;">Presentation: <a href="https://communities.netapp.com/docs/DOC-6162">Presentation on Data ONTAP PowerShell Toolkit</a><br /> </span>
  * <span style="color: black;">Toolkit Download: <a href="https://communities.netapp.com/docs/DOC-6138">PowerShell Toolkit for NetApp download page</a><br /> </span>

<span style="color: #1e4e79; font-size: 16pt;">Pre-requisites<br /> </span>

<span style="color: black;">You will need:<br /> </span>

  * <span style="color: black;">PowerShell 2.0 or higher installed on your Windows system (Windows 7/Server 2008 R2 has PowerShell 2.0 installed out of the box)<br /> </span>
  * <span style="color: black;">The NetApp PowerShell Toolkit <a href="https://communities.netapp.com/docs/DOC-6138">DataONTAP.zip file</a><br /> </span>

<span style="color: #1e4e79; font-size: 16pt;">Install the NetApp PowerShell Toolkit and adding the modules<br /> </span>

<span style="color: black;">Extract the downloaded DataONTAP.zip to:<br /> </span>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">%SYSTEMROOT%\system32\WindowsPowerShell\v1.0\Modules\<br /> </span>
</p>

<span style="color: black;">The files should end up inside:<span style="font-family: Consolas;"> %SYSTEMROOT%\system32\WindowsPowerShell\v1.0\Modules\DataONTAP</span><br /> </span>

<span style="color: black;">Note: On a multi-user system, if you want the toolkit to be available for only yourself, place it inside: %USERPROFILE%\Documents\WindowsPowerShell\Modules\<br /> </span>

<span style="color: black;">Start PowerShell and run:<br /> </span>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">import-module DATAONTAP<br /> </span>
</p>

<span style="color: black;">Optional: Add the import-module DataONTAP command to your profile (so it&#8217;s available every time you use PowerShell):<br /> </span>

<p style="margin-left: 27pt;">
  <span style="color: black;">Where is our profile?:<br /> </span>
</p>

<p style="margin-left: 54pt;">
  <span style="color: black; font-family: Consolas;">$profile<br /> </span>
</p>

<p style="margin-left: 27pt;">
  <span style="color: black;">Does that profile exist?:<br /> </span>
</p>

<p style="margin-left: 54pt;">
  <span style="color: black; font-family: Consolas;">test-path $profile<br /> </span>
</p>

<p style="margin-left: 27pt;">
  <span style="color: black;">If True, skip the &#8220;If False&#8221; step and move to notepad $profile.<br /> </span>
</p>

<p style="margin-left: 27pt;">
  <span style="color: black;">If False, run:<br /> </span>
</p>

<p style="margin-left: 54pt;">
  <span style="color: black; font-family: Consolas;">new-item $profile -itemtype file -force<br /> </span>
</p>

<p style="margin-left: 27pt;">
  <span style="color: black;">Edit the file:<br /> </span>
</p>

<p style="margin-left: 54pt;">
  <span style="color: black; font-family: Consolas;">notepad $profile<br /> </span>
</p>

<p style="margin-left: 27pt;">
  <span style="color: black;">Add the following line to the ps1 file:<br /> </span>
</p>

<p style="margin-left: 54pt;">
  <span style="color: black; font-family: Consolas;">import-module DataONTAP<br /> </span>
</p>

<p style="margin-left: 27pt;">
  <span style="color: black;">Save the file. You&#8217;ll now import the DataONTAP PowerShell modules every time you start PowerShell!<br /> </span>
</p>

<span style="color: #1e4e79; font-size: 16pt;">Getting help<br /> </span>

<span style="color: black;">One of the most important functions in PowerShell &#8211; or any command-line shell &#8211; is the ability to get help. You&#8217;ll find this invaluable as you work your way around PowerShell and the NetApp toolkit (I certainly have!).<br /> </span>

<span style="color: black;">To view the list of cmdlets available from the NetApp toolkit:<br /> </span>

<p style="margin-left: 54pt;">
  <span style="color: black; font-family: Consolas;">Get-NaHelp</span>
</p>

<span style="color: black;">Use -Category switch and/or wildcards to narrow the results. For example:<br /> </span>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">Get-NaHelp -Category volume<br /> </span>
</p>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">Get-NaHelp -Category options<br /> </span>
</p>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">Get-NaHelp *NaCredential<br /> </span>
</p>

<span style="color: black;">To see help for a specific cmdlet (command):<br /> </span>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">Get-Help Connect-NaController<br /> </span>
</p>

<span style="color: black;">For full details of a cmdlet, including examples:<br /> </span>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">Get-Help Connect-NaController -full<br /> </span>
</p>

<span style="color: #1e4e79; font-size: 16pt;">Authenticating and connecting to a NetApp storage system<br /> </span>  
<span style="color: black;">Before you can run commands/queries against a storage system, you need to connect to it and authenticate to it.<br /> </span>  
<span style="color: #2e75b5; font-size: 14pt;">Add login credentials for the session<br /> </span>  
<span style="color: black;">The Add-NaCredential cmdlet caches credentials for a storage system. This can be useful if you manage many storage systems, potentially each with different credentials. When you come to connect to a storage system using Connect-NaController, the connection will authenticate with the information held in the auth cache (pretty neat!).<br /> </span>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">Add-NaCredential -Name <hostname> -Credential <username><br /> </span>
</p>

<span style="color: black;">For example:<br /> </span>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">Add-NaCredential -Name cylon82 -Credential root<br /> </span>
</p>

<span style="color: black;">Alternatively, just use -Credential with the Connect-NAController command, if using a single NetApp controller<br /> </span>  
<span style="color: black;">To see current credential list:<br /> </span>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">Get-NaCredential<br /> </span>
</p>

<span style="color: black;">For example:<br /> </span>

<p style="margin-left: 27pt;">
  <img src="http://www.kabri.uk/wp-content/uploads/2014/07/071214_1316_GettingStar2.png" alt="" /><span style="color: black;"><br /> </span>
</p>

<span style="color: #2e75b5; font-size: 14pt;">Connecting to a single NetApp controller<br /> </span>

<span style="color: black;">Now you can open a connection to a Netapp controller to run some commands against it.<br /> </span>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">Connect-NaController -Name cylon82<br /> </span>
</p>

<span style="color: black;">Or if you didn&#8217;t specify authentication credentials earlier, try:<br /> </span>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">Connect-NaController -Name cylon82 -Credential root<br /> </span>
</p>

<span style="color: black;">For example:<br /> </span>

<p style="margin-left: 27pt;">
  <img src="http://www.kabri.uk/wp-content/uploads/2014/07/071214_1316_GettingStar3.png" alt="" /><span style="color: black;"><br /> </span>
</p>

<span style="color: #1e4e79; font-size: 16pt;">Basic usage<br /> </span>

<span style="color: black;">To get started, let&#8217;s take a look at a few very basic commands.<br /> </span>  
<span style="color: #2e75b5; font-size: 14pt;">Get System Information from the NetApp controller you&#8217;ve connected to<br /> </span>

<span style="color: black;">OK, now you&#8217;re connected, run a few sample commands to get a feel for how this works.<br /> </span>  
<span style="color: black;">Let&#8217;s look at some basic system information:<br /> </span>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">get-nasystemversion<br /> </span>
</p>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">get-nasysteminfo<br /> </span>
</p>

<p style="margin-left: 27pt;">
  <img src="http://www.kabri.uk/wp-content/uploads/2014/07/071214_1316_GettingStar4.png" alt="" /><span style="color: black;"><br /> </span>
</p>

<span style="color: #2e75b5; font-size: 14pt;">Volume information<br /> </span>

<span style="color: black;">Alright, now let&#8217;s take a look at the volumes on the system.<br /> </span>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">Get-NaVol<br /> </span>
</p>

<p style="margin-left: 27pt;">
  <img src="http://www.kabri.uk/wp-content/uploads/2014/07/071214_1316_GettingStar5.png" alt="" /><span style="color: black;"><br /> </span>
</p>

<span style="color: black;">It&#8217;s also possible to roll up two commands to run one after the other, using the semi-colon separator &#8220;;&#8221;, for example:<br /> </span>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">Get-NaVolContainer ; Get-NaVol | format-table<br /> </span>
</p>

<p style="margin-left: 27pt;">
  <img src="http://www.kabri.uk/wp-content/uploads/2014/07/071214_1316_GettingStar6.png" alt="" /><span style="color: black;"><br /> </span>
</p>

<span style="color: #1e4e79; font-size: 16pt;">It&#8217;s powerful, too!<br /> </span><span style="color: black;">With the power of PowerShell, we can do some really neat things. Take these two for example:<br /> </span>  
<span style="color: #2e75b5; font-size: 14pt;">How many shelves are connected to my system?<br /> </span><span style="color: black;"><span style="color: #808080;">*This only works on a real NetApp storage system. It won&#8217;t work on a NetApp Simulator, sorry.</span><br /> </span>  
<span style="color: black;">Normal command:<br /> </span>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">Get-NaShelf<br /> </span>
</p>

<span style="color: black;">Advanced:<br /> </span>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">Get-NaShelf | Sort ID -Unique | Select ID,Status,Name | Format-Table<br /> </span>
</p>

<span style="color: black;">This advanced command:<br /> </span>

  1. <span style="color: black;">Runs the Get-NaShelf command<br /> </span>
  2. <span style="color: black;">Sorts the output by Column ID (so they&#8217;re in order) and removes duplicates from the column. This is useful as Get-NaShelf outputs details for both channels of a shelf ID if you&#8217;re using Multipath cabling.<br /> </span>
  3. <span style="color: black;">Selects only the headers ID, Status and Name.<br /> </span>
  4. <span style="color: black;">and then outputs the results into a formatted Table.<br /> </span>

<img loading="lazy" class="alignnone size-large wp-image-1234" src="http://www.kabri.uk/wp-content/uploads/2014/07/list-shelves-powershell-1024x268.png" alt="list shelves - powershell" width="625" height="163" /> 

<span style="color: #2e75b5; font-size: 14pt;">Setting many options in one go<br /> </span>  
<span style="color: black;">As above, it&#8217;s possible to run a number of commands on a single line. In the example below, I&#8217;m setting some CIFS/SMB options on a test storage system:<br /> </span>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">set-naoption cifs.smb2.enable on ; set-naoption cifs.smb2.client.enable on ; set-naoption cifs.tcp_window_size 64240 ; set-naoption cifs.oplocks.enable on<br /> </span>
</p>

<p style="margin-left: 27pt;">
  <img src="http://www.kabri.uk/wp-content/uploads/2014/07/071214_1316_GettingStar7.png" alt="" /><span style="color: black;"><br /> </span>
</p>

<span style="color: black;">This command:<br /> </span>

  1. <span style="color: black;">Runs many set-naoption commands on a single line (separate by semi-colon &#8220;;&#8221;).<br /> </span>
  2. <span style="color: black;">This makes it easier to see what&#8217;s been run on the filer after the commands complete, as they all appear in a single block<br /> </span>

<span style="color: #1e4e79; font-size: 16pt;">How was that?</span>

<span style="color: black;">How did you find that?<br /> </span>  
<span style="color: black;">I was amazed at how easy it is to pick up and play with, given an hour or so initially. I really like the potential of the toolkit for automation some of my SMB benchmarking tasks, so I&#8217;ll be looking at that over the next few weeks.<br /> </span>  
<span style="color: black;">As always, I encourage and welcome feedback. So drop me a note in the comments! 🙂<br /> </span>  
<span style="color: #1e4e79; font-size: 16pt;">Next steps<br /> </span><span style="color: #17365d;">As you can see, the toolkit is very powerful; and I&#8217;ve barely scratched the surface! Take a look at all the options available to you by running:<br /> </span>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">Get-NaHelp<br /> </span>
</p>

<p style="margin-left: 27pt;">
  <span style="color: #17365d;">And for each interesting option, you can get more information by running:<br /> </span>
</p>

<p style="margin-left: 27pt;">
  <span style="color: black; font-family: Consolas;">Get-Help <cmdlet name><br /> </span>
</p>

<span style="color: #17365d;">In my next blog, I&#8217;ll take a look at how you can authenticate and connect to many NetApp controllers and run commands against them all: <a title="Connecting to multiple storage systems with the NetApp PowerShell Toolkit" href="http://www.kabri.uk/2014/07/23/connecting-to-multiple-storage-systems-with-the-netapp-powershell-toolkit/">Connecting to multiple storage systems with the NetApp PowerShell Toolkit</a><br /> </span>
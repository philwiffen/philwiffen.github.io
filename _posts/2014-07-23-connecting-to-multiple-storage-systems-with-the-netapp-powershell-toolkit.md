---
id: 1252
title: Connecting to multiple storage systems with the NetApp PowerShell Toolkit
date: 2014-07-23T12:28:38+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=1252
permalink: /2014/07/23/connecting-to-multiple-storage-systems-with-the-netapp-powershell-toolkit/
categories:
  - NetApp
  - PowerShell
---
<span style="color: #1e4e79; font-size: 16pt;">Scope<br /> </span>

<span style="color: black;">This post discusses methods to connect to multiple NetApp Storage Systems using the NetApp PowerShell Toolkit, and then execute commands against those storage systems<br /> </span>

<!--more-->

<span style="color: #1e4e79; font-size: 16pt;">Background<br /> </span>

<span style="color: black;">OK, so you&#8217;ve <a title="Getting Started with the NetApp PowerShell Toolkit" href="http://www.kabri.uk/2014/07/12/getting-started-with-the-netapp-powershell-toolkit/">setup the NetApp PowerShell Toolkit</a>, and you can connect to a storage system and run some commands. But what if you have more than one storage system?<br /> </span>

<span style="color: #1e4e79; font-size: 16pt;">Conceptual overview<br /> </span>

<span style="color: black;">As with all things scripting, there&#8217;s many ways to achieve this, but here&#8217;s roughly what I&#8217;ll be blogging about below:<br /> </span>

  1. <div>
      <span style="color: black;">Gettting a list of storage systems:<br /> </span>
    </div>
    
      1. <span style="color: black;">Via Text File: Keep an easily-accessible text file up to date with all your storage systems<br /> </span>
      2. <span style="color: black;">By enumerating from Active Directory: Query AD to get a list of all your storage systems (providing they&#8217;re in AD!)<br /> </span>
  2. <span style="color: black;">Setup authentication details for all the storage systems<br /> </span>
  3. <div>
      <span style="color: black;">Connect to the systems and run commands<br /> </span>
    </div>

<span style="color: #1e4e79; font-size: 16pt;">Getting a list of storage systems<br /> </span>

<span style="color: #2e75b5; font-size: 14pt;">Text file method<br /> </span>

<span style="color: black;">This is the simplest and sweetest method, but doesn&#8217;t scale too well in a large organisation, so buyer beware 😉<br /> </span>

<span style="color: black;">Create a text file in an easily accessible location, such as your home directory or Desktop and populate it with a carriage-returned list of hostnames. For example:<br /> </span>

<pre style="margin-left: 27pt;">cylon82
cylon814
&lt;/span></pre>

<span style="color: black;">Knowing where the text file is located, we can now setup the base for our PowerShell script:<br /> </span>

<pre class="brush:powershell">Where's the list?
$ListLocation = "C:\Users\Phil\Desktop\filers.txt"
#Read the contents of the list into an array
$FilerList = Get-Content $ListLocation
</pre>

<span style="color: black;">Now, to see what&#8217;s inside the $<span style="font-family: Courier New;">FilerList</span> array, just type:<br /> </span>

<pre class="brush:powershell" style="margin-left: 27pt;">echo $FilerList
</pre>

<span style="color: black;">You should now see a list of NetApp Storage Systems, like so:<br /> </span>

<p style="margin-left: 27pt;">
  <img src="http://www.kabri.uk/wp-content/uploads/2014/07/072214_2158_Connectingt1.png" alt="" /><span style="color: black;"><br /> </span>
</p>

<span style="color: #2e75b5; font-size: 14pt;">Enumerate from Active Directory<br /> </span>

<span style="color: black;">Another way to get a more dynamic list of storage systems is to use an Active Directory lookup<br /> </span>

<span style="color: black;">In the example below, all the storage systems are called roughly the same thing. Many organisations have naming schemes, such as: na-site-number (for example, na-cbg-001). If you always call your storage systems the same thing, you can query AD and locate all your filers, like so:<br /> </span>

<pre class="brush:powershell">import-module ActiveDirectory
 #what are we searching for?
 $FilerNameScheme = "na-site-*"
 #Let's query AD for systems with a name like $FilerNameScheme, and filter only Enabled accounts, and then only show the shortname for the host
 $FilerList = Get-ADComputer -Filter {(Name -like $FilerNameScheme) -and (Enabled -eq "True")} | Select -Expand Name</pre>

<span style="color: black;">Now, to see what&#8217;s inside the $<span style="font-family: Courier New;">FilerList</span> array, just type:<br /> </span>

<pre class="brush:powershell" style="margin-left: 27pt;">echo $FilerList
</pre>

<span style="color: black;">You should now see a list of NetApp Storage Systems!<br /> </span>

<span style="color: #1e4e79; font-size: 16pt;">Authenticating against multiple storage systems<br /> </span>

<span style="color: black;">OK great. Now that we have a list of storage systems, we can use the $FilerList array to authenticate to all the storage systems:<br /> </span>

<pre class="brush:powershell">#Let's setup the login credentials we'll be using for the storage systems
 $authentication = Get-Credential
 
 foreach ($filer in $FilerList) { 
 
 #add authentication for this filer, using the credentials we just entered
 Add-NaCredential -Name $filer -Credential $authentication 
 
 }</pre>

<span style="color: black;">At this point, you&#8217;ll be shown a list of all storage systems with authentication credentials stored.<br /> </span>

<span style="color: black;">For example:<br /> </span>

<p style="margin-left: 27pt;">
  <img src="http://www.kabri.uk/wp-content/uploads/2014/07/072214_2158_Connectingt2.png" alt="" /><span style="color: black;"><br /> </span>
</p>

<span style="color: #1e4e79; font-size: 16pt;">Running Commands<br /> </span>

<span style="color: black;">Now that you&#8217;ve got a list of filers inside the $FilerList array and credentials queued up, you can start to run commands against them all using the simple template below. I&#8217;ll throw some examples in too, in case it helps:<br /> </span>

<pre  class="brush:powershell">#for each entry in the list, run these commands…
 foreach ($filer in $FilerList) { 
 
 #connect to the storage system
 Connect-NaController -Name $filer
 
 #Put your commands here, for example...
 #show system version
 get-nasystemversion | format-table
 #show volumes and aggrs
 Get-NaVolContainer ; Get-NaVol | format-table
 # show me the following options settings
 get-naoption cifs.smb2.enable cifs.smb2.client.enable cifs.tcp_window_size cifs.oplocks.enable
 

}</pre>

<span style="color: #1e4e79; font-size: 16pt;">Putting it all together<br /> </span>

<span style="color: black;">Here&#8217;s an example of a full script which uses a text file for a list of filers, sets up login credentials, and then runs a few commands against each system.<br /> </span>

<pre  class="brush:powershell">#Where's the list?
$ListLocation = "C:\Users\Phil\Desktop\filers.txt"
#Read the contents of the list into an array
$FilerList = Get-Content $ListLocation

#Let's setup the login credentials we'll be using for the storage systems
$authentication = Get-Credential

foreach ($filer in $FilerList) { 
 
#add authentication for this filer, using the credentials we just entered
Add-NaCredential -Name $filer -Credential $authentication 
 
}

#for each entry in the list, run these commands...
foreach ($filer in $FilerList) { 
 
 #connect to the storage system
 Connect-NaController -Name $filer
 echo "Connecting to $filer"
 #show system version
 get-nasystemversion | format-table
 #show volumes and aggrs
 Get-NaVolContainer ; Get-NaVol | format-table
 # show me the following options settings
 get-naoption cifs.smb2.enable cifs.smb2.client.enable cifs.tcp_window_size cifs.oplocks.enable
 
}
</pre>

<span style="color: black;">And finally, here&#8217;s an example of the output you&#8217;d see:<br /> </span>

![](http://www.kabri.uk/wp-content/uploads/2014/07/072214_2158_Connectingt3.png) 

# <span style="color: black;">How was that? </span>

<span style="color: black;">How was that? Let me know in the comments what you&#8217;re using it for. I&#8217;d love to know! 🙂<br /> </span>

<span style="color: black;"><br /> </span>
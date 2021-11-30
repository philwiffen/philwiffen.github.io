---
id: 1307
title: 'Remove snapmirror relationships en-mass with NetApp&#8217;s PowerShell tools'
date: 2015-07-16T13:47:34+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=1307
permalink: /2015/07/16/remove-snapmirror-relationships-en-mass-with-netapps-powershell-tools/
categories:
  - NetApp
  - PowerShell
  - Storage
---
Anyone who&#8217;s tried to remove Snapmirror relationships using the NetApp commandline knows how painful it is. Recently, I had a need to remove all snapmirror relationships from a number of NetApp storage systems and figured I&#8217;d play with NetApp&#8217;s PowerShell toolkit to see if I could semi-automate the process.

<!--more-->

Below are some notes and some code snippets that may help if you ever need to do this yourself.

# Environment Setup

If you haven&#8217;t got them already, download and install [PowerShell 4.0](http://www.microsoft.com/en-gb/download/details.aspx?id=40855) and the latest [NetApp DATAONTAP Powershell toolkit](http://mysupport.netapp.com/NOW/download/tools/powershell_toolkit/)

Open up PowerShell and run:

<pre>import-module DATAONTAP</pre>

<p lang="en-GB">
  If you get an error about not being able to execute scripts, run:
</p>

<pre lang="en-GB"> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned</pre>

# Scenario

I have a number of storage systems, each with many snapmirror relationships with other storage systems. All storage systems will accept the same credentials. I want to remove all snapmirror relationships associated with the destination storage systems.

We&#8217;ll be using the following NetApp cmdlets:

<pre>Connect-NaController
Get-NaSnapmirror
Invoke-nasnapmirrorquiesce
Remove-NaSnapmirror</pre>

To find out more about these use:

<pre>get-help &lt;cmdlet name&gt; -full</pre>

# Scripting

First, you may wish to setup an authentication token. I like using this method as it&#8217;s relatively secure, and doesn&#8217;t involve embedding passwords into scripts

<pre>$authentication = Get-Credential</pre>

This asks for the credentials via an authentication popup, and stores those credentials in a new variable called $authentication that we can pass to the -Credential parameter when connecting to a storage system later on. Lovely.

Let&#8217;s connect to our destination storage system (that is, the one whose snapmirror relationships we want to <del>kill with fire</del> remove cleanly)

<pre lang="en-GB">Connect-NaController -Name &lt;storage system name&gt; -Credential $authentication</pre>

<p lang="en-GB">
  OK, now, we need to get a list of all the snapmirror relationships on the storage system and pass those results to the command that will quiesce all of those relationships
</p>

<pre lang="en-GB">Get-NaSnapmirror | foreach-object { invoke-nasnapmirrorquiesce -Destination $_.Destination }</pre>

<p lang="en-GB">
  This may take a while.
</p>

Once it&#8217;s done, this next code snippet will get that same list of snapmirror relationships and then:

  1. Grab the object in the Source field and use Regular Expressions to isolate the source storage system and put it in its own variable
  2. Pass that source storage system variable as well as the Source and Destination details to the Remove-NaSnapmirror cmdlet
  3. Use the authentication token to authenticate against the source storage system (in order to release the snapmirror relationship)

<pre lang="en-GB">Get-NaSnapmirror | foreach-object {
#remove all characters after the : from the output of the source. This gives us the filer name that we can then pass to the Remove-nasnapmirror command
$sourcefiler = $_.Source -Replace '\:.*'
Remove-NaSnapmirror -destination $_.Destination -source $_.Source -sourcecontroller (connect-nacontroller $sourcefiler -credential $authentication -transient)
}</pre>

<p lang="en-GB">
  For every relationship to be removed, you&#8217;ll be asked if that&#8217;s really what you want to do. For safety&#8217;s sake, leave that in place. If you&#8217;re feeling cavalier, you can automatically say yes to that prompt by replacing the above Remove-NaSnapmirror line with:
</p>

<pre lang="en-GB">Remove-NaSnapmirror -destination $_.Destination -source $_.Source -sourcecontroller (connect-nacontroller $sourcefiler -credential $authentication -transient) -confirm:$false</pre>

<p lang="en-GB">
  Your mileage may vary. Let me know how you get on!
</p>

<p lang="en-GB">
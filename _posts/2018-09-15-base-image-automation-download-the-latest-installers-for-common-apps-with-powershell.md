---
id: 1545
title: 'Base image automation &#8211; download the latest installers for common apps with PowerShell'
date: 2018-09-15T10:59:50+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://kabri.uk/?p=1545
permalink: /2018/09/15/base-image-automation-download-the-latest-installers-for-common-apps-with-powershell/
categories:
  - Automation
  - Citrix
  - PowerShell
  - Scripting
---
## Overview

Long overdue, and [inspired](https://twitter.com/CIT_Bronson/status/1040362979009744898) by [@xenappblog](https://twitter.com/xenappblog) and [@CIT_Bronson](https://twitter.com/CIT_Bronson), I&#8217;m finally documenting this.

In the Citrix [RTST environment](https://www.citrix.com/blogs/2017/07/10/the-secret-citrix-sysadmins/), we are frequently updating our base images with the latest common apps. To help with this, I cobbled together some scripts that will grab the latest version of apps like Chrome Enterprise, Firefox, VLC, Visual Studio Code, NotePad++, and FileZilla.

## PowerShell Scripts

Below is a list of super-basic PowerShell snippets that will get the latest versions of software commonly installed on base images in a Citrix <del>XenApp</del>-Virtual Apps and Desktops-type environment. They include the URLs used; useful if you just need the URLs for your own purposes.

The key to all of these is the URLs used &#8211; most installers have special URLs you can use to get the latest installer, but the challenge is finding them!

Some of the techniques used in these scripts may be useful to help build scripts for other apps you may need for your environment.

You&#8217;ll need to change $output or -OutFile location to match where you want the installer to be saved.

### Get Latest Google Chrome Enterprise

This will get you the latest stable build of Enterprise Google Chrome:

<pre class="">#direct download link:
$uri = "https://dl.google.com/tag/s/lang=en&browser=3&usagestats=0&appname=Google%20Chrome&needsadmin=true&ap=x64-stable-statsdef_1&brand=GCEA/dl/chrome/install/googlechromestandaloneenterprise64.msi"

#Where to put the file?
$output = "\\your\own\uncpath\Google Chrome\googlechromestandaloneenterprise64.msi"

#send the request, download the file
Invoke-WebRequest -Uri $uri -OutFile $output</pre>

### Get Latest Firefox

<pre class="">Invoke-WebRequest -Uri "https://download.mozilla.org/?product=firefox-latest&os=win64&lang=en-GB" -OutFile "\\your\own\uncpath\Firefox\Firefox Setup.exe"</pre>

### Get Latest VLC

<pre class="">#location to search
# VLC has a special "last" symlink which links to the latest version
$uri = "http://download.videolan.org/pub/videolan/vlc/last/win64/"

#Where to put the file?
$output = "\\your\own\uncpath\VLC Player\vlc-win64.exe"

#what filename do you want to match?
$pattern = "*-win64.exe"

# search the page for links that match -win64.exe, which is the only file we want/need.
$getFileName = (Invoke-WebRequest -Uri $uri).Links.href | Where-Object {$_ -like "$pattern"}

# pass that result to another webrequest to get the file
Invoke-WebRequest -Uri "$uri/$getFileName" -OutFile $output</pre>

### Get Latest Visual Studio Code

<pre>#direct download link for VS Code:
$uri = "https://go.microsoft.com/fwlink/?Linkid=852157"

#Where to put the file?
$output = "\\your\own\uncpath\VisualStudioCode\VSCodeSetup-x64.exe"

#send the request, download the file
Invoke-WebRequest -Uri $uri -OutFile $output</pre>

### Get Latest NotePad++

<pre class="">#URL to search:
$uri = "http://notepad-plus-plus.org/download/"
$baseUri = "http://notepad-plus-plus.org/"

#Where to put the file?
$output = "\\your\own\uncpath\Notepad++\npp.Installer.x64.exe"

#what filename do you want to match?
$pattern = "*Installer.x64.exe"

# set TLS to something more secure, otherwise we get error: Could not create SSL/TLS secure channel
[Net.ServicePointManager]::SecurityProtocol = "Tls12, Tls11, Tls, Ssl3"

#have to pass user agent because some sites act differently if you don't look like a browser
$userAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::FireFox

# search the page for links that match the pattern, which is the only file we want/need.
#Invoke-WebRequest -Uri $uri -UserAgent $userAgent
$getFileName = (Invoke-WebRequest -Uri $uri -UserAgent $userAgent).Links.href | Where-Object {$_ -like "$pattern"}
# pass that result to another webrequest to get the file
Invoke-WebRequest -Uri "$baseUri/$getFileName" -UserAgent $userAgent -OutFile $output</pre>

### Get Latest FileZilla

<pre>#Will always grab the latest FileZilla 64-bit installer
Invoke-WebRequest -Uri "https://download.filezilla-project.org/client/FileZilla_latest_win64-setup.exe" -OutFile "\\your\own\uncpath\FileZilla\FileZilla_win64-setup.exe"</pre>

## Other resources

The End-User Computer (EUC) community, including Citrix Technology Professionals (CTPs) are already sharing their techniques for getting other apps, including Adobe Reader DC, XenServer tools, and Firefox. If you&#8217;ve got something to share, let me know in the comments and I&#8217;ll get it added!

  * [Adobe Reader DC](https://xenappblog.com/2018/adobe-acrobat-reader-dc/)
  * [XenServer tools](https://xenappblog.com/2018/download-and-install-latest-citrix-xenserver-tools/)
  * [Firefox](https://xenappblog.com/2018/download-and-install-latest-mozilla-firefox/)

<p class="">
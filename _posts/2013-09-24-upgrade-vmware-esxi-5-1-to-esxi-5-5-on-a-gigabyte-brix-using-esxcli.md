---
id: 1092
title: Upgrade VMware ESXi 5.1 to ESXi 5.5 on a Gigabyte Brix using esxcli
date: 2013-09-24T00:06:40+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=1092
permalink: /2013/09/24/upgrade-vmware-esxi-5-1-to-esxi-5-5-on-a-gigabyte-brix-using-esxcli/
categories:
  - Gigabyte Brix
  - Home Lab
  - Virtualisation
---
# Background

Between ESX 5.1 and ESXi 5.5, VMware removed the bundled driver for the Realtek RTL8111E NIC, which is embedded in the Gigabyte Brix.

This means that if you try to boot a normal ESXi 5.5 installer, it won&#8217;t find the NIC driver and will refuse to install/upgrade your ESXi 5.1 instance.

<!--more-->

# How to upgrade

To get around this limitation, you can do one of two things:

  1. Upgrade by [creating an ESXi 5.5 install ISO](http://www.kabri.uk/2013/09/23/installing-vmware-esxi-5-5-on-the-gigabyte-brix/ "Installing VMware ESXi 5.5 on the Gigabyte Brix") that includes the net-r8168 driver package
  2. Upgrade directly via the esxcli command-line (which is what this guide covers)

# Upgrading via the command line

## Pre-requisites

If you want to do this remotely, you&#8217;ll need to enable SSH on the Brix. You can do this via the console, or if you run your Brix headless, you can do it via PowerCLI with these commands:

<pre>$esxihost="YourEsxiServerHostName"
Connect-viserver $esxihost
Start-VMHostService -HostService (Get-VMHost -Name $esxihost | Get-VMHostService | Where { $_.Key -eq "TSM-SSH"} )</pre>

## Performing the upgrade

Either from the console, or a SSH connection to the ESXi host, run the following commands:

<pre>esxcli network firewall ruleset set -e true -r httpClient
esxcli software profile update -d https://hostupdate.vmware.com/software/VUM/PRODUCTION/main/vmw-depot-index.xml -p ESXi-5.5.0-1331820-standard</pre>

You must run the update command, and not the install command, as the update command keeps existing VIBs and drivers already present. If you run the install command and continue, you&#8217;ll lose the NIC drivers. Thanks to Andreas Peetz for spotting this and [documenting it](http://www.v-front.de/2013/09/how-to-update-your-standalone-host-to.html).
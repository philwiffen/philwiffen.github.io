---
id: 636
title: How to Remotely enable TPM in the BIOS on a Dell PC
date: 2010-08-25T14:14:15+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=636
permalink: /2010/08/25/how-to-remotely-enable-tpm-in-the-bios-on-a-dell-pc/
categories:
  - Miscellaneous
---
This guide will run through how to remotely turn on and activate TPM in the BIOS on a Dell PC using the Dell Client Configuration ToolKit

# Setup

First we need to install the Dell Client Configuration Toolkit (CCTK) on the target system.

To do this:

  1. Log onto the target system via RDP
  2. Grab the [CCTK MSI file](http://support.dell.com/support/downloads/download.aspx?c=us&l=en&s=gen&releaseid=R229673&formatcnt=1&libid=0&fileid=329826)
  3. Install the CCTK onto the target system

# Making Configuration Changes

On the target system:

  1. Log onto the target system via RDP
  2. Open up a Command Prompt
  3. Navigate to: C:\Program Files\Dell\CCTK\ 
      1. If you’re running 32-bit OS, go into X86 folder
      2. If you’re running 64-bit OS go into X86_64 folder
      3. From here, run the relevant command&#8230;
      4. To enable and activate TPM on the target system: 
          1. `cctk --tpm=on`
          2. `cctk --tpmactivation=activate`
      5. Reboot, and TPM will be enabled

# Bootnote

This process was tested and confirmed working on a Dell Latitude E6410 running Windows 7 32-bit. Let us know in the comments if it works for you too! 🙂

# More Resources

There&#8217;s a page from Dell which covers more background here: <http://www.delltechcenter.com/page/Dell+Client+Configuration+Toolkit>
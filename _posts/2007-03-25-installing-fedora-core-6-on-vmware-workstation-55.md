---
id: 37
title: Installing Fedora Core 6 on VMWare Workstation 5.5
date: 2007-03-25T14:24:17+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/03/25/installing-fedora-core-6-on-vmware-workstation-55/
permalink: /2007/03/25/installing-fedora-core-6-on-vmware-workstation-55/
categories:
  - Troubleshooting
  - Virtualisation
---
When installing Fedora Core 6 on my Windows VMware setup, it failed to find any disks to install on. The reason? I selected the Guest OS as &#8220;Red Hat Linux&#8221;, seeing as Fedora Core has direct lineaege from Red Hat. Anyway, it doesn&#8217;t work and fails to find a disk. To get around this, choose &#8220;Red Hat Enterprise Linux 4&#8221; or &#8220;Other Linux 2.6.x kernel&#8221; and it&#8217;ll find the Virtual SCSI disk perfectly.

<!--more-->

![vmware-fedora-core-6-install.png](http://www.kabri.uk/wp-content/uploads/2007/03/vmware-fedora-core-6-install.png)
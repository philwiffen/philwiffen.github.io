---
id: 29
title: RAID-5 in Ubuntu with mdadm
date: 2007-03-14T14:12:55+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://kabri.uk/?p=29
permalink: /2007/03/14/raid-5-in-ubuntu-with-mdadm/
categories:
  - Linux
---
Couldn&#8217;t really find anyone who&#8217;d documented setting up a RAID 5 array with Linux and mdadm, so figured I&#8217;d jot down the method I used in Ubuntu 6.10. It basically boils down to four commands (I am assuming you have a fresh install):

<pre>sudo apt-get install mdadm
sudo mdadm --create /dev/md0 --raid-devices=5 /dev/sd[abcde]1 --level=raid5
sudo mke2fs -j /dev/md0
sudo mount /dev/md0 /mnt/raid</pre>

To explain a little:

The first command installs mdadm.

The second command creates the raid array /dev/md0, then sets how many disks &#8211; and their respective locations &#8211; there&#8217;ll be in the array. In my case, we have 5 750GB drives, which are /dev/sda through to /dev/sde. The 1 is the partition identifier. Level sets the raid level, which in this case is raid5.

The third command &#8216;`sudo mke2fs -j /dev/md0` &#8216; makes an ext3 filesystem on the array.

And finally &#8216;`sudo mount /dev/md0 /mnt/raid`&#8216; mounts the array to /mnt/raid (you can mount it wherever you like)

Note 1: Make sure you have mdadm installed. If you don&#8217;t: `sudo apt-get install mdadm`

Note 2: If you&#8217;re not using Ubuntu, su to root and run the commands without &#8216;sudo&#8217;

Note 3: If you get an error stating &#8216;mdadm: error opening /dev/md0: No such file or directory&#8217;, you need to bypass udev and use this command instead: `sudo mdadm --create /dev/md0 --raid-devices=5 /dev/sd[abcde]1 --level=raid5 --auto=yes`

Note 4: To view the status of your array: `sudo mdadm --detail /dev/md0`

Note 5: If you need to view a list of your hard drives, try these commands: `ls -l /dev/sd*` or `ls -l /dev/hd*`

I am certainly no Linux expert. **Corrections, and suggestions on how to improve this method are encouraged** 🙂

Update: There&#8217;s a very thorough guide [here](http://bfish.xaedalus.net/?p=188), but it seems to cover some GUI elements &#8211; which wasn&#8217;t an option for me.
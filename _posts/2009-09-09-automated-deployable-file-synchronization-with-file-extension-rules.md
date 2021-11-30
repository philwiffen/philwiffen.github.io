---
id: 550
title: Automated, Deployable File Synchronization with file extension rules?
date: 2009-09-09T14:30:33+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2009/09/09/automated-deployable-file-synchronization-with-file-extension-rules/
permalink: /2009/09/09/automated-deployable-file-synchronization-with-file-extension-rules/
categories:
  - Miscellaneous
---
I&#8217;ve had this recurring nightmare over the past year. How on Earth can we easily deploy a file sync solution for our laptop and desktop users?

Due to our company&#8217;s flexibility with end-user&#8217;s computers, we have to have rulesets (i.e. do not back up .avi or .mp3 files). Otherwise we&#8217;ll fill up our NAS/SAN with useless media files within a few hours 😉

The solution needs to sync between the end-users local computer &#8220;My Documents&#8221; folder, to their network storage space. And it needs to be able to be deployed in an automated, pre-configured way, complete with scheduling. **EDIT**: By deployed, I don&#8217;t mean exclusively with GPSI. I&#8217;m more than happy just running some kind of AutoIT Script or Batch file that installs the software then dumps/edits the config files for the end-user based on env variables or whatever, but it must not require any &#8211; or at least minimise &#8211; end-user interaction.

I&#8217;ve checked out SyncToy and it&#8217;s nice, but a complete pain to automate the actual Scheduling &#8220;part&#8221;.

I&#8217;m currently looking at Toucan Backup, but that seems more keen on backing up \*everything\*, then applying exclusions. I need something that will back up nothing, except what I tell it to.

Any ideas or pointers? I&#8217;d greatly appreciate it! 🙂
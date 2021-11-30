---
id: 40
title: Setting Folder Sharing Permissions on Windows XP Home
date: 2004-06-02T21:54:49+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2004/06/02/40/
permalink: /2004/06/02/setting-folder-sharing-permissions-on-windows-xp-home/
ratings_users:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
ratings_score:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
ratings_average:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
categories:
  - Security
  - Windows
---
<p class="storycontent">
  2007-03-27 &#8211; This article is very old and I&#8217;m republishing it as it was, without any edits. At the time I was a youngin&#8217;, so please accept my apologies in advance 😉
</p>

<p class="storycontent">
  As I found out yesterday, sharing folders on Windows XP using Simple File Sharing is like leaving your back door unlocked while you&#8217;re upstairs. This article discusses ways to make folder shares secure on Windows XP Home and Professional by allowing the use of user and group permissions.
</p>

## Simple File Sharing &#8211; Why it&#8217;s a pain

Simple file sharing is, just as it&#8217;s name suggests; simple. It doesn&#8217;t concern itself with who can or can&#8217;t get at your files, nor does it distinguish between who you want modifying your files and who you&#8217;d rather not. This is fine on your personal home network, as it&#8217;s safe to bet you trust the people who&#8217;re using it. Not so on an open network, such as a company&#8217;s, or indeed an academic one.

Looking at it from a users point of view, it gets the job done. From an administrator&#8217;s point of view it&#8217;s pretty messy &#8211; It doesn&#8217;t take much for a disgruntled employee to poke around in the <acronym title="Research & Development">R&D</acronym> departments shared files before they find something they&#8217;re competitors (and soon to be new employers) may be **very** interested in. And finally from a geeks point of view it really is incredibly frustrating being told by Windows I can&#8217;t control access to **my** PC.

## XP Home Vs XP Pro

As we all know, XP Home is aimed at, well, home users. Only a lot of people using it aren&#8217;t your typical home user; they need the flexibility to be able to control access to their files on the network. Having used XP Pro at home, I was disappointed to find that Home won&#8217;t let you turn off simple file sharing.

With XP Professional, the options to enable permissions and get rid of Simple File Sharing are there, they&#8217;re just not in the most obvious of places.

So, onto disabling SFS and getting control of your PC back.

## Setting Share Permissions for XP Pro

The solution for XP Pro is relatively simple:

> My Computer » Tools » Folder Options » View Tab.

Go right down to the bottom of the list, and **uncheck** Use Simple File Sharing (Recommended).

Now go back to your shared folder&#8217;s properties

> Right Click on Shared Folder » Sharing and Security.

You are now able to set permissions. Hooray!

## Folder Sharing Permissions on XP Home

XP Home won&#8217;t let you turn off Simple File Sharing like on XP Pro, so we have to go around it. To allow you to set permissions on your shares follow this:

> Start » Run » Type &#8216;shrpubw&#8217; into the box and hit OK.

A nice menu now appears allowing you to specify what you want to share, and to describe it.

Click next and the following options are fairly self explanatory. however, remember that with XP Home &#8216;Other Users&#8217; is usually the _Everyone_ group which **includes** the _Anonymous_ group.

**If you wish to prevent anonymous access** and properly lock down your permissions, you should choose _Custom_, delete the &#8216;Everyone&#8217; entry and add the groups and users you want to control access for.

## Final Thoughts

I mainly use XP Pro at home, so to be honest I didn&#8217;t even know of the &#8216;shrpubw&#8217; method until yesterday, whilst searching for a way to control Share permissions on my XP Home Laptop. So, if you found this article useful, please, please, please pass the link on to others who you think might benefit. After all, knowledge is power and all that.

Phil
---
id: 16
title: Clean dllcache
date: 2006-12-14T19:44:41+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://kabri.uk/?p=16
permalink: /2006/12/14/clean-dllcache/
categories:
  - Windows
---
To clear out/clean up the dllcache folder within Windows\system32 open up a command line and type the following:

<kbd>sfc /purgecache</kbd>  
<kbd>sfc /cachesize=x</kbd> (where x equals the maximum size, in megabytes, you&#8217;d like the dllcache to be. For example, I used cachesize=150)
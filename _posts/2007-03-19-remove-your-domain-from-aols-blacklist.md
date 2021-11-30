---
id: 32
title: 'Remove your domain from AOL&#8217;s blacklist'
date: 2007-03-19T11:53:29+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://kabri.uk/2007/03/19/remove-your-domain-from-aols-blacklist/
permalink: /2007/03/19/remove-your-domain-from-aols-blacklist/
categories:
  - Security
---
A friend of mine has just had his employer&#8217;s Exchange server blacklisted by AOL, meaning anything from or to an aol address won&#8217;t go through. This often happens when people mistakenly flag legitimate mail as Spam in their AOL client or you leave your mail server as an Open Relay, opening a nice gateway for spammers.

### Check for Open Relay

To check your Mail Server for Open Relay, go here: [http://www.checkor.com](http://www.checkor.com/) 

If you have an open relay fix it ASAP. You should always enable some kind of authentication on your mail servers! (POP or SMTP auth is usually sufficient)

### Remove from AOL Blacklist

To find out how to remove your mail server from the AOL blacklist (and get yourself on their whitelist) check out <http://postmaster.aol.com/>
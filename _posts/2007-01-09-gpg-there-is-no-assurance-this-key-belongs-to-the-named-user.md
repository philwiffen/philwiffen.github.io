---
id: 19
title: 'GPG: There is no assurance this key belongs to the named user'
date: 2007-01-09T11:59:28+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://kabri.uk/?p=19
permalink: /2007/01/09/gpg-there-is-no-assurance-this-key-belongs-to-the-named-user/
categories:
  - Linux
  - Security
---
In GnuPG, if you get an error saying &#8220;There is no assurance this key belongs to the named user&#8221; when trying to encrypt, you need to sign the public key.

You can sign the key by typing &#8220;`gpg --sign-key <em>user-id</em>`&#8221; at the command prompt.

Footnote: I came across this whilst migrating our e-commerce system to a new server. The system uses GnuPG to encrypt the order/credit card information and then emails it to our sales team. I&#8217;m making sure I document the process fully, so that I don&#8217;t have to spend so much time figuring this stuff out again! 🙂
---
id: 20
title: 'SpamAssassin: Can’t locate Mail/SPF/Query.pm'
date: 2007-01-11T11:25:48+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://kabri.uk/?p=20
permalink: /2007/01/11/spamassassin-cant-locate-mailspfquerypm/
categories:
  - Linux
  - SpamAssassin
---
If you have SpamAssassin installed and see &#8220;`Can't locate Mail/SPF/Query.pm in @INC...`&#8221; in your error logs, you need to install _Mail::SPF::Query._ <span></span>

<span>SpamAssassin uses SPF to detect header and email-source forgery &#8211; very important in determining if e-mail is legitimate or not.</span>

To install Mail::SPF::Query, run these commands as root:

`perl -MCPAN -e shell<br />
install Mail::SPF::Query`

If you haven&#8217;t yet added SPF records to your DNS, you can find out more at the [Sender Policy Framework site](http://www.openspf.org/)
---
id: 85
title: 'PHP: Making Credit Card Numbers Human-Readable'
date: 2007-06-05T16:28:53+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/06/05/php-making-credit-card-numbers-human-readable/
permalink: /2007/06/05/php-making-credit-card-numbers-human-readable/
categories:
  - Business
  - Design and Usability
---
If you&#8217;ve ever tried to enter a 16 digit credit card number all in one blob, you&#8217;ll know it&#8217;s hard. To make life easier for the person responsible for processing online credit card orders, I needed to split up the credit card number and insert a space every 4 characters.

I&#8217;m not very schooled up on RegEx, and after spending ages searching for how to do it, I came across this:

`<?php<br />
echo implode(' ',str_split($credit_card_number,4));<br />
?>`

Hopefully it saves someone else some time!
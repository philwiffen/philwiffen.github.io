---
id: 55
title: 'Google Analytics: Tracking over both HTTP and HTTPS'
date: 2007-04-13T18:07:20+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/2007/04/13/google-analytics-tracking-over-both-http-and-https/
permalink: /2007/04/13/google-analytics-tracking-over-both-http-and-https/
ratings_score:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
ratings_users:
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
  - Web Development
---
Crownhill&#8217;s e-commerce website uses Google Analytics to provide some of our tracking metrics (it&#8217;s free, so it gives us instant ROI ;)). One major problem I had was that, when the order process moved from HTTP to HTTPS to protect our customer&#8217;s credit card details, browsers would throw up a &#8220;Mixed content&#8221; warning; something which would most likely confuse and, ultimately, scare customers away.

After a bit of digging around in Google Groups I devised a solution to the problem using a dash of PHP. I&#8217;ve provided the code below:

    
    <?php if ($_SERVER['HTTPS'] == "off") { // if the server isn't in HTTPS mode, echo this ?>
    <script src="http://www.google-analytics.com/urchin.js" type="text/javascript">
    <?php } else { // otherwise echo the HTTPS URL for the javascript ?>
    <script src="https://ssl.google-analytics.com/urchin.js" type="text/javascript">
    <?php } ?>
    
    </script>
    <script type="text/javascript">
    _uacct = "UA-xxxxxx"; /* Make sure you change this to reflect your GA account number! */
    urchinTracker();
    </script></pre>
    <p>  
    To explain a little. Basically, all I'm doing is checking to see what mode Apache is in, then adjusting the JavaScript source accordingly; to ensure that the browser doesn't present any Mixed-Content warnings to the customer - we certainly don't want to scare them off! The rest of the Javascript code is exactly the same as Google Analytics gives you; all I've done is change the link to the .js file.</p>
    
    
    [Grab the code in a .txt file](http://www.kabri.uk/wp-content/uploads/2007/04/google-analytics-http-to-ssl-https-transition-code.txt "Google Analytics: Track over both HTTP and HTTPS code")
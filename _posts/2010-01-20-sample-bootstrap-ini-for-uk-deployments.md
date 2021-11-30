---
id: 594
title: Sample BOOTSTRAP.INI for UK deployments
date: 2010-01-20T17:11:12+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=594
permalink: /2010/01/20/sample-bootstrap-ini-for-uk-deployments/
categories:
  - Miscellaneous
---
Here&#8217;s a sample BOOTSTRAP.INI that we use at DisplayLink for MDT deployments.

This will pre-fill a number of options throughout the MDT WinPE Deployment Wizard.

Share and enjoy 😉

    
    [Settings]
    Priority=Default
    
    [Default]
    DeployRoot=\\MDTSERVER\Distribution$
    
    SkipBDDWelcome=YES
    
    
    
    KeyboardLocale=0809:00000809
    UserLocale=en-GB
    InputLocale=0809:00000809
    SystemLocale=en-GB
    UILanguage=en-US
    UserDomain=YOURDOMAIN
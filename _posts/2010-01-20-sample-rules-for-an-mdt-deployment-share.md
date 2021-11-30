---
id: 597
title: Sample Rules for an MDT Deployment Share
date: 2010-01-20T17:15:43+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=597
permalink: /2010/01/20/sample-rules-for-an-mdt-deployment-share/
categories:
  - Miscellaneous
tags:
  - BDD
  - MDT
  - MDT 2010
  - Microsoft Deployment Toolkit
---
Here&#8217;s a sample of the UK rules we use at DisplayLink for our MDT 2010 Deployment Shares:

    
    [Settings]
    Priority=Default
    Properties=MyCustomProperty
    
    [Default]
    OSInstall=Y
    SkipAppsOnUpgrade=YES
    SkipCapture=YES
    SkipAdminPassword=YES
    SkipProductKey=YES
    
    ;Skips Welcome Screen
    SkipBDDWelcome=YES
    
    ; VISTA LOCALE SETTINGS
    KeyboardLocale=0809:00000809
    UserLocale=en-GB
    InputLocale=0809:00000809
    SystemLocale=en-GB
    UILanguage=en-US
    
    ;BitLocker
    OSDBitLockerWaitForEncryption = "FALSE"
    BdeRecoveryKey=AD
    BDEInstall=TPMPin
    BdeInstallSupress=NO
    OSDBitLockerMode=TPMKey
    OSDBitLockerCreateRecoveryPassword=AD
    
    ;SkipTimeZone=YES
    TimeZone=85
    TimeZoneName=GMT Standard Time
    
    UserDataLocation=AUTO
    
    SkipComputerBackup=YES
---
id: 501
title: How to make Visual Studio 2005 automatically install SQL Server Express 2005 SP2
date: 2009-01-09T10:31:09+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://www.kabri.uk/?p=501
permalink: /2009/01/09/how-to-make-visual-studio-2005-automatically-install-sql-server-express-2005-sp2/
aktt_notify_twitter:
  - 'no'
  - 'no'
  - 'no'
  - 'no'
  - 'no'
categories:
  - General IT
tags:
  - sql express 2005 sp2
  - vista
  - visual studio
---
As standard, the Visual Studio 2005 setup installs the original SQL Server 2005 Express Edition. In most environments this is highly undesirable &#8211; particularly as Vista has &#8220;app compatability&#8221; issues with the original SQL Express 2005.

If you want to get the Visual Studio setup to install SQL Server 2005 Express Edition SP2 instead, check out these great [instructions by Aaron Stebner](http://blogs.msdn.com/astebner/archive/2007/02/22/mailbag-can-i-update-visual-studio-2005-setup-to-install-sql-express-2005-sp2.aspx).

Here&#8217;s what I did for reference:

  1. Went to the [SQL Express 2005 SP2 download page](http://www.microsoft.com/downloads/details.aspx?familyid=31711D5D-725C-4AFA-9D65-E4465CDFF1E7&displaylang=en).
  2. Downloaded _both_ packages.
  3. Navigated to the Visual Studio install share and located the SQL Express installers (\wcu\SSE\).
  4. Renamed the existing installers to *.old
  5. Copied the new installers to the same directory.
  6. All done 🙂

<div>
  Thanks again Aaron!
</div>
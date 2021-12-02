---
title: 'How to get a Bearer Token from Citrix Cloud for API access, using PowerShell'
date: 2020-07-15T15:56:08+00:00
author: Phil Wiffen
excerpt: |
layout: post
categories:
  - code
---

Wanted to share a quick PowerShell code snippet.

I used this to get a Bearer Token from the Citrix Cloud API trust service using PowerShell.

It’s not beautiful, but it gets the job done.

## Ingredients

You’ll need:

1.  The clientID and clientSecret from your Citrix Cloud customer API client ([how to do that is here](https:/developer.cloud.com/getting-started))
1.  Your customerID for your Citrix Cloud instance

Then put those in-between the relevant quotation marks in the code snippet 🙂

```
$customerID = "yourcustomerID"
$clientID = "yourclientID"
$clientSecret = "yourclientSecret"
```

## PowerShell code snippet

```
$customerID = "yourcustomerID"
$uri = "https://trust.citrixworkspacesapi.net/$customerID/tokens/clients"
$clientID = "yourclientID"
$clientSecret = "yourclientSecret"
 
#create a hash table for the body and headers: https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_hash_tables?view=powershell-7
$body = @{ 
"ClientId" = "$clientID";
"ClientSecret" = "$clientSecret";
}
$headers = @{ 
"Accept" = "application/json";
"Content-Type" ="application/json";
}
 
#must convert the body to JSON, otherwise you get error "Invoke-RestMethod : {"message":"The request is invalid.","modelState":{"credentials":["An error has occurred."]}}"
#To show the whole response, comment out the next line and use this instead: Invoke-RestMethod -Method 'Post' -Uri $uri -Body (ConvertTo-Json $body) -Headers $headers
 
$getBearerToken = Invoke-RestMethod -Method 'Post' -Uri $uri -Body (ConvertTo-Json $body) -Headers $headers
 
$bearerToken = $getBearerToken.token
 
Write-Host "Your Authorization header is:"
$authHeader = "CwsAuth Bearer=$bearerToken"
Write-Host "$authHeader
```

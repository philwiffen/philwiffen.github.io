---
id: 1553
title: Install Citrix Cloud Connector on Server Core 2016
date: 2018-09-22T15:20:05+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://kabri.uk/?p=1553
permalink: /2018/09/22/install-citrix-cloud-connector-on-server-core-2016/
categories:
  - Citrix
  - Cloud
  - PowerShell
  - Virtualisation
---
## Scope

This post will provide some quick notes on installing the Citrix Cloud Connector on Server Core 2016.

## Conceptual overview

  * We&#8217;re going to take our domain-joined Server Core installation and install the Citrix Cloud Connector on to it.
  * You can&#8217;t simply run the installer from the Server Core UI, because Server Core doesn&#8217;t have all the bits required for the Connector wizard to work.
  * So to work around this we&#8217;ll get an API Access key from Citrix Cloud admin UI and use that to install the connector silently on the command line.

## Pre-requisites and considerations

  * It&#8217;s assumed you have installed Server Core 2016 and joined it to the domain.
  * I believe you&#8217;ll need an API access secure client entry for **each** controller you&#8217;re setting up. Happy to be corrected on this, but it feels like that&#8217;s the best way to go about this.
  * The API access key is tied to the Citrix Administrator. If that Adminstrator account is later revoked access or permissions changed, the API keys will stop working. More on this [here.](https://developer.cloud.com/create_api_client.html)
  * As of right now (September 2018) installing the Cloud Connector on Server Core is not supported &#8211; however, the team is aware of appetite for this, and have a workstream open to do some testing with all the components.

## Steps

### Create an API Access secure client entry for the connector

Go to https://citrix.cloud.com > Identity and Access Management > [API Access](https://us.cloud.com/identity/api-access) tab

<p style="padding-left: 30px;">
  <a href="http://kabri.uk/wp-content/uploads/2018/09/api-access-clients-2.png"><img loading="lazy" class="size-medium wp-image-1567 alignnone" src="http://kabri.uk/wp-content/uploads/2018/09/api-access-clients-2-300x201.png" alt="" width="300" height="201" /></a>
</p>

Enter a descriptive name of your Server Core VM in the &#8220;Name your Secure Client box&#8221; and click Create Client &#8211; I typically use the VM hostname so it&#8217;s easy to track which controllers are using which credentials. If you want to add more contextual info, do so. The field isn&#8217;t tied or reliant on the VM name at all.

<p style="padding-left: 30px;">
  <a href="http://kabri.uk/wp-content/uploads/2018/09/api-access-key-generated.png"><img loading="lazy" class="alignnone size-medium wp-image-1559" src="http://kabri.uk/wp-content/uploads/2018/09/api-access-key-generated-300x184.png" alt="" width="300" height="184" /></a>
</p>

Store the ID and the Secret given to you in a secure place. You&#8217;ll never be given the Secret again, so I&#8217;d recommend storing it securely.

### Gather required information

To install the connector from the command line you&#8217;ll need the following information:

  * Citrix Cloud Customer ID 
      * <span style="color: #808080;">You&#8217;re told this just before you make the <a style="color: #808080;" href="https://us.cloud.com/identity/api-access">API access</a> credentials, when entering a secure client name.</span>
  * API Access secure client ID 
      * <span style="color: #808080;">You&#8217;re told this when you make the <a style="color: #808080;" href="https://us.cloud.com/identity/api-access">API access</a> credentials</span>
  * API Access secure client Secret 
      * <span style="color: #808080;">You&#8217;re told this when you make the <a style="color: #808080;" href="https://us.cloud.com/identity/api-access">API access</a> credentials</span>
  * The ID of the Resource Location you&#8217;re installing the connector into. 
      * <span style="color: #808080;">This is the UUID of the Resource Location, not its friendly name. You&#8217;ll find it in the <a style="color: #808080;" href="https://us.cloud.com/locations">Resource Locations</a> &#8211; click on &#8220;ID&#8221; to view it.</span>

### Download the Connector onto the Server Core VM

Log in to the Server Core VM and run the following, replacing &#8220;_yourcustomeridhere_&#8221; with your Customer ID

> <pre class="toolbar-overlay:false lang:ps highlight:0 decode:true">powershell
cd c:\windows\temp\
Invoke-WebRequest -Uri https://downloads.cloud.com/yourcustomeridhere/connector/cwcconnector.exe -OutFile cwcconnector.exe -UseBasicParsing</pre>

### Install the connector silently

Now, from the same command line, build your silent install command, replacing _yourcustomeridhere_, _yourclientid_,  _yourclientsecret_, and _yourresourcelocationid_ with the information you gathered earlier, and run it:

> <pre class="lang:ps highlight:0 decode:true">.\cwcconnector.exe /quiet /Customer:yourcustomeridhere /ClientId:yourclientid /ClientSecret:yourclientsecret /ResourceLocationId:yourresourcelocationid /AcceptTermsOfService:true</pre>

That&#8217;s it. You won&#8217;t get confirmation that it worked, so you&#8217;ll need to check via Citrix Cloud

### Check your Resource Location to verify connectivity

Go back to the Citrix Cloud UI and check your [Resource Locations](https://us.cloud.com/locations) to verify if the connector is being setup. It can take a few minutes to complete.

### Uninstalling the Cloud Connector

Should you need to Uninstall the Cloud Connector from Server Core, you can run:

> <pre class="toolbar-overlay:false lang:ps decode:true">.\cwcconnector.exe /uninstall</pre>

It looks like this isn&#8217;t documented (not mentioned if you use /?) but it does work.

## Further reading

  * [Details on API Access clients](https://developer.cloud.com/create_api_client.html)
  * If you desire a more robust and automated way to do this, check out this [blog post](https://xenappblog.com/2018/citrix-windows-server-core/)
  * [Cloud Connector installation documentation](https://docs.citrix.com/en-us/citrix-cloud/citrix-cloud-resource-locations/citrix-cloud-connector/installation.html)

&nbsp;
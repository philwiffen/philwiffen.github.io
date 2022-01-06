---
id: 1588
title: Building a simple Citrix microapp that shows blog posts from a WordPress RSS feed
date: 2019-12-18T00:09:30+00:00
author: Phil Wiffen
excerpt: |
layout: post
guid: http://kabri.uk/?p=1588
permalink: /2019/12/18/building-a-simple-citrix-microapp-that-shows-blog-posts-from-a-wordpress-rss-feed/
categories:
  - Citrix
---
<div class="wp-block-image">
  <h1 class="aligncenter is-resized">
    Scope
  </h1>
</div>

This post will cover how to setup a simple microapp that anyone with access to the Citrix microapps service can build, using public URLs, with no authentication requirements. We&#8217;ll be using the RSS integration to talk to a WordPress RSS feed and build a microapp from that.

Here&#8217;s roughly how it&#8217;ll look in Workspace, when it&#8217;s finished:

[<img loading="lazy" class="alignnone  wp-image-1722" src="https://kabri.uk/wp-content/uploads/2019/12/how-it-looks-1024x358.png" alt="" width="831" height="291" />](https://kabri.uk/wp-content/uploads/2019/12/how-it-looks.png)

## Why bother?

I&#8217;ve spent the last few months learning about microapps, and implementing them into Citrix Engineering&#8217;s pre-release Workspace environments &#8211; and honestly, I wish I had a guide like this to follow when I first started. So here we are 🙂

My hope is that following this guide will help you get familiar with the concepts, before you dive into the heavier stuff, like accessing internal API endpoints for enterprise systems, or figuring out the details around Oauth 2.0 authentication.



By following this post you&#8217;ll learn:



  * How to add an Integration and a microapp
  * How to make changes to how a microapp displays data

## What are we building?

We&#8217;ll build a Citrix Blog posts microapp, which uses the [RSS Out-of-the-box integration](https://docs.citrix.com/en-us/citrix-microapps/set-up-template-integrations/integrate-rss.html) to connect to the Citrix Blogs RSS feed, which happens to be in a WordPress format and:

  * Notifies Workspace when there&#8217;s a new blog post
  * Enables colleagues to view blog posts from Workspace
  * Allows colleagues to view a list of blog posts in a searchable table

## Before you start

This guide assumes that you already have access to the Microapps service in your Citrix Cloud account. If you do not, you can request access to a Test Instance here: <https://developer.cloud.com/citrix-workspace>

First, familiarise yourself with the following microapps concepts by [reading the documentation that covers Terminology](https://docs.citrix.com/en-us/citrix-microapps.html#terminology?)

Specifically you&#8217;ll need to learn the meanings of:

  * Integration
  * Microapp
  * Notification
  * Page
  * Action

I&#8217;ll be using the above terms liberally, so knowing what they mean will help.

## Let&#8217;s build it!

### We&#8217;re going to:

  1. Add an RSS Integration to sync Citrix Blog posts
  2. Change the name of the microapp so it&#8217;s more intuitively named in Workspace Actions
  3. Change the sort order of Blog posts to: Date, Descending
  4. Change the Description field of the Item Detail page to show HTML content for prettier viewing
  5. Set the Title of the blog post to be in the header of the page
  6. Add a &#8220;View Post&#8221; button, that goes to the Blog Post online
  7. Setup the Synchronization Schedule
  8. Add Subscribers to the microapp (so they can see Notifications and Actions)

### Add the Integration

Go to the Microapps Admin page, and choose &#8220;Add New Integration&#8221;<figure class="wp-block-image">

<img class="wp-image-1589" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-16-22_00_30-Microapps-Admin.png" alt="" />  

If asked, you want to use a Citrix-provided template

Choose the RSS Integration<figure class="wp-block-image">

<img class="wp-image-1598" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-16-22_12_50-Microapps-Admin.png" alt="" />  

Give the Integration a name, such as Citrix Blogs (RSS), and enter the URL to the WordPress RSS feed. In this example, for Citrix Blogs, the URL to the RSS feed is: http://feeds.feedblitz.com/citrix&x=1<figure class="wp-block-image">

<img class="wp-image-1591" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-16-22_04_39-Microapps-Admin.png" alt="" />  

You&#8217;ll then be taken to the Microapps list of integrations, and you&#8217;ll see the new integration. Inside, it&#8217;ll already have a microapp configured called &#8220;Items&#8221;, and you&#8217;ll see it has Synchronized. We&#8217;ll be modifying this microapp to make it fit our needs.<figure class="wp-block-image">

<img class="wp-image-1596" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-16-22_08_53-Microapps-Admin-1024x189.png" alt="" />  

Because the RSS Integration is deliberately generic &#8211; we need to make a number of tweaks to make the Blog microapp nicer to use and look at.

### Change the name of the Microapp

We change the name of the microapp, because this is how it appears in the Actions pane in Workspace. If we keep it as &#8220;Items&#8221;, its naming isn&#8217;t particularly user friendly. In our pre-release environments, we rename this microapp to Citrix Blogs, so people will know what they get when they click the Action.

To change the Microapp name:

  1. Click on &#8220;Items&#8221;
  2. Go to Properties
  3. Change the App Name, and the App Description to something more meaningful such as &#8220;Citrix Blogs&#8221; and &#8220;Shows posts from Citrix Blogs&#8221;
  4. Click Save<figure class="wp-block-image is-resized">

<img loading="lazy" class="wp-image-1602" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-16-22_18_04-Microapps-Admin-2.png" alt="" width="440" height="542" />  

Here&#8217;s a comparison of how they&#8217;d look in Workspace. I much prefer it to say Citrix Blogs. rather than Items 🙂<figure class="wp-block-image">

<img class="wp-image-1604" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-16-22_35_40-Citrix-Workspace.png" alt="" />  

### Change the sort order of Blog posts to Date, Descending

Out of the box, the Items table is not sorted by Date. Let&#8217;s fix that so it&#8217;s suitable for a Blog post list that shows the latest posts at the top of the table.

In the Citrix Blogs microapp, click on Pages, then click on Items<figure class="wp-block-image">

<img class="wp-image-1611" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-16-22_47_27-Microapps-Admin-3-1024x312.png" alt="" />  

Click the Table, so that it&#8217;s highlighted (a blue x will appear in the top-right of the table). Then click Set Order, or Edit Order, under Data Order<figure class="wp-block-image">

<img class="wp-image-1627" src="http://kabri.uk/wp-content/uploads/2019/12/2019-12-16-23_16_53-Microapps-Admin-1-1024x442.png" alt="" />  

  1. Set the Order by to: items, published_at, Descending.
  2. Click Save<figure class="wp-block-image">

<img class="wp-image-1613" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-16-22_51_30-Microapps-Admin.png" alt="" />  

Bonus points: Change the table Label from Items to Blog Posts. Again, this just makes it look nicer.<figure class="wp-block-image">

<img class="wp-image-1614" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-16-23_02_47-Microapps-Admin.png" alt="" />  

### Displaying HTML content from the blog posts

Just FYI: This HTML component is in the product at GA because I had issues with showing blog content in the microapp page, and the Product Management team did amazing work to accelerate their plans for this functionality. It sounds small, but it&#8217;s just one tangible example of what I (and my team) do inside Citrix &#8211; we use the product, we feedback, we help make things better

Out of the box, the RSS Integration shows raw text. It works really well for many kinds of feeds/data, but for some RSS feeds, the fields have HTML embedded in them.

Out of the box, it looks like this:<figure class="wp-block-image">

<img class="wp-image-1636" src="http://kabri.uk/wp-content/uploads/2019/12/2019-12-17-21_24_46-Microapps-Admin-5-588x1024.png" alt="" />  

And we&#8217;re going to tidy it up so it looks like this:<figure class="wp-block-image">

<img class="wp-image-1701" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-17-22_36_03-Microapps-Admin.png" alt="" />  

### Add the blog title to the header of the Page

Set the Blog Title as the page title and remove the existing title. This makes the title look much nicer:

  * Go to Pages, then click on Item Detail
  * Click the Back button in the Builder viewer
  * In the right-hand pane, set the Title Template from blank, to {{title}}<figure class="wp-block-image">

<img class="wp-image-1703" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-17-21_25_46-1024x265.png" alt="" />  

  * Click the Title text in the main body of the Builder viewer, and delete it (because the title is now shown at the top of the page)
  * This will now show the Blog post title in the Page header (and looks much nicer)

Replace the Description default Test component, with the HTML Content component:

  * Drag the HTML Content component so it goes above where the current Description text component is
  *  <figure class="wp-block-image">

<img class="wp-image-1649" src="http://kabri.uk/wp-content/uploads/2019/12/2019-12-17-21_33_41-Microapps-Admin-10-1024x630.png" alt="" />  

  * Set the Label (you can make it blank &#8211; it&#8217;s not required) and set the Data Table to &#8220;Items&#8221; and the Data column to &#8220;Description&#8221;
  * Delete the other Description component, by clicking on it, then clicking the X in the top=right hand corner.<figure class="wp-block-image">

<img class="wp-image-1678" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-17-21_47_49-1024x375.png" alt="" />  

It&#8217;ll then populate the HTML component and look much nicer!<figure class="wp-block-image">

<img class="wp-image-1698" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-17-22_01_28-3-1024x580.png" alt="" />  

Personally, I remove the Categories Table, as it serves no purpose in this view. Click it and remove it with the X in the top-right corner of the Categories Table.<figure class="wp-block-image">

<img class="wp-image-1697" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-17-22_06_53-Microapps-Admin-1.png" alt="" />  

## Add a button to link to the Blog Post

Finally, let&#8217;s add a button to link to the Blog Post. This is a nice way to allow people to open the blog post if they want to read more than just the lede.

Drag the &#8220;Button&#8221; button to the bottom of the page:<figure class="wp-block-image">

<img class="wp-image-1696" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-17-22_08_52-Microapps-Admin-1-1024x925.png" alt="" />  

Then, set the button up like so&#8230;

Change the Button Label from Button, to &#8220;View Post&#8221; (or whatever you&#8217;d like it to say :))<figure class="wp-block-image">

<img class="wp-image-1699" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-17-22_34_52-Microapps-Admin.png" alt="" />  

Now we setup the link part.

Click Actions, on the right hand side:<figure class="wp-block-image">

<img class="wp-image-1688" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-17-22_09_54-Microapps-Admin-1-1024x207.png" alt="" />  

Then on the Drop down, choose &#8220;Go to URL&#8221;<figure class="wp-block-image">

<img class="wp-image-1685" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-17-22_10_38-Microapps-Admin.png" alt="" />  

Expand the Goto URL, then click on Insert Variable<figure class="wp-block-image">

<img class="wp-image-1684" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-17-22_11_27-Microapps-Admin.png" alt="" />  

From the dropdown, choose &#8220;url&#8221; and click Insert:<figure class="wp-block-image">

<img class="wp-image-1695" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-17-22_15_22-1.png" alt="" />  

You&#8217;ll then see the field populated with {{url}}. This will insert the Blog Post&#8217;s URL into the button, and will launch the site when clicked.

Preview the microapp to see your handiwork:<figure class="wp-block-image">

<img class="wp-image-1704" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-17-22_44_05-Microapps-Admin.png" alt="" />  

Looks good!<figure class="wp-block-image">

<img class="wp-image-1710" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-17-23_06_33-Microapps-Admin.png" alt="" />  <figure class="wp-block-image"><img class="wp-image-1705" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-17-22_44_43-Microapps-Admin-1024x732.png" alt="" /> 

### Set a Synchronization Schedule

Now we&#8217;ve made the microapp, with its pages, we should set a Synchronization Schedule.

The schedule is up to you and the feed you&#8217;re pulling in. For Citrix Blogs, we set this to once every hour, which is a good balance between keeping things up to date, but not hitting the website too much with requests.

After a sync happens, if a new blog post entry is found a notification is sent to Subscribers to that microapp, and it appears in the Workspace feed (and, if enabled, a Push Notification to the person&#8217;s device with Citrix Workspace app, too)

_Please note: The first time you sync &#8211; no Notifications will be generated. So when you look in your feed, there won&#8217;t be any Notifications yet. This is because notifications are generated the **next** time a sync occurs **and** there&#8217;s new blog posts. The first sync will simply load up the microapps cache. You&#8217;ll need to wait for a new blog post to be posted into the RSS, and for a sync to happen, for a notification to be generated._

You set the Synchronization by going to the Microapp Integrations page, clicking the three dots next to the integration and choosing Synchronization<figure class="wp-block-image">

<img class="wp-image-1706" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-17-22_47_32-Microapps-Admin-1024x165.png" alt="" />  

### Adding Subscribers to the microapp

The final step of this process: Giving people access to the microapp itself. Without being granted this, people won&#8217;t see the microapp, or the notifications

To give people access, Click the three dots next to the microapp, and choose Subscriptions<figure class="wp-block-image">

<img class="wp-image-1707" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-17-22_51_15-Microapps-Admin-1024x232.png" alt="" />  

In the example below, I&#8217;m showing that you can add Security Groups, as well as individual users. This can help you test, and gradually roll out the microapp in a live environment in phases, to help ensure quality and user acceptance.<figure class="wp-block-image">

<img class="wp-image-1708" src="https://kabri.uk/wp-content/uploads/2019/12/2019-12-17-22_52_51-Microapps-Admin.png" alt="" />  

## Pat yourself on the back

You just made your first microapp!

You learned how pages work, how to modify those pages if you need to, you learned about changing and adding variables to buttons and components, how to order data in tables, add buttons that link somewhere else, and finally how to add subscribers to a microapp, schedule synchronizations and how to preview it.

There&#8217;s a lot to take in, but hopefully running through this will make it easier on you when you come to do more heavy-weight microapps that might need things like authentication, and on-premises connections with the Connector Appliance.

Happy microapping 🙂
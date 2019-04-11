---
title: Sitecore wish list
description: This is a master list of features/ upgrades/ documentation that we wish Sitecore would have
categories: [Sitecore Features, Sitecore]
tags: [Sitecore, Documentation, Development, Examples, Personalisation, DAM]
author: Richard Dias
date: 04-09-2019
image: /images/wishlist/sitecore-angel.png
scversion: 9.1
---
![sitecore angel](/images/wishlist/sitecore-angel.png "sitecore angel")

This post is dedicated to a wishlist of what we would like to see from features to documentation and everything in between. 
Please feel free to comment below or email me on <rdias@1digit.co.uk> if you want me to add something to this list, correct me or let me know if a wish has been granted.
<!--more-->

## Features
### Workflow & Workbox
I've been working with Sitecore since version 5.3 and I must say that the workbox seems to have hardly changed.
We are selling Sitecore to clients with thousands of content items, globally distributed authoring teams and this content is often constantly changing. The current workbox isn't suitable for large volumes of content and authors are often requesting to bypass the Sitecore workflow altogether which is a very bad thing.
Start thinking about:
* Redoing the UI to make approving large numbers of content realistic
* Better methods of grouping content and assiging to individual approvers
* Using the search index to power the new workflow UI
* SXA is out, we can start approving partial designs/ composites etc as a whole

### Media cropping OTB
One of the biggest issues we see on many Sitecore websites is the fact that content authors seem to upload and use very large (200KB<) images on their site. They often allocate for the best looking image on Macbook Pro Retina screens without any notion of what this would do to a mobile site for example.
Larger page weights also get penalised by google so this is another loss.

Sitecore has a great media processing pipeline which will let you pass in parameters for width and height, you can use this to resize images and you can set the process quality to around 75 to get really good image compression.

The problem is that most websites need to have different aspect ratios for an individual image and simply resizing will not do, we need to be able to crop and optimize.

#### Sitecore Modules
There is a nice tool in the marketplace now:
* [Image field with cropping](https://marketplace.sitecore.net/Modules/I/ImageCropping.aspx?sc_lang=en "Image field with cropping Sitecore module"), this needs some tweaking for us to define a fixed/limited number of crops per site, otherwise it does a great job.

#### DAM's (Digital Asset Management)
There are DAM integrations like [Digizuite](https://www.digizuite.com/digital-asset-management-for-sitecore "Digizuite sitecore integration") (which at the time of writing has the most complete DAM integration with Sitecore) and Sitecore has recently acquired [Stylelabs](https://www.sitecore.com/en-gb/company/press-and-media/press-releases/2018/10/sitecore-to-acquire-innovative-content-marketing-software-vendor-stylelabs "Sitecore aquires Stylelabs") (which will do the job). Both of these have cropping functionality (and much more), the problem is that that these are paid services and have a lot more functionality and a pricetag to match. 

Sitecore should have a middle-ground solution that comes with the core platform.

### Options for hosting media externally
Although using a DAM solves this problem, we should be able to select more than 2 options for storing media (Blob, File system) by default.

I've worked with clients who are starting to have huge Master and Web Db's (> 20GB) and 95% of the space is used up by media blobs. Moving these externally would not only allow us more flexibility for backingup/restoring and moving DB's around, it can also prove invaluable when we have downtime because of deployment issues, sync issues, publishing issues where we would need to restore our web DB's ASAP.

Thanks to [Kate Orlova](https://github.com/kate-orlova/external-asset-management-in-sitecore "Kate Orlova") we've got a nice module which I hope Sitecore adopts:
[External asset management in Sitecore](https://marketplace.sitecore.net/Modules/E/External_asset_management_in_Sitecore.aspx?sc_lang=en "External asset management in Sitecore module. "). I've not used this personally but it looks nice and clean after having a browse of the code and its a Helix foundation project to boot!
This can easily be adpated for multiple DFS's and cloud hosting providers.

### Personalisation with CDN
At the moment Sitecore does all of its personalisation on the client side unless you start using some JSS functionality.
If you're a client with a global presense (and there are a lot of these) who needs to cover more than one geographical region and don't want to spend large sums on a geographically distributed CD node system then you will most likely be using a CDN like Akamai, Cloudlare or any number of players.
If we want to make use of Sitecores' rich personalisation and analytics we won't be able to edge cache the actual documents (Media or any other assets are not an issue). If we edge cache the document then the persona profiling won't work nor will other personalisation functionality.
Sitecore needs to move personalisation and content profiling to the client side so that working with CDN's won't hinder any Sitecore functionality.

## Development
### Async Sitecore Controllers
Please please can we have async controllers? the ability to mark renderings as async would be fantastic, this means non-essential renderings can be loaded asynctonously without our pages needing to 'wait' for them. The sooner the server can respond with the DOM the better.
```csharp
public async Task<ActionResult> MarketingTile()
```
Here is a nice article about [how async methods work](https://docs.microsoft.com/en-us/aspnet/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4 "Using Asynchronous Methods in ASP.NET MVC 4") in ASP.NET.

## Documentation
### Better scaling guidelines
It would be great to see more guidelines on how to horizontally scale a solution so that we can span multiple geographical datacentres.
Sitecore has provided some documentation on [clustering and geographic distribution](https://doc.sitecore.com/developers/90/platform-administration-and-architecture/en/clustering-and-geographic-distribution.html "Clustering and geographic distribution")  which shows the elements we would need for something like this but it's all very high level:

Each Content Delivery (CD) cluster which should be in its own data canter should have its own 
 * Session State DB
 * Web DB 
 * Core DB
 ![Sitecore horizontal web cluster](/images/wishlist/web-clusters.png "Sitecore horizontal web cluster")

So we can make some assumptions, that we have a load balancing strategy that sends visitors to their own cluster based on reverse GeoIP lookup.
What will we be sacrificing for this type of configuration? for example if we rely on the new Identity Server, this isn't built for multi-geography scale so its not an option. 
We can't have extranet users in the CoreDb anymore, so what is the alternative soluiton?
What are the implications on upgrading Sitecore?

## Examples
What can Sitecore provide in terms of examples, tutorials and demo enviornments?

### Helix & Habitat  &#10004;
This was going to be about providing better Helix project examples than Habitat. Luckily, this is going to happen already as announced by [Peter Brinkman at Sugcon London 2019](https://www.sugcon.eu/agenda/#day2  "Sugcon link").
There will be 3 new demo environments released (with source code) for small, medium and enterprise scale Sitecore Helix solutions!


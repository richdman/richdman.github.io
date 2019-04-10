---
title: Sitecore wish list
description: This is a master list of features/ upgrades/ documentation that we wish Sitecore would have
categories: [Feautres, Sitecore]
tags: [Sitecore, Documentation, Development, Examples, Personalisation]
author: Richard Dias
date: 04-09-2019
---
![sitecore angel](/images/wishlist/sitecore-angel.png "sitecore angel")

This post is dedicated to a wishlist of what we would like to see from features to documentation and everything in between. 
Please feel free to comment below or email me on <rdias@1digit.co.uk> if you want me to add something to this list, correct me or let me know if a wish has been granted.
<!--more-->
---
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
One of the biggest problems

### Personalisation with CDN
At the moment Sitecore does all of its personalisation on the client side unless you start using some JSS functionality.
If you're a client with a global presense (and there are a lot of these) who needs to cover more than one geographical region and don't want to spend large sums on a geographically distributed CD node system then you will most likely be using a CDN like Akamai, Cloudlare or any number of players.
If we want to make use of Sitecores' rich personalisation and analytics we won't be able to edge cache the actual documents (Media or any other assets are not an issue). If we edge cache the document then the persona profiling won't work nor will other personalisation functionality.
Sitecore needs to move personalisation and content profiling to the client side so that working with CDN's won't hinder any Sitecore functionality.

---
## Development
### Async Sitecore Controllers
Please please can we have async controllers? the ability to mark renderings as async would be fantastic, this means non-essential renderings can be loaded asynctonously without our pages needing to 'wait' for them. The sooner the server can respond with the DOM the better.
```csharp
public async Task<ActionResult> MarketingTile()
```
Here is a nice article about [how async methods work](https://docs.microsoft.com/en-us/aspnet/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4 "Using Asynchronous Methods in ASP.NET MVC 4") in ASP.NET.

---
## Documentation
### Better scaling guidelines
---
## Examples
What can Sitecore provide in terms of examples, tutorials and demo enviornments?

### Helix & Habitat
This was going to be about providing better Helix project examples than Habitat. Luckily, this is going to happen already as announced by [Peter Brinkman at Sugcon London 2019](https://www.sugcon.eu/agenda/#day2  "Sugcon link").
There will be 3 new demo environments released (with source code) for small, medium and enterprise scale Sitecore Helix solutions!


---
title: Some issues and solutions I faced when installing Sitecore commerce 9.1 with Sitecore 9.1.1 (9.1 Update 1)
date: 2019-04-17 13:35:41
categories: [Sitecore Commerce 9.1]
tags: [Sitecore Commerce 9.1, Sitecore Commerce Install, Sitecore 9.1 Update 1]
author: Richard Dias
---

The first thing to recommend is, use Viet Hoangs installation guides and his scrips, there are things like trusted itentity server certs which and needed for the commerce install that Sitecores default installation for 9.1.1 does not have:
* [Sitecore XP 9.1 Update 1 – Step by step Install Guide on your machine](https://buoctrenmay.com/2019/04/06/sitecore-xp-9-1-update-1-step-by-step-install-guide-on-your-machine/ "Sitecore XP 9.1 Update 1 – Step by step Install Guide on your machine") - first install SC 9.1 Update 1
* [Sitecore Commerce 9.1 Initial Release – Step by step Install Guide on your machine](https://buoctrenmay.com/2019/04/18/sitecore-commerce-9-1-initial-release-step-by-step-install-guide-on-your-machine/ "Sitecore Commerce 9.1 Initial Release – Step by step Install Guide on your machine")

# Sitecore 9.1 update 1 issues 
<!--more-->
## license.xml has not expired

You will see issues like:
```pshell
Install-SitecoreConfiguration : Failed to start service 'Sitecore XConnect Search Indexer -
sc911.xconnect.local-IndexWorker (sc911.xconnect.local-IndexWorker)'.
```
![Failed to start service](/images/commerce-install/sc911_installissue.png "expired license file")

Once the above error was sorted then I got the failiure below:

```pshell
Install-SitecoreConfiguration : Failed to start service 'Sitecore Marketing Automation Engine -
sc911.xconnect.local-MarketingAutomationService (sc911.xconnect.local-MarketingAutomationService)'.
```
![Failed to start marketting service](/images/commerce-install/sc911_installissue-marketting-nostart.png "expired license file")

Did and uninstall an reinstall and still no luck. It looks like a license file issue again, I made sure it's the correct license, made sure all host entries and certs were deleted via the cert MMS and restarted the machine, kicked off the installation and everything worked this time!

# Sitecore 9.1 Commerce install
## Make sure your Identity server cert is trusted

You need to make sure that you don't see any SSL validation error when navigating to the https:// URL of your identity server. If you have an error, then go back to you SC 9.1 Update 1 install and sort this out first.

If you're seeing this, then your commerce installation will not complete:
![Sitecore identity server not trusted](/images/commerce-install/identitty-server-notrust-snip.png "Sitecore identity server not trusted")
Make sure the SSL cert is trusted:
![Sitecore identity server is trusted](/images/commerce-install/identitty-server-trusted.png "Sitecore identity server is trusted")

## No storefront site?
Don't use the latest version of powershell (5.0), Viet Hoang mentions this in his blog. As far as I am concernted, Powershell Extenstion 4.7.2 is mandatory for a SC 9.1 Commerce install.
![No Storefront site](/images/commerce-install/no-storefront.png "No Storefront site")

## How long does the install take to complate?
It took my i7 18GB RAM SSD laptop almost an hour to complete:
![Installation time for commerce](/images/commerce-install/sc911_success.png "Installation time for commerce")
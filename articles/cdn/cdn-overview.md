---
title: Azure CDN Overview | Microsoft Docs
description: Learn what the Azure Content Delivery Network (CDN) is and how to use it to deliver high-bandwidth content by caching blobs and static content.
services: cdn
documentationcenter: ''
author: dksimpson
manager: akucer
editor: ''

ms.assetid: 866e0c30-1f33-43a5-91f0-d22f033b16c6
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/10/2017
ms.author: v-semcev

---
# Overview of the Azure Content Delivery Network

The Azure Content Delivery Network (CDN) caches static web content at strategically placed locations to provide maximum throughput for securely delivering content to users. The CDN offers developers a global solution for rapidly delivering high-bandwidth content by caching the content at physical nodes across the world. 

> [!NOTE]
> This article describes the Azure CDN, how it works, and the features of each Azure CDN product. To skip this information and view a tutorial about how to create a CDN endpoint, see [Getting started with Azure CDN](cdn-create-new-endpoint.md). To see a list of current CDN node locations, see [Azure CDN POP Locations](cdn-pop-locations.md).

The benefits of using a CDN to cache web site assets include:

* Better performance and improved user experience for end users, especially when using applications in which multiple round-trips are required to load content.
* Large scaling to better handle instantaneous high loads, such as the start of a product launch event.
* Distribution of user requests and serving of content directly from edge servers so that less traffic is sent to the origin.

## How it works
![CDN Overview](./media/cdn-overview/cdn-overview.png)

1. A user (Alice) requests a file (also called an asset) using a URL with a special domain name, such as `<endpointname>.azureedge.net`. DNS routes the request to the best performing Point-of-Presence (POP) location, which is usually the POP that is geographically closest to the user.
2. If the edge servers in the POP do not have the file in their cache, the edge server requests the file from the origin.  The origin can be an Azure Web App, Azure Cloud Service, Azure Storage account, or any publicly accessible web server.
3. The origin returns the file to the edge server, including optional HTTP headers describing the file's Time-to-Live (TTL).
4. The edge server caches the file and returns the file to the original requestor (Alice).  The file remains cached on the edge server until the TTL expires.  If the origin didn't specify a TTL, the default TTL is seven days.
5. Additional users may then request the same file using that same URL, and may also be directed to that same POP.
6. If the TTL for the file hasn't expired, the edge server returns the file from the cache. This process results in a faster, more responsive user experience.

## Azure CDN Features
There are three Azure CDN products:  **Azure CDN Standard from Akamai**, **Azure CDN Standard from Verizon**, and **Azure CDN Premium from Verizon**.  The following table lists the features available with each product.

|  | Standard Akamai | Standard Verizon | Premium Verizon |
| --- | --- | --- | --- |
| __Performance Features and Optimizations__ |
| [Dynamic Site Acceleration](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration) | **&#x2713;**  | **&#x2713;** | **&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Dynamic Site Acceleration - Adaptive Image Compression](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#adaptive-image-compression-akamai-only) | **&#x2713;**  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Dynamic Site Acceleration - Object Prefetch](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#object-prefetch-akamai-only) | **&#x2713;**  |  |  |
| [Video streaming optimization](https://docs.microsoft.com/azure/cdn/cdn-media-streaming-optimization) | **&#x2713;**  | \* |  \* |
| [Large file optimization](https://docs.microsoft.com/azure/cdn/cdn-large-file-optimization) | **&#x2713;**  | \* |  \* |
| [Global Server Load balancing (GSLB)](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-load-balancing-azure) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Fast purge](cdn-purge-endpoint.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Asset pre-loading](cdn-preload-endpoint.md) | |**&#x2713;** |**&#x2713;** |
| Cache/header settings (using [caching rules](cdn-caching-rules.md)) |**&#x2713;** |**&#x2713;** | |
| Cache/header settings (using [rules engine](cdn-rules-engine.md)) | | |**&#x2713;** |
| [Query string caching](cdn-query-string.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| IPv4/IPv6 dual-stack |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [HTTP/2 support](cdn-http2.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| __Security__ |
| HTTPS support with CDN endpoint |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Custom domain HTTPS](cdn-custom-ssl.md) | |**&#x2713;** |**&#x2713;** |
| [Custom domain name support](cdn-map-content-to-custom-domain.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Geo-filtering](cdn-restrict-access-by-country.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Token authentication](cdn-token-auth.md)|  |  |**&#x2713;**| 
| [DDOS protection](https://www.us-cert.gov/ncas/tips/ST04-015) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| __Analytics and Reporting__ |
| [Azure diagnostic logs](cdn-azure-diagnostic-logs.md) | **&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Core reports from Verizon](cdn-analyze-usage-patterns.md) | |**&#x2713;** |**&#x2713;** |
| [Custom reports from Verizon](cdn-verizon-custom-reports.md) | |**&#x2713;** |**&#x2713;** |
| [Advanced HTTP reports](cdn-advanced-http-reports.md) | | |**&#x2713;** |
| [Real-time stats](cdn-real-time-stats.md) | | |**&#x2713;** |
| [Edge node performance](cdn-edge-performance.md) | | |**&#x2713;** |
| [Real-time alerts](cdn-real-time-alerts.md) | | |**&#x2713;** |
| __Ease of Use__ |
| Easy integration with Azure services such as [Storage](cdn-create-a-storage-account-with-cdn.md), [Cloud Services](cdn-cloud-service-with-cdn.md), [Web Apps](../app-service/app-service-web-tutorial-content-delivery-network.md), and [Media Services](../media-services/media-services-portal-manage-streaming-endpoints.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| Management via [REST API](https://msdn.microsoft.com/library/mt634456.aspx), [.NET](cdn-app-dev-net.md), [Node.js](cdn-app-dev-node.md), or [PowerShell](cdn-manage-powershell.md). |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Customizable, rule-based content delivery engine](cdn-rules-engine.md) | | |**&#x2713;** |
| URL redirect/rewrite  (using [rules engine](cdn-rules-engine.md)) | | |**&#x2713;** |
| Mobile device rules (using [rules engine](cdn-rules-engine.md)) | | |**&#x2713;** |

\* Verizon supports delivering large files and media directly via General Web Delivery.


> [!TIP]
> Is there a feature you'd like to see in Azure CDN?  [Give us feedback](https://feedback.azure.com/forums/169397-cdn)! 
> 
> 

## Next steps
To get started with CDN, see [Getting started with Azure CDN](cdn-create-new-endpoint.md).

If you are an existing CDN customer, you can now manage your CDN endpoints through the [Microsoft Azure portal](https://portal.azure.com) or with [PowerShell](cdn-manage-powershell.md).

To see the CDN in action, check out the [video of the Build 2016 session](https://azure.microsoft.com/documentation/videos/build-2016-leveraging-the-new-azure-cdn-apis-to-build-wicked-fast-applications/).

Learn how to automate Azure CDN with [.NET](cdn-app-dev-net.md) or [Node.js](cdn-app-dev-node.md).

For pricing information, see [Content Delivery Network pricing](https://azure.microsoft.com/pricing/details/cdn/).


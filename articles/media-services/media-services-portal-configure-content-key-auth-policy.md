---
title: Configure Content Key Authorization Policy using the Azure portal | Microsoft Docs
description: Learn how to configure an authorization policy for a content key.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''

ms.assetid: ee82a3fa-c34b-48f2-a108-8ba321f1691e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako

---
# Configure Content Key Authorization Policy
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## Overview
Microsoft Azure Media Services enables you to deliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). AMS also enables you to deliver DASH streams encrypted with Widevine DRM. Both PlayReady and Widevine are encrypted per the Common Encryption (ISO/IEC 23001-7 CENC) specification.

Media Services also provides a **Key/License Delivery Service** from which clients can obtain AES keys or PlayReady/Widevine licenses to play the encrypted content.

This article shows how to use the Azure portal to configure the content key authorization policy. The key can later be used to dynamically encrypt your content. Currently you can encrypt the following streaming formats: HLS, MPEG DASH, and Smooth Streaming. You cannot encrypt progressive downloads.

When a player requests a stream that is set to be dynamically encrypted, Media Services uses the configured key to dynamically encrypt your content using AES or DRM encryption. To decrypt the stream, the player requests the key from the key delivery service. To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.

If you plan to have multiple content keys or want to specify a **Key/License Delivery Service** URL other than the Media Services key delivery service, use Media Services .NET SDK or REST APIs.

[Configure Content Key Authorization Policy using Media Services .NET SDK](media-services-dotnet-configure-content-key-auth-policy.md)

[Configure Content Key Authorization Policy using Media Services REST API](media-services-rest-configure-content-key-auth-policy.md)

### Some considerations apply:
* When your AMS account is created a **default** streaming endpoint is added  to your account in the **Stopped** state. To start streaming your content and take advantage of dynamic packaging and dynamic encryption, your streaming endpoint has to be in the **Running** state. 
* Your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files. For more information, see [Encode an asset](media-services-encode-asset.md).
* The Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.  If you create a ContentKeyAuthorizationPolicy and specify to use a “Token” restriction, then test it, and then update the policy to “Open” restriction, it will take roughly 15 minutes before the policy switches to the “Open” version of the policy.
* AMS streaming endpoint sets the value of the CORS 'Access-Control-Allow-Origin' header in preflight response as the wildcard '\*'. This works well with most players including our Azure Media Player, Roku and JW, and others. However, some players that leverage dashjs do not work since, with credentials mode set to “include”, XMLHttpRequest in their dashjs does not allow wildcard “\*” as the value of “'Access-Control-Allow-Origin”. As a workaround to this limitation in dashjs, if you are hosting your client from a single domain, Azure Media Services can specify that domain in the preflight response header. You can reach out by opening a support ticket through Azure portal.

## How to: configure the key authorization policy
To configure the key authorization policy, select the **CONTENT PROTECTION** page.

Media Services supports multiple ways of authenticating users who make key requests. The content key authorization policy can have **open**, **token**, or **IP** authorization restrictions (**IP** can be configured with REST or .NET SDK).

### Open restriction
The **open** restriction means the system delivers the key to anyone who makes a key request. This restriction might be useful for testing purposes.

![OpenPolicy][open_policy]

### Token restriction
To choose the token restricted policy, press the **TOKEN** button.

The **token** restricted policy must be accompanied by a token issued by a **Secure Token Service** (STS). Media Services supports tokens in the **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token** (JWT) format. For information, see [JWT token authentication](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/).

Media Services does not provide **Secure Token Services**. You can create a custom STS or leverage Microsoft Azure ACS to issue tokens. The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration. The Media Services key delivery service will return the encryption key to the client if the token is valid and the claims in the token match those configured for the content key. For more information, see [Use Azure ACS to issue tokens](http://mingfeiy.com/acs-with-key-services).

When configuring the **token** restricted policy, you must specify the primary **verification key**, **issuer** and **audience** parameters. The primary **verification key** contains the key that the token was signed with, **issuer** is the secure token service that issues the token. The **audience** (sometimes called **scope**) describes the intent of the token or the resource the token authorizes access to. The Media Services key delivery service validates that these values in the token match the values in the template.

### PlayReady
When protecting your content with **PlayReady**, one of the things you need to specify in your authorization policy is an XML string that defines the PlayReady license template. By default, the following policy is set:

<PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1">
      <LicenseTemplates>
        <PlayReadyLicenseTemplate><AllowTestDevices>true</AllowTestDevices>
          <ContentKey i:type="ContentEncryptionKeyFromHeader" />
          <LicenseType>Nonpersistent</LicenseType>
          <PlayRight>
            <AllowPassingVideoContentToUnknownOutput>Allowed</AllowPassingVideoContentToUnknownOutput>
          </PlayRight>
        </PlayReadyLicenseTemplate>
      </LicenseTemplates>
    </PlayReadyLicenseResponseTemplate>

You can click the **import policy xml** button and provide a different XML that conforms to the  XML Schema defined [here](media-services-playready-license-template-overview.md).

## Next steps
Review Media Services learning paths.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## Provide feedback
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[open_policy]: ./media/media-services-portal-configure-content-key-auth-policy/media-services-protect-content-with-open-restriction.png
[token_policy]: ./media/media-services-key-authorization-policy/media-services-protect-content-with-token-restriction.png


---
title: Restrictions and known issues in Azure API Management API import | Microsoft Docs
description: Details of known issues and restrictions on import into Azure API Management using the Open API, WSDL or WADL formats.
services: api-management
documentationcenter: ''
author: vladvino
manager: vlvinogr
editor: ''

ms.assetid: 7a5a63f0-3e72-49d3-a28c-1bb23ab495e2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2017
ms.author: apipm

---
# API import restrictions and known issues
## About this list
When importing an API, you might come across some restrictions or identify issues that need to be rectified before you can successfully import. This article documents these, organized by the import format of the API.

## <a name="open-api"> </a>Open API/Swagger
If you are receiving errors importing your Open API document, ensure you have validated it - either using the designer in the Azure portal (Design - Front End - Open API Specification Editor), or with a third-party tool such as <a href="http://www.swagger.io">Swagger Editor</a>.

* **Host Name** APIM requires a host name attribute.
* **Base Path**  APIM requires a base path attribute.
* **Schemes**  APIM requires a scheme array. 

## <a name="wsdl"> </a>WSDL
WSDL files are used to generate SOAP Pass-through APIs or serve as the backend of a SOAP-to-REST API.

* **WSDL:Import** - Currently, APIM  does not support APIs using this attribute. Customers should merge the imported elements into one document.
* **Messages with multiple parts** Currently, APIM  does not support these types of messages.
* **WCF wsHttpBinding** SOAP services created with Windows Communication Foundation should use basicHttpBinding - wsHttpBinding is not supported.
* **MTOM** Services using MTOM <em>may</em> work. Official support is not offered at this time.
* **Recursion** types that are defined recursively (for example, refer to an array of themselves) are not supported by APIM.

## <a name="wadl"> </a>WADL
Currently, there are no known WADL import issues.

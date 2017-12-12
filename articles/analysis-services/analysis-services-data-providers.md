---
title: Client libraries required for connecting to Azure Analysis Services | Microsoft Docs
description: Describes client libraries required for client applications and tools to connect Azure Analysis Services
services: analysis-services
documentationcenter: ''
author: minewiskan
manager: kfile
editor: ''
tags: ''

ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 12/04/2017
ms.author: owend

---

# Client libraries for connecting to Azure Analysis Services

Client libraries are necessary for client applications and tools to connect to Analysis Services servers. 

## Download the latest client libraries  

|Download  |Version  | 
|---------|---------|
|[MSOLAP (amd64)](https://go.microsoft.com/fwlink/?linkid=829576)    |    14.0.1000.397      |
|[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)     |    14.0.1000.397      |
|[AMO](https://go.microsoft.com/fwlink/?linkid=829578)     |   14.0.800.218      |
|[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)     |    14.0.1000.397      |

## Understanding client libraries

Analysis Services utilize three client libraries, also known as data providers. ADOMD.NET and Analysis Services Management Objects (AMO) are managed client libraries. The Analysis Services OLE DB Provider (MSOLAP DLL) is a native client library. Typically, all three are installed at the same time. **Azure Analysis Services requires the latest versions of all three libraries**. 

Microsoft client applications like Power BI Desktop and Excel install all three client libraries and update them when new versions are available. Depending on the version or frequency of updates, some client libraries may not be the latest versions required by Azure Analysis Services. The same applies to custom applications or other interfaces such as AsCmd, TOM, ADOMD.NET. These applications require manually or programmatically installing the libraries. The client libraries for manual installation are included in SQL Server feature packs as distributable packages. However, these client libraries are tied to the SQL Server version and may not be the latest.  

Client libraries for client connections are different from data providers required to connect from an Azure Analysis Services server to a data source. To learn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).

## Client library types

### Analysis Services OLE DB Provider (MSOLAP) 

 Analysis Services OLE DB Provider (MSOLAP) is the native client library for Analysis Services database connections. It's used indirectly by both ADOMD.NET and AMO, delegating connection requests to the data provider. You can also call the OLE DB Provider directly from application code.  
  
 The Analysis Services OLE DB Provider is installed automatically by most tools and client applications used to access Analysis Services databases. It must be installed on computers used to access Analysis Services data.  
  
 OLE DB providers are often specified in connection strings. An Analysis Services connection string uses a different nomenclature to refer to the OLE DB Provider: MSOLAP.\<version>.dll.

### AMO  

 AMO is a managed client library used for server administration and data definition. It's installed and used by tools and client applications. For example, SQL Server Management Studio (SSMS) uses AMO to connect to Analysis Services.  
  
 A connection using AMO is typically minimal, consisting of `“data source=\<servername>”`. After a connection is established, you use the API to work with database collections and major objects. Both SSDT and SSMS use AMO to connect to an Analysis Services instance.  

  
### ADOMD

 ADOMD.NET is a managed data client library used for querying Analysis Services data. It's installed and used by tools and client applications. 
  
 When connecting to a database, the connection string properties for all three libraries are similar. Almost any connection string you define for ADOMD.NET by using  [Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString](https://msdn.microsoft.com/library/microsoft.analysisservices.adomdclient.adomdconnection.connectionstring.aspx) also works for AMO and the Analysis Services OLE DB Provider (MSOLAP). To learn more, see [Connection string properties &#40;Analysis Services&#41;](https://docs.microsoft.com/sql/analysis-services/instances/connection-string-properties-analysis-services).  

  
##  <a name="bkmk_LibUpdate"></a> How to determine client library version   
  
### OLEDDB (MSOLAP)  
  
1.  Go to `C:\Program Files\Microsoft Analysis Services\AS OLEDB\140`. If you have more than one folder, choose the higher number.
  
2.  Right-click **msolap140.dll** > **Properties** > **Details**.  
    
    ![Client library details](media/analysis-services-data-providers/aas-msolap-details.png)
  
### AMO

1. Go to `C:\Windows\Microsoft.NET\assembly\GAC_MSIL\Microsoft.AnalysisServices\v4.0_14.0.0.0__89845dcd8080cc91`.
2. Right-click **Microsoft.AnalysisServices** > **Properties** > **Details**.  

### ADOMD

1. Go to `C:\Windows\Microsoft.NET\assembly\GAC_MSIL\Microsoft.AnalysisServices.AdomdClient\v4.0_14.0.0.0__89845dcd8080cc91`.
2. Right-click **Microsoft.AnalysisServices.AdomdClient** > **Properties** > **Details**.  


## Next steps
[Connect with Excel](analysis-services-connect-excel.md)    
[Connect with Power BI](analysis-services-connect-pbi.md)

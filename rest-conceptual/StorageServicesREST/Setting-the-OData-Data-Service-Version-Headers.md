---
title: "Setting the OData Data Service Version Headers"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 086d4db0-0743-4987-b8a7-2cd15090dfd6
caps.latest.revision: 6
author: tamram
manager: carolz
translation.priority.mt: 
  - de-de
  - es-es
  - fr-fr
  - it-it
  - ja-jp
  - ko-kr
  - pt-br
  - ru-ru
  - zh-cn
  - zh-tw
---
# Setting the OData Data Service Version Headers
The following Table service operations are OData-compatible:  
  
-   [Query Tables](../StorageServicesREST/Query-Tables.md)  
  
-   [Create Table](../StorageServicesREST/Create-Table.md)  
  
-   [Query Entities](../StorageServicesREST/Query-Entities.md)  
  
-   [Insert Entity](../StorageServicesREST/Insert-Entity.md)  
  
-   [Update Entity](../StorageServicesREST/Update-Entity2.md)  
  
-   [Merge Entity](../StorageServicesREST/Merge-Entity.md)  
  
-   [Delete Entity](../StorageServicesREST/Delete-Entity1.md)  
  
-   [Insert Or Replace Entity](../StorageServicesREST/Insert-Or-Replace-Entity.md)  
  
-   [Insert Or Merge Entity](../StorageServicesREST/Insert-Or-Merge-Entity.md)  
  
 When you call one of these operations, you must specify the OData data service version, using one of the following request headers:  
  
-   `MaxDataServiceVersion`, to specify the maximum data service version  
  
-   `DataServiceVersion`, to specify the exact data service version  
  
 If both headers are present, precedence is given to `MaxDataServiceVersion`.  
  
 Note that the headers which specify the OData protocol version are similar to the `x-ms-version` header, which indicates the version of the Table service to use when making a request against the service. You must specify both headers for the operations listed above.  
  
 Not all versions of the Table service are compatible with all OData data service versions, so you must ensure that both `x-ms-version` and `DataServiceVersion`/`MaxDataServiceVersion` are set to compatible versions, as summarized in the following table:  
  
|DataServiceVersion/MaxDataServiceVersion Header Value|Compatible Table Service Versions (x-ms-version Header Values)|  
|------------------------------------------------------------|------------------------------------------------------------------------|  
|1.0;NetFx|Any version|  
|[2.0;NetFx](http://www.odata.org/)|2011-08-18 or later|  
|[3.0;NetFx](http://www.odata.org/)|2013-08-15 or later|  
  
 Note that if you are accessing the Table service using the Azure Storage Client Library, these headers are automatically set for you.  
  
## See Also  
 [Table Service Concepts](../StorageServicesREST/Table-Service-Concepts.md)
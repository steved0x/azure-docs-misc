---
title: "Setting the Prefer Header to Manage Response Echo on Insert Operations"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 018572c7-bcee-41f8-abfa-d38ef71fedbc
caps.latest.revision: 5
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
# Setting the Prefer Header to Manage Response Echo on Insert Operations
By default, the [Create Table](../StorageServicesREST/Create-Table.md) and [Insert Entity](../StorageServicesREST/Insert-Entity.md) operations return a response payload that echoes the data contained in the request body. For version 2013-08-15 and higher of the storage services and OData data service version 3.0, it is possible to omit the response body echo by setting the `Prefer` header to `return-no-content`. If the `Prefer` header is set to `return-no-content`, the service will respond with status code 204 (`No Content`) and response header `Preference-Applied:``return-no-content`.  
  
 You can also set the `Prefer` header to `return-content`, which provides the default behavior of returning the response payload. In this case, the service will respond with status code 201 (`Created`) and response header `Preference-Applied:``return-content`.  
  
 If no `Prefer` header is specified, the service responds with status code 201 (`Created`) without the `Preference-Applied` header in the response.  
  
 For more details, see the documentation for the [OData Prefer header](http://msdn.microsoft.com/library/hh537533.aspx).  
  
## See Also  
 [Setting the OData Data Service Version Headers](../StorageServicesREST/Setting-the-OData-Data-Service-Version-Headers.md)   
 [Table Service Concepts](../StorageServicesREST/Table-Service-Concepts.md)
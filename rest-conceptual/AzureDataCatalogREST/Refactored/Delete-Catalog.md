---
title: "Delete Catalog"
ms.custom: na
ms.date: 2016-07-21
ms.prod: azure
ms.reviewer: na
ms.service: data-catalog
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 75fafe77-a1f6-4c64-85f2-f18403364046
caps.latest.revision: 6
author: spelluru
manager: jhubbard
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
# Delete Catalog
Deletes a catalog.  
  
**Required**  
  
Azure Resource Manager requests must be **Authorized**, see [Authenticating Azure Resource Manager requests](https://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
    DELETE https://management.azure.com/subscriptions/<subscriptionId>/resourceGroups/<rgName>/providers/Microsoft.DataCatalog/catalogs/<catalogName>  
  
## Request  
  
### Headers  
None  
  
### Body Example  
None  
  
### Example Response Headers  
|Name|Value  
|---|---  
|Access-Control-Allow-Origin|*,*  
|Cache-Control|no-cache,no-cache,no-store  
|Content-Length|0  
|Content-Type|application/json; charset=utf-8  
|Date|Wed,02 Mar 2016 01:42:46 GMT  
|Expires|-1  
  
## Response  
  
### Status codes  
|**Code**|**Description**  
|---|---  
|200|OK. An existing annotation was updated.  
|204 | No Content (didn't exist).  
|202 | Accepted. Delete is asynchronous. In this case, the caller needs to read the Location header for an URL to poll. That URL will continue to return 202 until the operation is complete. When it stops returning 202, the response it gives back is the result of the DELETE operation.  
|400 | Bad request.  

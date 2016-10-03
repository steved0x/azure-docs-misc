---
title: "Table Service REST API"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 8e8a98bc-9cd0-42c2-b0aa-be6a4065c35c
caps.latest.revision: 29
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
# Table Service REST API
The Table service offers structured storage in the form of tables. The Table service API is a REST API for working with tables and the data that they contain.  
  
## REST API Operations  
 The REST API for the Table service includes the operations listed in the following table.  
  
|Operation|Description|  
|---------------|-----------------|  
|[Set Table Service Properties](../rest-conceptual/Set-Table-Service-Properties.md)|Sets the properties of the Table service.|  
|[Get Table Service Properties](../rest-conceptual/Get-Table-Service-Properties.md)|Gets the properties of the Table service.|  
|[Preflight Table Request](../rest-conceptual/Preflight-Table-Request.md)|Queries the Cross-Origin Resource Sharing (CORS) rules for the Table service prior to sending the actual request.|  
|[Get Table Service Stats](../rest-conceptual/Get-Table-Service-Stats.md)|Retrieves statistics related to replication for the Table service. This operation is only available on the secondary location endpoint when read-access geo-redundant replication is enabled for the storage account.|  
|[Query Tables](../rest-conceptual/Query-Tables.md)|Enumerates the tables in a storage account.|  
|[Create Table](../rest-conceptual/Create-Table.md)|Creates a new table within a storage account.|  
|[Delete Table](../rest-conceptual/Delete-Table.md)|Deletes a table from a storage account.|  
|[Get Table ACL](../rest-conceptual/Get-Table-ACL.md)|Returns details about any stored access policies specified on the table that may be used with Shared Access Signatures.|  
|[Set Table ACL](../rest-conceptual/Set-Table-ACL.md)|Sets details about any stored access policies specified on the table that may be used with Shared Access Signatures.|  
|[Query Entities](../rest-conceptual/Query-Entities.md)|Queries data in a table.|  
|[Insert Entity](../rest-conceptual/Insert-Entity.md)|Inserts a new entity into a table.|  
|[Insert Or Merge Entity](../rest-conceptual/Insert-Or-Merge-Entity.md)|Inserts or merges an entity in a table.|  
|[Insert Or Replace Entity](../rest-conceptual/Insert-Or-Replace-Entity.md)|Inserts or replaces an entity in a table.|  
|[Update Entity](../rest-conceptual/Update-Entity2.md)|Updates an existing entity within a table by replacing it.|  
|[Merge Entity](../rest-conceptual/Merge-Entity.md)|Updates an existing entity within a table by merging new property values into the entity.|  
|[Delete Entity](../rest-conceptual/Delete-Entity1.md)|Deletes an entity within a table|  
  
## Entity Group Transactions  
 The Table service supports batch operations for [Insert Entity](../rest-conceptual/Insert-Entity.md), [Update Entity](../rest-conceptual/Update-Entity2.md), [Merge Entity](../rest-conceptual/Merge-Entity.md), and [Delete Entity](../rest-conceptual/Delete-Entity1.md) operations. For more information about batch operations, see [Performing Entity Group Transactions](../rest-conceptual/Performing-Entity-Group-Transactions.md).  
  
## In This Section  
 [Summary of Table Service Functionality](../rest-conceptual/Summary-of-Table-Service-Functionality.md)  
  
 [Table Service Concepts](../rest-conceptual/Table-Service-Concepts.md)  
  
 [Operations on the Account (Table Service)](../rest-conceptual/Operations-on-the-Account--Table-Service-.md)  
  
 [Operations on Tables](../rest-conceptual/Operations-on-Tables.md)  
  
 [Operations on Entities](../rest-conceptual/Operations-on-Entities.md)  
  
## See Also  
 [Storage Services REST](../rest-conceptual/Azure-Storage-Services-REST-API-Reference.md)
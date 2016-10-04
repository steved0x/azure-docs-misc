---
title: "Addressing Table Service Resources"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 238c4c0e-da32-416d-99ba-c02f24f00cfb
caps.latest.revision: 36
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
# Addressing Table Service Resources
The Table service exposes the following resources via the REST API:  
  
-   **Account.** The storage account is a uniquely identified entity within the storage system. The storage account is the parent namespace for the Table service. All tables are associated with an account.  
  
-   **Tables.** The Tables resource represents the set of tables within a given storage account.  
  
-   **Entity.** An individual table stores data as a collection of entities.  
  
## Resource URI Syntax  
 The base URI for Table service resources is the storage account:  
  
```  
https://myaccount.table.core.windows.net  
```  
  
 To list the tables in a given storage account, to create a new table, or to delete a table, refer to the set of tables in the specified storage account:  
  
```  
https://myaccount.table.core.windows.net/Tables  
```  
  
 To return a single table, name that table within the Tables collection, as follows:  
  
```  
https://myaccount.table.core.windows.net/Tables('MyTable')  
```  
  
 To query entities in a table, or to insert, update, or delete an entity, refer to that table directly within the storage account. This basic syntax refers to the set of all entities in the named table:  
  
```  
https://myaccount.table.core.windows.net/MyTable()  
```  
  
 The format for addressing data resources for queries conforms to that specified by the [OData Protocol Specification](http://www.odata.org/). You can use this syntax to filter entities based on criteria specified on the URI.  
  
 Note that all values for query parameters must be URL encoded before they are sent to the Azure storage services.  
  
## Supported HTTP Operations  
 Each resource supports operations based on the HTTP verbs GET, PUT, HEAD, and DELETE. The verb, syntax, and supported HTTP version(s) for each operation appears on the reference page for each operation. For a complete list of operation reference pages, see [Table Service REST API](../StorageServicesREST/Table-Service-REST-API.md).  
  
## See Also  
 [Table Service REST API](../StorageServicesREST/Table-Service-REST-API.md)   
 [Understanding the Table Service Data Model](../StorageServicesREST/Understanding-the-Table-Service-Data-Model.md)   
 [Query Timeout and Pagination](../StorageServicesREST/Query-Timeout-and-Pagination.md)   
 [Operations on Tables](../StorageServicesREST/Operations-on-Tables.md)   
 [Operations on Entities](../StorageServicesREST/Operations-on-Entities.md)
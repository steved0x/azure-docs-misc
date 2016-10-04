---
title: "Summary of Table Service Functionality"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: db7c3e5d-09a0-46d8-a2b7-00a0c4e75f0c
caps.latest.revision: 43
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
# Summary of Table Service Functionality
The Table service REST API is compliant with the [OData Protocol Specification](http://www.odata.org/), with some differences, as described in the following sections.  
  
 [Table Service Extensions](#TableServiceExtensions)  
  
 [Table Service Restrictions](#TableServiceRestrictions)  
  
##  <a name="TableServiceExtensions"></a> Table Service Extensions  
 The Table service extends the functionality of OData in the following ways.  
  
### Shared Key and Shared Key Lite Authentication  
 The Table service requires that each request be authenticated. Both Shared Key and Shared Key Lite authentication are supported. Shared Key authentication is more secure and is recommended for requests made against the Table service using the REST API.  
  
 For more information about authenticating requests, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).  
  
### Continuation Tokens for Query Pagination  
 A query against the Table service may return a maximum of 1,000 items at one time and may execute for a maximum of five seconds. If the result set contains more than 1,000 items, or if the query did not complete within five seconds, the response includes headers which provide the developer with continuation tokens to use in order to resume the query at the next item in the result set. Continuation token headers may be returned for a [Query Tables](../StorageServicesREST/Query-Tables.md) operation or a [Query Entities](../StorageServicesREST/Query-Entities.md) operation.  
  
 Note that the total time allotted to the request for scheduling and processing the query is 30 seconds, including the five seconds for query execution.  
  
 For more information about continuation tokens, see [Query Timeout and Pagination](../StorageServicesREST/Query-Timeout-and-Pagination.md).  
  
### Primary Key System Properties  
 Every entity in the Table service has two key properties: the `PartitionKey` property and the `RowKey` property. These properties together form the table's primary key and uniquely identify each entity in the table.  
  
 Both properties require string values. It is the developer's responsibility to provide values for these properties when a new entity is inserted, and to include them in any update or delete operation on an entity.  
  
 For more information about these required key properties, see [Understanding the Table Service Data Model](../StorageServicesREST/Understanding-the-Table-Service-Data-Model.md).  
  
### Timestamp System Property  
 Every entity in the Table service has a `Timestamp` system property. The `Timestamp` property is a `DateTime` value that is maintained on the server side to record the time an entity was last modified. The Table service uses the `Timestamp` property internally to provide optimistic concurrency. The value of `Timestamp` is a monotonically increasing value, meaning that each time the entity is modified, the value of `Timestamp` increases for that entity. This property should not be set on insert or update operations (the value will be ignored).  
  
 For more information about the `Timestamp` property, see [Understanding the Table Service Data Model](../StorageServicesREST/Understanding-the-Table-Service-Data-Model.md).  
  
### Batch Operations  
 The Table service supports batch transactions on entities that are in the same table and belong to the same partition group, which means they have the same `PartitionKey` value. This allows multiple insert, update, merge, and delete operations to be supported within a single atomic transaction. The Table service supports a subset of the functionality provided by the [OData protocol](http://www.odata.org/).  
  
 For more information about batch operations, see [Performing Entity Group Transactions](../StorageServicesREST/Performing-Entity-Group-Transactions.md).  
  
##  <a name="TableServiceRestrictions"></a> Table Service Restrictions  
 The Table service has the following restrictions on functionality provided by OData.  
  
### Credentials Property  
 The Table service does not support using the [Credentials](http://go.microsoft.com/fwlink/?LinkId=154550) property of the [DataServiceContext](http://go.microsoft.com/fwlink/?linkid=151839) class to authenticate a request. Instead, you must authenticate a request against the Table service by adding an `Authorization` header to the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).  
  
### Property Types  
 Not all property types supported by the OData are supported by the Table service. For a list of supported property types, see [Understanding the Table Service Data Model](../StorageServicesREST/Understanding-the-Table-Service-Data-Model.md).  
  
### Operations on Links  
 The Table service does not currently support links between tables. Links are associative relationships between data.  
  
### Operations on Select Properties  
 Projection refers to querying a subset of the properties for an entity or entities. It is analogous to selecting a subset of the columns or properties of a table when querying in LINQ. Projection reduces the amount of data that must be returned by a query by specifying that only certain properties are returned in the response. Projection is supported as part of the 2011-08-18 version of the Azure storage services. For more information, refer to [Query Entities](../StorageServicesREST/Query-Entities.md), [Writing LINQ Queries Against the Table Service](../StorageServicesREST/Writing-LINQ-Queries-Against-the-Table-Service.md), and [OData: Select System Query Option ($select)](http://www.odata.org/).  
  
### LINQ Query Operators  
 The Table service supports using language-integrated queries (LINQ). Only these LINQ query operators are supported for use with the Table service:  
  
-   `From`  
  
-   `Where`  
  
-   `Take`  
  
 For more information, see [Query Operators Supported for the Table Service](../StorageServicesREST/Query-Operators-Supported-for-the-Table-Service.md).  
  
### LINQ Comparison Operators  
 The Table service supports using a subset of the comparison operators provided by LINQ. For more information, see [Querying Tables and Entities](../StorageServicesREST/Querying-Tables-and-Entities.md) and [Writing LINQ Queries Against the Table Service](../StorageServicesREST/Writing-LINQ-Queries-Against-the-Table-Service.md).  
  
### GetMetadataURI Method  
 The Table service supports the [GetMetadataURI](http://msdn.microsoft.com/library/system.data.services.client.dataservicecontext.getmetadatauri.aspx) method of the [DataServiceContext](http://msdn.microsoft.com/library/system.data.services.client.dataservicecontext.aspx) class, but it does not return any schema information beyond the three fixed schema properties. These properties are `PartitionKey`, `RowKey`, and `Timestamp`.  
  
### Payload Formats  
 OData supports sending payloads in JSON format. The Azure Table service supports the OData JSON format as of API version 2013-08-15, with the OData data service version set to 3.0; prior versions do not support the JSON format.  
  
 Atom payloads are supported in all versions prior to 2015-12-11. Version 2015-12-11 and newer support only JSON payloads.  
  
> [!NOTE]
>  JSON is the recommended payload format, and is the only format supported for versions 2015-12-11 and later.  
  
 For more information, see [Payload Format for Table Service Operations](../StorageServicesREST/Payload-Format-for-Table-Service-Operations.md) and [Setting the OData Data Service Version Headers](../StorageServicesREST/Setting-the-OData-Data-Service-Version-Headers.md).  
  
## See Also  
 [Table Service REST API](../StorageServicesREST/Table-Service-REST-API.md)
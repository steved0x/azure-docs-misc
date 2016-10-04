---
title: "Query Timeout and Pagination"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: d962e4c0-709a-4f04-a296-32a49d82c799
caps.latest.revision: 37
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
# Query Timeout and Pagination
The Table service supports the following two types of query operations:  
  
-   The [Query Tables](../StorageServicesREST/Query-Tables.md) operation returns the list of tables within the specified storage account. The list of tables may be filtered according to criteria specified on the request.  
  
-   The [Query Entities](../StorageServicesREST/Query-Entities.md) operation returns a set of entities from the specified table. Query results may be filtered according to criteria specified on the request.  
  
 A query against the Table service may return a maximum of 1,000 items at one time and may execute for a maximum of five seconds. If the result set contains more than 1,000 items, if the query did not complete within five seconds, or if the query crosses the partition boundary, the response includes headers which provide the developer with continuation tokens to use in order to resume the query at the next item in the result set. Continuation token headers may be returned for a [Query Tables](../StorageServicesREST/Query-Tables.md) operation or a [Query Entities](../StorageServicesREST/Query-Entities.md) operation.  
  
 Note that the total time allotted to the request for scheduling and processing the query is 30 seconds, including the five seconds for query execution.  
  
 It is possible for a query to return no results but to still return a continuation header.  
  
 The continuation token headers are shown in the following table.  
  
|Continuation token header|Description|  
|-------------------------------|-----------------|  
|`x-ms-continuation-NextTableName`|This header is returned in the context of a [Query Tables](../StorageServicesREST/Query-Tables.md) operation. If the list of tables returned is not complete, a hash of the name of the next table in the list is included in the continuation token header.|  
|`x-ms-continuation-NextPartitionKey`|This header is returned in the context of a [Query Entities](../StorageServicesREST/Query-Entities.md) operation. The header contains a hash of the next partition key to be returned in a subsequent query against the table.|  
|`x-ms-continuation-NextRowKey`|This header is returned in the context of a [Query Entities](../StorageServicesREST/Query-Entities.md) operation. The header contains a hash of the next row key to be returned in a subsequent query against the table.<br /><br /> Note that in some instances, `x-ms-continuation-NextRowKey` may be `null`.|  
  
 To retrieve the continuation tokens and execute a subsequent query to return the next page of results, first inspect the response headers for continuation tokens. If there are no headers or the header values are `null`, there are no additional entities to return.  
  
> [!NOTE]
>  When making subsequent requests that include continuation tokens, be sure to pass the original URI on the request. For example, if you have specified a `$filter`, `$select`, or `$top` query option as part of the original request, you will want to include that option on subsequent requests. Otherwise your subsequent requests may return unexpected results.  
>   
>  Note that the `$top` query option in this case specifies the maximum number of results per page, not the maximum number of results in the whole response set.  
>   
>  See [Querying Tables and Entities](../StorageServicesREST/Querying-Tables-and-Entities.md) for more details.  
  
 If you are handling continuation tokens manually using the Microsoft .NET Client Library, first cast the result of the query operation to a [QueryOperationResponse](http://go.microsoft.com/fwlink/?LinkId=155325) object. You can then access the continuation token headers in the [Headers](http://go.microsoft.com/fwlink/?LinkId=155326) property of the `QueryOperationResponse` object.  
  
 After you have retrieved the continuation tokens, use their values to construct a query to return the next page of results. A query request URI may take these parameters, which correspond to the continuation token headers returned with the response:  
  
-   `NextTableName`  
  
-   `NextPartitionKey`  
  
-   `NextRowKey`  
  
> [!NOTE]
>  The total time allotted to the request for scheduling and processing a query is 30 seconds, including five seconds for query execution.  
>   
>  If the operation is an insert, update, or delete operation, the operation may have succeeded on the server despite an error being returned by the client. This may happen when the client timeout is set to less than 30 seconds, which is the maximum timeout for an insert, update, or delete operation.  
  
## Sample Response Headers and Subsequent Request  
 The following code example shows a set of sample response headers from an entity query against a table named Customers that returns continuation headers. Both `x-ms-continuation-NextPartitionKey` and `x-ms-continuation-NextRowKey` are returned.  
  
```  
Date: Mon, 27 Jun 2016 20:11:08 GMT  
Content-Type: application/json;charset=utf-8  
Server: Windows-Azure-Table/1.0 Microsoft-HTTPAPI/2.0  
Cache-Control: no-cache  
x-ms-request-id: f9b2cd09-4dec-4570-b06d-4fa30179a58e  
x-ms-version: 2015-12-11  
x-ms-continuation-NextPartitionKey: 1!8!U21pdGg-  
x-ms-continuation-NextRowKey: 1!8!QmVuOTk5  
Content-Length: 880298  
```  
  
 The request for the next page of data can be constructed like the following URI:  
  
```  
http://myaccount.table.core.windows.net/Customers?NextPartitionKey=1!8!U21pdGg-&NextRowKey=1!12!QmVuMTg5OA--  
```  
  
## See Also  
 [Addressing Table Service Resources](../StorageServicesREST/Addressing-Table-Service-Resources.md)   
 [Operations on Tables](../StorageServicesREST/Operations-on-Tables.md)   
 [Operations on Entities](../StorageServicesREST/Operations-on-Entities.md)
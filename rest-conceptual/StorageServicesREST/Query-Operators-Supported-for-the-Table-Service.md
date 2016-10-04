---
title: "Query Operators Supported for the Table Service"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: de258a1e-4101-4443-88cb-f9d156f04246
caps.latest.revision: 22
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
# Query Operators Supported for the Table Service
The Microsoft® .NET Client Library supports data service queries by using [language-integrated queries (LINQ)](http://go.microsoft.com/fwlink/?LinkId=137420). The client library handles the details of mapping the LINQ statement to the appropriate URI for the Table service and of retrieving the specified resources as .NET objects.  
  
## LINQ Query Operators  
 The following tables note which LINQ query operators are supported for use with the Table service. For more information about LINQ query operators, see [LINQ: .NET Language-Integrated Query](http://go.microsoft.com/fwlink/?LinkId=137420).  
  
### Supported Query Operators  
  
|LINQ operator|Table service support|Additional information|  
|-------------------|---------------------------|----------------------------|  
|`From`|Supported as defined.||  
|`Where`|Supported as defined.||  
|`Take`|Supported, with some restrictions.|The value specified for the `Take` operator must be less than or equal to 1,000. If it is greater than 1,000, the service returns status code 400 (Bad Request).<br /><br /> If the `Take` operator is not specified, a maximum of 1,000 entries will be returned.|  
|`First, FirstOrDefault`|Supported.||  
|`Select`|Supported for version 2011-08-18 and newer.|Projection is supported. For more information, see [Writing LINQ Queries Against the Table Service](../StorageServicesREST/Writing-LINQ-Queries-Against-the-Table-Service.md).|  
  
### Unsupported Query Operators  
  
|LINQ operator|Table service support|Additional information|  
|-------------------|---------------------------|----------------------------|  
|`GroupBy`|Not Supported.||  
|`OrderBy, OrderByDescending`|Not Supported.||  
|`ThenBy, ThenByDescending`|Not Supported.||  
|`Average`|Not Supported.||  
|`Min`|Not Supported.||  
|`Max`|Not Supported.||  
|`Last, LastOrDefault`|Not Supported.||  
|`Skip`<br /><br /> `Count, LongCount`|Not Supported.||  
|`Sum`|Not Supported.||  
|`TakeWhile`|Not Supported.||  
|`SkipWhile`|Not Supported.||  
|`Join, GroupJoin`|Not Supported.||  
|`Single`|Not Supported.||  
|`OfType`|Not Supported.||  
|`SelectMany`|Not Supported.||  
|`Concat`|Not Supported.||  
|`ElementAt, ElemenatAtOrDefault`|Not Supported.||  
|`Distinct`|Not Supported.||  
|`Except`|Not Supported.||  
|`Intersect`|Not Supported.||  
|`Union`|Not Supported.||  
|`All`|Not Supported.||  
|`Any`|Not Supported.||  
|`Contains`|Not Supported.||  
|`SequenceEqual`|Not Supported.||  
|`Empty, Range, Repeat`|Not Supported.||  
|`SingleOrDefault`|Not Supported.||  
|`Reverse`|Not Supported.||  
  
## See Also  
 [Table Service Concepts](../StorageServicesREST/Table-Service-Concepts.md)
---
title: "Querying Tables and Entities"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 74e73539-b624-4f47-8603-112cbb6780db
caps.latest.revision: 35
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
# Querying Tables and Entities
Querying tables and entities in the Table service requires careful construction of the request URI. The following sections describe query options and demonstrate some common scenarios.  
  
## Basic Query Syntax  
 To return all of the tables in a given storage account, perform a `GET` operation on the Tables resource, as described in the [Query Tables](../StorageServicesREST/Query-Tables.md) operation. The basic URI for addressing the Tables resource is as follows:  
  
```  
https://myaccount.table.core.windows.net/Tables  
```  
  
 To return a single named table, specify that table as follows:  
  
```  
https://myaccount.table.core.windows.net/Tables('MyTable')  
```  
  
 To return all entities in a table, specify the table name on the URI, without the Tables resource:  
  
```  
https://myaccount.table.core.windows.net/MyTable()  
```  
  
 Query results are sorted by `PartitionKey`, then by `RowKey`. Ordering results in any other way is not currently supported.  
  
 You can specify additional options to limit the set of tables or entities returned, as described in the following **Supported Query Options** section.  
  
> [!NOTE]
>  The number of entities returned for a single request may be limited, if the query exceeds the maximum number of entities, exceeds the timeout interval, or crosses a partition boundary. For more information, see [Query Timeout and Pagination](../StorageServicesREST/Query-Timeout-and-Pagination.md).  
  
## Supported Query Options  
 The Table service supports the following query options, which conform to the [OData Protocol Specification](http://www.odata.org/). You can use these options to limit the set of tables, entities, or entity properties returned by a query.  
  
|System query option|Description|  
|-------------------------|-----------------|  
|`$filter`|Returns only tables or entities that satisfy the specified filter.<br /><br /> Note that no more than 15 discrete comparisons are permitted within a `$filter` string.|  
|`$top`|Returns only the top `n` tables or entities from the set.|  
|`$select`|Returns the desired properties of an entity from the set. This query option is only supported for requests using version 2011-08-18 or newer. For more information, see [Writing LINQ Queries Against the Table Service](../StorageServicesREST/Writing-LINQ-Queries-Against-the-Table-Service.md).|  
  
> [!NOTE]
>  A request that returns more than the default maximum or specified maximum number of results returns a continuation token for performing pagination. When making subsequent requests that include continuation tokens, be sure to pass the original URI on the request. For example, if you have specified a `$filter`, `$select`, or `$top` query option as part of the original request, you will want to include that option on subsequent requests. Otherwise your subsequent requests may return unexpected results. See [Query Timeout and Pagination](../StorageServicesREST/Query-Timeout-and-Pagination.md) for additional information.  
>   
>  Note that the `$top` query option in the case where results are paginated specifies the maximum number of results per page, not the maximum number of results in the whole response set.  
>   
>  Additional query options defined by OData are not supported by the Table service.  
  
## Supported Comparison Operators  
 Within a `$filter` clause, you can use comparison operators to specify the criteria against which to filter the query results.  
  
 For all property types, the following comparison operators are supported:  
  
|Operator|URI expression|  
|--------------|--------------------|  
|`Equal`|`eq`|  
|`GreaterThan`|`gt`|  
|`GreaterThanOrEqual`|`ge`|  
|`LessThan`|`lt`|  
|`LessThanOrEqual`|`le`|  
|`NotEqual`|`ne`|  
  
 Additionally, the following operators are supported for Boolean properties:  
  
|Operator|URI expression|  
|--------------|--------------------|  
|`And`|`and`|  
|`Not`|`not`|  
|`Or`|`or`|  
  
 For more information about filter syntax, see the [OData Protocol Specification](http://www.odata.org/).  
  
## Query String Encoding  
 The following characters must be encoded if they are to be used in a query string:  
  
-   Forward slash (/)  
  
-   Question mark (?)  
  
-   Colon (:)  
  
-   'At' symbol (@)  
  
-   Ampersand (&)  
  
-   Equals sign (=)  
  
-   Plus sign (+)  
  
-   Comma (,)  
  
-   Dollar sign ($)  
  
## Sample Query Expressions  
 The following samples show how to construct the request URI for some typical entity queries using REST syntax. The same queries could be written using LINQ syntax. For more information, see [Writing LINQ Queries Against the Table Service](../StorageServicesREST/Writing-LINQ-Queries-Against-the-Table-Service.md).  
  
 Note that both the `$top` and `$filter` options can be used to filter on table names as well, using the syntax demonstrated for filtering on properties of type `String`.  
  
### Returning the Top n Entities  
 To return the top `n` entities for any query, specify the `$top` query option. The following example returns the top 10 entities from a table named Customers:  
  
```  
https://myaccount.table.core.windows.net/Customers()?$top=10  
```  
  
### Filtering on the PartitionKey and RowKey Properties  
 Because the `PartitionKey` and `RowKey` properties form an entity's primary key, you can use a special syntax to identify the entity, as follows:  
  
```  
https://myaccount.table.core.windows.net/Customers(PartitionKey='MyPartition',RowKey='MyRowKey1')  
```  
  
 Alternatively, you can specify these properties as part of the `$filter` option, as shown in the following section.  
  
 Note that the key property names and constant values are case-sensitive. Both the `PartitionKey` and `RowKey` properties are of type `String`.  
  
### Constructing Filter Strings  
 When constructing a filter string, keep these rules in mind:  
  
-   Use the logical operators defined by the [OData Protocol Specification](http://www.odata.org/) to compare a property to a value. Note that it is not possible to compare a property to a dynamic value; one side of the expression must be a constant.  
  
-   The property name, operator, and constant value must be separated by URL-encoded spaces. A space is URL-encoded as `%20`.  
  
-   All parts of the filter string are case-sensitive.  
  
-   The constant value must be of the same data type as the property in order for the filter to return valid results. For more information about supported property types, see [Understanding the Table Service Data Model](../StorageServicesREST/Understanding-the-Table-Service-Data-Model.md).  
  
> [!NOTE]
>  Be sure to check whether a property has been explicitly typed before assuming it is of a type other than string. If a property has been explicitly typed, the type is indicated within the response when the entity is returned. If the property has not been explicitly typed, it will be of type `String`, and the type will not be indicated within the response when the entity is returned.  
  
#### Filtering on String Properties  
 When filtering on string properties, enclose the string constant in single quotes.  
  
 The following example filters on the `PartitionKey` and `RowKey` properties; additional non-key properties could also be added to the query string.  
  
```  
https://myaccount.table.core.windows.net/Customers()?$filter=PartitionKey%20eq%20'MyPartitionKey'%20and%20RowKey%20eq%20'MyRowKey1'  
```  
  
 The following example filters on a `FirstName` and `LastName` property:  
  
```  
https://myaccount.table.core.windows.net/Customers()?$filter=LastName%20eq%20'Smith'%20and%20FirstName%20eq%20'John'  
```  
  
 Note that the Table service does not support wildcard queries. However, you can perform prefix matching by using comparison operators on the desired prefix. The following example returns entities with a `LastName` property beginning with the letter 'A':  
  
```  
https://myaccount.table.core.windows.net/Customers()?$filter=LastName%20ge%20'A'%20and%20LastName%20lt%20'B'  
```  
  
#### Filtering on Numeric Properties  
 To filter on an integer or floating-point number, specify the constant value on the URI without quotes.  
  
 This example returns all entities with an `Age` property whose value is greater than 30:  
  
```  
https://myaccount.table.core.windows.net/Customers()?$filter=Age%20gt%2030  
```  
  
 This example returns all entities with an `AmountDue` property whose value is less than or equal to 100.25:  
  
```  
https://myaccount.table.core.windows.net/Customers()?$filter=AmountDue%20le%20100.25%20  
```  
  
#### Filtering on Boolean Properties  
 To filter on a Boolean value, specify `true` or `false` without quotes.  
  
 The following example returns all entities where the `IsActive` property is set to `true`:  
  
```  
https://myaccount.table.core.windows.net/Customers()?$filter=IsActive%20eq%20true  
```  
  
#### Filtering on DateTime Properties  
 To filter on a `DateTime` value, specify the `datetime` keyword on the URI, followed by the date/time constant in single quotes. The date/time constant must be in combined UTC format, as described in [Formatting DateTime Property Values](../StorageServicesREST/Formatting-DateTime-Property-Values.md).  
  
 The following example returns entities where the `CustomerSince` property is equal to July 10, 2008:  
  
```  
https://myaccount.table.core.windows.net/Customers()?$filter=CustomerSince%20eq%20datetime'2008-07-10T00:00:00Z'  
```  
  
## Filtering on GUID Properties  
 To filter on a GUID value, specify the `guid` keyword on the URI, followed by the guid constant in single quotes.  
  
 The following example returns entities where the `GuidValue` property is equal to :  
  
```  
https://myaccount.table.core.windows.net/Customers()?$filter=GuidValue%20eq%20guid'a455c695-df98-5678-aaaa-81d3367e5a34'  
```  
  
## See Also  
 [Table Service Concepts](../StorageServicesREST/Table-Service-Concepts.md)   
 [Understanding the Table Service Data Model](../StorageServicesREST/Understanding-the-Table-Service-Data-Model.md)   
 [Addressing Table Service Resources](../StorageServicesREST/Addressing-Table-Service-Resources.md)   
 [Query Timeout and Pagination](../StorageServicesREST/Query-Timeout-and-Pagination.md)   
 [Writing LINQ Queries Against the Table Service](../StorageServicesREST/Writing-LINQ-Queries-Against-the-Table-Service.md)
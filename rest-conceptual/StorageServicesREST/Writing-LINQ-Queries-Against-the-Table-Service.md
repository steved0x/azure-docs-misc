---
title: "Writing LINQ Queries Against the Table Service"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: c1ff6980-6c93-4327-9d19-69790370e1ee
caps.latest.revision: 21
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
# Writing LINQ Queries Against the Table Service
You can write queries against the Table service using LINQ syntax. The following examples show how to write sample queries similar to the sample queries shown in [Querying Tables and Entities](../StorageServicesREST/Querying-Tables-and-Entities.md), but using LINQ instead of the REST protocol.  
  
 The Table service supports executing simple queries that retrieve all properties of an entity; it's not possible to select a subset of an entity's properties. The Table service also supports filtering query results using the `Where` operator, and specifying how many entities to return using the `Take` operator.  
  
 For details about which LINQ operators are supported by the Table service, see [Query Operators Supported for the Table Service](../StorageServicesREST/Query-Operators-Supported-for-the-Table-Service.md).  
  
## Projecting Entity Properties  
 The LINQ `select` clause can be used to project a subset of properties from an entity or entities. The maximum number of properties that can be projected is 255, which is also the maximum number of properties in an entity.  
  
 To project an entity’s properties, the client must support OData Data Service Version 2.0, indicated by specifying either the `DataServiceVersion` or `MaxDataServiceVersion` headers as follows:  
  
```c#  
DataServiceVersion: 2.0;NetFx  
MaxDataServiceVersion: 2.0;NetFx  
```  
  
 The following example demonstrates how to project properties from a single entity, using the required object initializer:  
  
```c#  
var query = from entity in dataServiceContext.CreateQuery<SampleEntity>(tableName)  
                 where entity.PartitionKey == "MyPartitionKey"  
                 select new { entity.RowKey };  
```  
  
 The following example projects 3 properties from an entity that has 10 properties. In this example, `SampleEntity`’s 10 properties are letters from A through J:  
  
```c#  
IEnumerable<SampleEntity> query = from entity in  
                                       dataServiceContext.CreateQuery<SampleEntity>(tableName)  
                                       where entity.PartitionKey == "MyPartitionKey"  
                                       select new SampleEntity  
                                      {  
                                          PartitionKey = entity.PartitionKey,  
                                          RowKey = entity.RowKey,  
                                          A = entity.A,  
                                          D = entity.D,  
                                          I = entity.I  
                                      };  
```  
  
 Single entity projection is not supported. The REST request produced by the following code is invalid:  
  
```  
var query = from entity in dataServiceContext.CreateQuery<SampleEntity>(tableName)  
                 where entity.PartitionKey == "MyPartitionKey"  
                 select { entity.RowKey }; // this code is invalid!  
```  
  
 You can also project entity properties by using the **$select** query option in a standard REST request. For more information, see [Query Entities](../StorageServicesREST/Query-Entities.md).  
  
 For more information on entity projections and transformations, see [Select System Query Option ($select)](http://www.odata.org/) in the OData documentation.  
  
## Returning the Top n Entities  
 To return `n` entities, use the LINQ `Take` operator. Note that the maximum number of entities that may be returned in a single query is 1,000. Specifying a value greater than 1,000 for the `Take` operator results in error code 400 (Bad Request).  
  
 The following example returns the top 10 entities from a Customers table:  
  
```c#  
var query = (from entity in context.CreateQuery<Customer>("Top10Customers")  
                 select entity).Take(10);  
```  
  
## Filtering on String Properties  
 The following example filters on two String properties:  
  
```c#  
var query = from entity in context.CreateQuery<Customer>("SpecificCustomer")  
                 where entity.LastName.Equals("Smith")  
                 && entity.FirstName.Equals("John")  
                 select entity;  
```  
  
 The following example performs prefix matching using comparison operators to return entities with a `LastName` property beginning with the letter 'A':  
  
```ecmascript  
var query = from entity in context.CreateQuery<Customer>("CustomersA")  
                 where entity.LastName.CompareTo("A") >= 0  
                 && entity.LastName.CompareTo("B") < 0  
                 select entity;  
```  
  
## Filtering on Numeric Properties  
 The following example returns all entities with an `Age` property whose value is greater than 30:  
  
```c#  
var query = from entity in context.CreateQuery<Customer>("CustomersOver30")  
                 where entity.Age > 30  
                 select entity;  
```  
  
 This example returns all entities with an `AmountDue` property whose value is less than or equal to 100.25:  
  
```c#  
var query = from entity in context.CreateQuery<Customer>("CustomersAmountDue")  
                 where entity.AmountDue <= 100.25  
                 select entity;  
```  
  
## Filtering on Boolean Properties  
 The following example returns all entities where the `IsActive` property is set to `true`:  
  
```c#  
var query = from entity in context.CreateQuery<Customer>("ActiveCustomers")  
                 where entity.IsActive == true  
                 select entity;  
```  
  
## Filtering on DateTime Properties  
 The following example returns entities where the `CustomerSince` property is equal to July 10, 2008:  
  
```c#  
DateTime dt = new DateTime(2008, 7, 10);  
var query = from entity in context.CreateQuery<Customer>("CustomerSince")  
                 where entity.CustomerSince.Equals(dt)  
                 select entity;  
```  
  
## See Also  
 [Querying Tables and Entities](../StorageServicesREST/Querying-Tables-and-Entities.md)   
 [Query Operators Supported for the Table Service](../StorageServicesREST/Query-Operators-Supported-for-the-Table-Service.md)
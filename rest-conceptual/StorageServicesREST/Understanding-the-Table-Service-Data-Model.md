---
title: "Understanding the Table Service Data Model"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 01f78ed1-9cbd-4b00-8113-71129751357e
caps.latest.revision: 55
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
# Understanding the Table Service Data Model
The Table service offers structured storage in the form of tables. The following sections outline the Table service data model.  
  
## Storage Account  
 A storage account is a globally unique entity within the storage system. The storage account is the parent namespace for the Table service, and is the basis for authentication. You can create any number of tables within a given storage account, as long as each table is uniquely named.  
  
 The storage account must always be specified in the request URI. The base URI for accessing the Table service is as follows:  
  
```  
https://myaccount.table.core.windows.net  
```  
  
## Tables, Entities, and Properties  
 Tables store data as collections of entities. Entities are similar to rows. An entity has a primary key and a set of properties. A property is a name, typed-value pair, similar to a column.  
  
 The Table service does not enforce any schema for tables, so two entities in the same table may have different sets of properties. Developers may choose to enforce a schema on the client side. A table may contain any number of entities.  
  
### Table Names  
 Table names must conform to these rules:  
  
-   Table names must be unique within an account.  
  
-   Table names may contain only alphanumeric characters.  
  
-   Table names cannot begin with a numeric character.  
  
-   Table names are case-insensitive.  
  
-   Table names must be from 3 to 63 characters long.  
  
-   Some table names are reserved, including "tables". Attempting to create a table with a reserved table name returns error code 404 (Bad Request).  
  
 These rules are also described by the regular expression "^[A-Za-z][A-Za-z0-9]{2,62}$".  
  
 Table names preserve the case with which they were created, but are case-insensitive when used.  
  
### Property Names  
 Property names are case-sensitive strings up to 255 characters in size. Property names should follow naming rules for [C# identifiers](http://go.microsoft.com/fwlink/?LinkId=155321).  
  
> [!NOTE]
>  Some C# identifiers are not valid according to the [XML specification](http://go.microsoft.com/fwlink/?LinkId=155322). These identifiers may not be used in property names, because property names are sent via an XML payload in a request against the Table service.  
  
> [!IMPORTANT]
>  Property names are passed to the Table service within a URL. Certain characters must be percent-encoded to appear in a URL, using UTF-8 (preferred) or MBCS. This encoding occurs automatically when you use the Azure .NET Libraries or construct a <xref:System.Uri?qualifyHint=False> object that includes a property name. However, there are certain characters that are not valid in URL paths even when encoded. These characters cannot appear in property names.  Code points like \uE000, while valid in NTFS filenames, are not valid Unicode characters, so they cannot be used.  In addition, some ASCII or Unicode characters, like control characters (0x00 to 0x1F, \u0081, etc.), are also not allowed. For rules governing Unicode strings in HTTP/1.1 see:  
>   
>  -   [RFC 2616, Section 2.2: Basic Rules](http://www.ietf.org/rfc/rfc2616.txt)  
> -   [RFC 3987](http://www.ietf.org/rfc/rfc3987.txt)  
  
> [!NOTE]
>  Beginning with version 2009-04-14, the Table service no longer supports including the dash (-) character in property names.  
  
### Property Limitations  
 An entity can have up to 255 properties, including 3 system properties described in the following section. Therefore, the user may include up to 252 custom properties, in addition to the 3 system properties. The combined size of all data in an entity's properties cannot exceed 1 MB.  
  
### System Properties  
 An entity always has the following system properties:  
  
-   `PartitionKey` property  
  
-   `RowKey` property  
  
-   `Timestamp` property  
  
 These system properties are automatically included for every entity in a table. The names of these properties are reserved and cannot be changed. The developer is responsible for inserting and updating the values of `PartitionKey` and `RowKey`. The server manages the value of `Timestamp`, which cannot be modified.  
  
#### Characters Disallowed in Key Fields  
 The following characters are not allowed in values for the `PartitionKey` and `RowKey` properties:  
  
-   The forward slash (/) character  
  
-   The backslash (\\) character  
  
-   The number sign (#) character  
  
-   The question mark (?) character  
  
-   Control characters from U+0000 to U+001F, including:  
  
    -   The horizontal tab (\t) character  
  
    -   The linefeed (\n) character  
  
    -   The carriage return (\r) character  
  
-   Control characters from U+007F to U+009F  
  
#### PartitionKey Property  
 Tables are partitioned to support load balancing across storage nodes. A table's entities are organized by partition. A partition is a consecutive range of entities possessing the same partition key value. The partition key is a unique identifier for the partition within a given table, specified by the `PartitionKey` property. The partition key forms the first part of an entity's primary key. The partition key may be a string value up to 1 KB in size.  
  
 You must include the `PartitionKey` property in every insert, update, and delete operation.  
  
#### RowKey Property  
 The second part of the primary key is the row key, specified by the `RowKey` property. The row key is a unique identifier for an entity within a given partition. Together the `PartitionKey` and `RowKey` uniquely identify every entity within a table.  
  
 The row key is a string value that may be up to 1 KB in size.  
  
 You must include the `RowKey` property in every insert, update, and delete operation.  
  
#### Timestamp Property  
 The `Timestamp` property is a `DateTime` value that is maintained on the server side to record the time an entity was last modified. The Table service uses the `Timestamp` property internally to provide optimistic concurrency. The value of `Timestamp` is a monotonically increasing value, meaning that each time the entity is modified, the value of `Timestamp` increases for that entity. This property should not be set on insert or update operations (the value will be ignored).  
  
### Property Types  
 The Table service supports a subset of data types defined by the [OData Protocol Specification](http://www.odata.org/). The following table shows the supported property types for the Table service:  
  
|OData Data Type|Common Language Runtime type|Details|  
|---------------------|----------------------------------|-------------|  
|`Edm.Binary`|`byte[]`|An array of bytes up to 64 KB in size.|  
|`Edm.Boolean`|`bool`|A Boolean value.|  
|`Edm.DateTime`|`DateTime`|A 64-bit value expressed as Coordinated Universal Time (UTC). The supported `DateTime` range begins from 12:00 midnight, January 1, 1601 A.D. (C.E.), UTC. The range ends at December 31, 9999.|  
|`Edm.Double`|`double`|A 64-bit floating point value.|  
|`Edm.Guid`|`Guid`|A 128-bit globally unique identifier.|  
|`Edm.Int32`|`Int32` or `int`|A 32-bit integer.|  
|`Edm.Int64`|`Int64` or `long`|A 64-bit integer.|  
|`Edm.String`|`String`|A UTF-16-encoded value. String values may be up to 64 KB in size.|  
  
 By default a property is created as type `String`, unless you specify a different type. To explicitly type a property, specify its data type by using the appropriate OData data type for an [Insert Entity](../StorageServicesREST/Insert-Entity.md) or [Update Entity](../StorageServicesREST/Update-Entity2.md) operation. For more information, see [Inserting and Updating Entities](../StorageServicesREST/Inserting-and-Updating-Entities.md).  
  
 For examples that show how to filter on the various property types in a query request URI, see [Querying Tables and Entities](../StorageServicesREST/Querying-Tables-and-Entities.md).  
  
## See Also  
 [Get Started with Table Storage](http://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)   
 [Table Service Concepts](../StorageServicesREST/Table-Service-Concepts.md)
---
title: "Payload Format for Table Service Operations"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 9f1dce4a-d528-40ec-a5a4-fd93f9ee4c5e
caps.latest.revision: 18
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
# Payload Format for Table Service Operations
The Table service REST API supports ATOM and JSON as OData payload formats.  While the ATOM protocol is supported for all versions of the Azure storage services,  the JSON protocol is supported only for version 2013-08-15 and newer.  
  
-   JSON is the recommended payload format. JSON is supported for version 2013-08-15 and newer. You must use JSON with version 2015-12-11 and later.  
  
-   ATOM is supported for versions earlier than 2015-12-11.  
  
> [!NOTE]
>  The following REST API operations are not OData APIs and do not currently do not support JSON: [Get Table ACL](../StorageServicesREST/Get-Table-ACL.md), [Set Table ACL](../StorageServicesREST/Set-Table-ACL.md), [Get Table Service Properties](../StorageServicesREST/Get-Table-Service-Properties.md), and [Set Table Service Properties](../StorageServicesREST/Set-Table-Service-Properties.md).  
  
 To specify the JSON or ATOM format, specify the appropriate values for the `Content-Type` and `Accept` headers (described below). Note the following constraints:  
  
-   The `Content-Type` header is required for all requests containing an OData payload.  
  
-   If the `Accept` header is not provided, then the content type of the response defaults to `application/atom+xml`.  
  
-   Specifying the `$format` URI parameter overrides the value specified in the `Accept` request header, when the OData data service version is set to 3.0. See [Setting the OData Data Service Version Headers](../StorageServicesREST/Setting-the-OData-Data-Service-Version-Headers.md) for details about the OData service version.  
  
 To specify the payload format, set the `Content-Type` and `Accept` request headers according to the table below:  
  
|Payload Format|Content-Type Header|Accept Header|Data Service Version (REST API Version)|Supported APIs|  
|--------------------|--------------------------|-------------------|-----------------------------------------------|--------------------|  
|`Atom`|`application/atom+xml`|`application/atom+xml`|1.0 (Any version)<br /><br /> 2.0 (2011-08-18 or later)<br /><br /> 3.0 (2013-08-15 or later)|QueryTables<br /><br /> CreateTable<br /><br /> Delete Table<br /><br /> Query Entities<br /><br /> Insert Entities<br /><br /> Insert Or Merge Entity<br /><br /> Insert Or Replace Entity<br /><br /> Update Entity<br /><br /> Merge Entity<br /><br /> Delete Entity|  
|`JSON`|`application/json`|`application/json;odata=nometadata`<br /><br /> `application/json;odata=minimalmetadata`<br /><br /> `application/json;odata=fullmetadata`<br /><br /> For details, see the **JSON Format** section below.|3.0 (2013-08-15 or later)|QueryTables<br /><br /> CreateTable<br /><br /> Delete Table<br /><br /> Query Entities<br /><br /> Insert Entities<br /><br /> Insert Or Merge Entity<br /><br /> Insert Or Replace Entity<br /><br /> Update Entity<br /><br /> Merge Entity<br /><br /> Delete Entity|  
|`XML`|`application/xml`|`application/xml`|N/A|Get Table ACL<br /><br /> Set Table ACL<br /><br /> Get Table Service Properties<br /><br /> Set Table Service Properties|  
  
## JSON Format (application/json) (Versions 2013-08-15 and later)  
 OData extends the JSON format by defining general conventions for these name-value pairs, similar to the ATOM format described above. OData defines a set of canonical annotations for control information such as IDs, type, and links. For details about the JSON format, see [Introducing JSON](http://www.json.org/).  
  
 The key advantage of using OData's JSON format is that the predictable parts of the payload can be omitted to reduce the payload size. To reconstitute this data on the receiving end, expressions are used to compute missing links, type information, and control data. To control what is omitted from the payload, there are three levels that you can specify as part of the `Accept` header:  
  
-   `application/json;odata=nometadata`  
  
-   `application/json;odata=minimalmetadata`  
  
-   `application/json;odata=fullmetadata`  
  
 The following ODATA annotations are supported by the Azure Table service:  
  
-   `odata.metadata`: The metadata URL for a collection, entity, primitive value, or service document.  
  
-   `odata.id`: The entity id which is generally the URL to the resource.  
  
-   `odata.editlink`: The link used to edit/update the entry, if the entity is updatable and the odata.id does not represent a URL that can be used to edit the entity.  
  
-   `odata.type`: The type name of the containing object.  
  
-   `odata.etag`: The ETag of the entity.  
  
-   `PropertyName@odata.type`, for custom properties: The type name of the targeted property.  
  
-   `PropertyName@odata.type`, for system properties (*i.e.*, the `PrimaryKey`, `RowKey`, and `Timestamp` properties): The type name of the targeted property.  
  
 The information included in each level is summarized in the following table:  
  
|||||  
|-|-|-|-|  
|`Annotations`|`odata=fullmetadata`|`odata=minimalmetadata`|`odata=nometadata`|  
|`odata.metadata`|Yes|Yes|No|  
|`odata.id`|Yes|No|No|  
|`odata.editlink`|Yes|No|No|  
|`odata.type`|Yes|No|No|  
|`odata.etag`|Yes|No|No|  
|`PropertyName@odata.type` for custom properties|Yes|Yes|No|  
|`PropertyName@odata.type` for system properties|Yes|No|No|  
  
### Property Types in a JSON Feed  
 The `odata.type` annotation is used in the OData JSON format to determine the type of an open property. This annotation is present when all of the conditions below are satisfied:  
  
-   The JSON control level is set to either `odata=minimalmetadata` or `odata=fullmetadata`, as discussed in the **JSON Format** section.  
  
-   The property is a custom property. Note that for Azure tables, only the `PartitionKey`, `RowKey`, and `Timestamp` properties are system properties, and their type information is declared in `$metadata`. The type annotation for these properties is present only when the control level is set to `odata=fullmetadata`. For more information see [Understanding the Table Service Data Model](../StorageServicesREST/Understanding-the-Table-Service-Data-Model.md).  
  
-   The type of the property cannot be determined through the type detection heuristics summarized in the table below.  
  
||||  
|-|-|-|  
|Edm type|odata.type annotation required|JSON Type|  
|`Edm.Binary`|Yes|String|  
|`Edm.Boolean`|No|Literals|  
|`Edm.DateTime`|Yes|String|  
|`Edm.Double`|No|Numeric (contains decimal point)|  
|`Edm.Guid`|Yes|String|  
|`Edm.Int32`|No|Numeric (Doesn't contain decimal point)|  
|`Edm.Int64`|Yes|String|  
|`Edm.String`|No|String|  
  
 The following JSON entity provides an example for each of the eight different property types:  
  
```  
{  
  "PartitionKey":"mypartitionkey",  
  "RowKey":"myrowkey",  
  "DateTimeProperty@odata.type":"Edm.DateTime",  
  "DateTimeProperty":"2013-08-02T17:37:43.9004348Z",  
  "BoolProperty":false,  
  "BinaryProperty@odata.type":"Edm.Binary",  
  "BinaryProperty":"AQIDBA==",  
  "DoubleProperty":1234.1234,  
  "GuidProperty@odata.type":"Edm.Guid",  
  "GuidProperty":"4185404a-5818-48c3-b9be-f217df0dba6f",  
  "Int32Property":1234,  
  "Int64Property@odata.type":"Edm.Int64",  
  "Int64Property":"123456789012",  
  "StringProperty":"test"  
}  
```  
  
 Since `PartitionKey` and `RowKey` are system properties, meaning that all table rows must define these properties, their type annotation does not appear in the entity. These properties are predefined as type `Edm.String`. However, the other properties arecustom properties and therefore contain type information corresponding to one of the supported primitive types in the table above.  
  
### Examples:  
 The following sample OData entry demonstrates the JSON format sent as a request to insert an entity into Azure Table storage (see [Insert Entity](../StorageServicesREST/Insert-Entity.md) for details on the insert operation):  
  
```  
{  
  "Address":"Mountain View",  
  "Age":23,  
  "AmountDue":200.23,  
  "CustomerCode@odata.type":"Edm.Guid",  
  "CustomerCode":"c9da6455-213d-42c9-9a79-3e9149a57833",  
  "CustomerSince@odata.type":"Edm.DateTime",  
  "CustomerSince":"2008-07-10T00:00:00",  
  "IsActive":true,  
  "NumOfOrders@odata.type":"Edm.Int64",  
  "NumOfOrders":"255",  
  "PartitionKey":"mypartitionkey",  
  "RowKey":"myrowkey1",  
}  
```  
  
 When a client queries a set of entities in Azure Table storage, the service responds with a JSON payload (see [Query Entities](../StorageServicesREST/Query-Entities.md) for details on the query operation). The feed can include one of the three levels of information: no metadata, minimal metadata, or full metadata. The following examples demonstrate each kind:  
  
 **No metadata:**  
  
```  
{  
  "value":[  
    {  
      "PartitionKey":"Customer03",  
      "RowKey":"Name",  
      "Timestamp":"2013-08-09T18:55:48.3402073Z",  
      "CustomerSince":"2008-10-01T15:25:05.2852025Z",  
    }  
}  
```  
  
 **Minimal metadata:**  
  
```  
{  
  "odata.metadata":"https://myaccount.table.core.windows.net/$metadata#Customers,  
  "value":[  
    {  
      "PartitionKey":"Customer03",  
      "RowKey":"Name",  
      "Timestamp":"2013-08-09T18:55:48.3402073Z",  
      "CustomerSince@odata.type":"Edm.DateTime",  
      "CustomerSince":"2008-10-01T15:25:05.2852025Z",  
    }  
}  
```  
  
 **Full metadata:**  
  
```  
{  
  "odata.metadata":"https://myaccount.table.core.windows.net/$metadata#Customers",  
  "value":[  
    {  
      "odata.type":"myaccount.Customers",  
      "odata.id":"https://myaccount.table.core.windows.net/Customers(PartitionKey='Customer03',RowKey='Name')",  
      "odata.etag":"W/\"0x5B168C7B6E589D2\"",  
      "odata.editLink":"Customers(PartitionKey='Customer03',RowKey='Name')",  
      "PartitionKey":"Customer03,  
      "RowKey":"Name",  
      "Timestamp@odata.type":"Edm.DateTime",  
      "Timestamp":"2013-08-09T18:55:48.3402073Z",  
      "CustomerSince@odata.type":"Edm.DateTime",  
      "CustomerSince":"2008-10-01T15:25:05.2852025Z",  
    }  
}  
```  
  
 To learn more about OData JSON format see the [OData JSON Format Version 4.0](http://go.microsoft.com/fwlink/?LinkId=301473) specification, in conjunction with the [\[MS-ODATAJSON\]: OData Protocol JSON Format Standards Support Document](http://msdn.microsoft.com/library/dn260768.aspx).  
  
## Atom Format (application/atom+xml)  (Versions earlier than 2015-12-11 only)  
 [Atom](http://tools.ietf.org/html/rfc4287) is an XML-based document format that describes collections of related information referred to as *feeds*. Feeds are composed of a number of items, known as *entries*. [AtomPub](http://tools.ietf.org/html/rfc5023) defines additional format constructs for entries and feeds so that the resources they represent may be easily categorized, grouped, edited, and discovered. However, since Atom does not define how structured data is encoded with feeds, [OData](http://www.odata.org/) defines a set of conventions for representing structured data in an Atom feed in order to enable transfers of structured content by services based on OData.  
  
 For example, the following sample OData entry demonstrates the Atom format sent through a request to insert an entity into Azure Table storage using the REST API (see [Insert Entity](../StorageServicesREST/Insert-Entity.md) for details on the insert operation):  
  
```  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<entry xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">  
  <title />  
  <author>  
    <name />  
  </author>  
  <id />  
  <content type="application/xml">  
    <m:properties>  
      <d:Address>Mountain View</d:Address>  
      <d:Age m:type="Edm.Int32">23</d:Age>  
      <d:AmountDue m:type="Edm.Double">200.23</d:AmountDue>  
      <d:BinaryData m:type="Edm.Binary" m:null="true" />  
      <d:CustomerCode m:type="Edm.Guid">c9da6455-213d-42c9-9a79-3e9149a57833</d:CustomerCode>  
      <d:CustomerSince m:type="Edm.DateTime">2008-07-10T00:00:00</d:CustomerSince>  
      <d:IsActive m:type="Edm.Boolean">true</d:IsActive>  
      <d:NumOfOrders m:type="Edm.Int64">255</d:NumOfOrders>  
      <d:PartitionKey>mypartitionkey</d:PartitionKey>  
      <d:RowKey>myrowkey1</d:RowKey>  
    </m:properties>  
  </content>  
</entry>  
```  
  
 When a client queries a set of entities in Table storage, the service responds with an Atom feed, which is a collection of Atom entries (see [Query Entities](../StorageServicesREST/Query-Entities.md) for details on the query operation):  
  
```  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<feed xml:base="https://myaccount.table.core.windows.net/" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">  
  <title type="text">Customers</title>  
  <id>https://myaccount.table.core.windows.net/Customers</id>  
  <link rel="self" title="Customers" href="Customers" />  
  <entry m:etag="W/"0x5B168C7B6E589D2"">  
  <id>https://myaccount.table.core.windows.net/Customers(PartitionKey='Customer03',RowKey='Name')</id>  
    <title type="text"></title>  
    <updated>2008-10-01T15:26:13Z</updated>  
    <author>  
      <name />  
    </author>  
    <link rel="edit" title="Customers" href="Customers (PartitionKey='Customer03',RowKey='Name')" />  
    <category term="myaccount.Customers" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />  
    <content type="application/xml">  
      <m:properties>  
        <d:PartitionKey>Customer03</d:PartitionKey>  
        <d:RowKey>Name</d:RowKey>        <d:CustomerSince m:type="Edm.DateTime">2008-10-01T15:25:05.2852025Z</d:CustomerSince>  
      </m:properties>  
    </content>  
  </entry>  
</feed>  
```  
  
### Property Types in an Atom Feed  
 Property data types are defined by the [OData Protocol Specification](http://www.odata.org/). Not all data types defined by the specification are supported by the Table service. For information about the supported data types and how they map to common language runtime (CLR) types, see [Understanding the Table Service Data Model](../StorageServicesREST/Understanding-the-Table-Service-Data-Model.md).  
  
 A property may be specified with or without an explicit data type. If the type is omitted, the property is automatically created as data type `Edm.String`.  
  
 If a property is created with an explicit type, a query that returns the entity includes that type within the Atom feed, so that you can determine the type of an existing property if necessary. Knowing a property's type is important when you are constructing a query that filters on that property. For more information, see [Querying Tables and Entities](../StorageServicesREST/Querying-Tables-and-Entities.md).  
  
## See Also  
 [Setting the OData Data Service Version Headers](../StorageServicesREST/Setting-the-OData-Data-Service-Version-Headers.md)   
 [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md)   
 [Table Service Concepts](../StorageServicesREST/Table-Service-Concepts.md)
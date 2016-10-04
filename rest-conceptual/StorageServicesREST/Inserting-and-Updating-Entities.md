---
title: "Inserting and Updating Entities"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 8f029e46-f7c1-476a-b349-0649551aa127
caps.latest.revision: 19
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
# Inserting and Updating Entities
To insert or update an entity, you include with the request an an OData ATOM or OData JSON entity that specifies the properties and data for the entity. For more information regarding the format of the payload see [Payload Format for Table Service Operations](../StorageServicesREST/Payload-Format-for-Table-Service-Operations.md).  
  
 The [Insert Entity](../StorageServicesREST/Insert-Entity.md) operation inserts a new entity with a unique primary key, formed from the combination of the PartitionKey and the RowKey. The [Update Entity](../StorageServicesREST/Update-Entity2.md) operation replaces an existing entity with the same `PartitionKey` and `RowKey`. The [Merge Entity](../StorageServicesREST/Merge-Entity.md) operation updates the properties of an existing entity, but does not replace the entity. The [Insert Or Merge Entity](../StorageServicesREST/Insert-Or-Merge-Entity.md) operation creates a new entity with a unique primary key or updates the properties of an existing entity, but does not replace the entity. The [Insert Or Replace Entity](../StorageServicesREST/Insert-Or-Replace-Entity.md) operation creates a new entity with a unique primary key or replaces an existing entity.  
  
## Constructing the Atom Feed  
 The Atom feed for an insert or update operation defines the entity's properties by specifying their names and data types, and sets the values for those properties.  
  
 The `content` element contains the entity's property definitions, which are specified within the `m:properties` element. The property's type is specified by the `m:type` attribute. For detailed information about property types, see [Payload Format for Table Service Operations](../StorageServicesREST/Payload-Format-for-Table-Service-Operations.md).  
  
 Here is an example of an Atom feed for an [Insert Entity](../StorageServicesREST/Insert-Entity.md) operation:  
  
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
  
> [!NOTE]
>  Atom payloads are supported only in versions prior to 2015-12-11. Beginning with version 2015-12-11, payloads must be in JSON.  
  
## Constructing the JSON Feed  
 To insert or update an entity using the OData JSON format, create a JSON object with property names as keys together with their property values. You may need to include the property type if it cannot be inferred through OData JSON type detection heuristics. See [Payload Format for Table Service Operations](../StorageServicesREST/Payload-Format-for-Table-Service-Operations.md) for information on property type detection heuristics and on using JSON OData.  
  
 The JSON payload corresponding to the ATOM example above is as follows:  
  
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
   "RowKey":"myrowkey"  
}  
  
```  
  
## See Also  
 [Table Service Concepts](../StorageServicesREST/Table-Service-Concepts.md)   
 [Operations on Entities](../StorageServicesREST/Operations-on-Entities.md)
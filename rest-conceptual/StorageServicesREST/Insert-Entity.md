---
title: "Insert Entity"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 9ca046aa-e9b4-4eaf-a7c0-d6ccdbaf48b9
caps.latest.revision: 56
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
# Insert Entity
The `Insert Entity` operation inserts a new entity into a table.  
  
## Request  
 The `Insert Entity` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account, and `mytable` with the name of your table:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`POST`|`https://myaccount.table.core.windows.net/mytable`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Table service port as `127.0.0.1:10002`, followed by the emulated storage account name:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`POST`|`http://127.0.0.1:10002/devstoreaccount1/mytable`|HTTP/1.1|  
  
 The Table service in the storage emulator differs from the Windows® Azure™ Table service in several ways. For more information, see [Differences Between the Storage Emulator and Azure Storage Services](assetId:///c60f2090-c0f4-4817-8559-e98786461dbe).  
  
### URI Parameters  
 None.  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Optional. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`Content-Type`|Required. Specifies the content type of the payload. Possible values are `application/atom+xml` (versions prior to 2015-12-11 only) and `application/json`.<br /><br /> For more formation about valid content types, see [Payload Format for Table Service Operations](../StorageServicesREST/Payload-Format-for-Table-Service-Operations.md).|  
|`Content-Length`|Required. The length of the request body.|  
|`Accept`|Optional. Specifies the accepted content-type of the response payload. Possible values are:<br /><br /> -   `application/atom+xml` (versions prior to 2015-12-11 only)<br />-   `application/json;odata=nometadata`<br />-   `application/json;odata=minimalmetadata`<br />-   `application/json;odata=fullmetadata`<br /><br /> For more information, see [Payload Format for Table Service Operations](../StorageServicesREST/Payload-Format-for-Table-Service-Operations.md).|  
|`Prefer`|Optional. Specifies whether the response should include the inserted entity in the payload. Possible values are `return-no-content` and `return-content`. For more information, see [Setting the Prefer Header to Manage Response Echo on Insert Operations](../StorageServicesREST/Setting-the-Prefer-Header-to-Manage-Response-Echo-on-Insert-Operations.md).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
### Request Body  
 The `Insert Entity` operation sends the entity to be inserted as an OData entity, which is either a JSON or an Atom feed. For more information, see [Inserting and Updating Entities](../StorageServicesREST/Inserting-and-Updating-Entities.md).  
  
> [!NOTE]
>  JSON is the recommended payload format, and is the only format supported for versions 2015-12-11 and later.  
  
#### JSON (versions 2013-08-15 and later)  
 Here is a sample JSON request body for `Insert Entity` operation:  
  
```  
{  
   "Address":"Mountain View",  
   "Age":23,  
   "AmountDue":200.23,  
   "CustomerCode@odata.type":"Edm.Guid",  
   "CustomerCode":"c9da6455-213d-42c9-9a79-3e9149a57833",  
   "CustomerSince@odata.type":"Edm.DateTime",  
   "CustomerSince":"2008-07-10T00:00:00",  
   "IsActive":true,  
   "NumberOfOrders@odata.type":"Edm.Int64",  
   "NumberOfOrders":"255",  
   "PartitionKey":"mypartitionkey",  
   "RowKey":"myrowkey"  
}  
```  
  
#### Atom Feed (versions prior to 2015-12-11)  
 Here is a sample Atom request body for the `Insert Entity` operation.  
  
```  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<entry xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">  
  <title />  
  <updated>2013-09-18T23:46:19.3857256Z</updated>  
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
  
## Response  
 The response includes an HTTP status code, a set of response headers, and a response body.  
  
### Status Code  
 The status code depends on the value of the `Prefer` header. If the `Prefer` header is set to `return-no-content`, then a successful operation returns status code 204 (`No Content`). If the `Prefer` header is not specified or if it is set to `return-content`, then a successful operation returns status code 201 (`Created`). For more information, see [Setting the Prefer Header to Manage Response Echo on Insert Operations](../StorageServicesREST/Setting-the-Prefer-Header-to-Manage-Response-Echo-on-Insert-Operations.md).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md) and [Table Service Error Codes](../StorageServicesREST/Table-Service-Error-Codes.md).  
  
### Response Headers  
 The response includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Table service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
|`ETag`|The ETag for the entity.|  
|`Preference-Applied`|Indicates whether the `Prefer` request header was honored. If the response does not include this header, then the `Prefer` header was not honored. If this header is returned, its value will either be `return-content` or `return-no-content`.<br /><br /> For more information, see [Setting the Prefer Header to Manage Response Echo on Insert Operations](../StorageServicesREST/Setting-the-Prefer-Header-to-Manage-Response-Echo-on-Insert-Operations.md).|  
|`Content-Type`|Indicates the content type of the payload. The value depends on the value specified for the `Accept` request header. Possible values are:<br /><br /> -   `application/atom+xml`<br />-   `application/json;odata=nometadata`<br />-   `application/json;odata=minimalmetadata`<br />-   `application/json;odata=fullmetadata`<br /><br /> For more information about content types, see [Payload Format for Table Service Operations](../StorageServicesREST/Payload-Format-for-Table-Service-Operations.md).|  
  
### Response Body  
 If the request includes the `Prefer` header with the value `return-no-content`, no response body is returned. Otherwise, the response body is an OData entity set.  
  
> [!NOTE]
>  JSON is the recommended payload format, and is the only format supported for versions 2015-12-11 and later.  
  
#### JSON (versions 2013-08-15 and later)  
 Here is a sample JSON response for each metadata level:  
  
 **No metadata:**  
  
```  
{  
   "PartitionKey":"mypartitionkey",  
   "RowKey":"myrowkey",  
   "Timestamp":"2013-08-22T01:12:06.2608595Z",  
   "Address":"Mountain View",  
   "Age":23,  
   "AmountDue":200.23,  
   "CustomerCode":"c9da6455-213d-42c9-9a79-3e9149a57833",  
   "CustomerSince":"2008-07-10T00:00:00",  
   "IsActive":true,  
   "NumberOfOrders":"255"  
}  
  
```  
  
 **Minimal metadata:**  
  
```  
{  
   "odata.metadata":"https://myaccount.table.core.windows.net/Customer/$metadata#Customers/@Element",  
   "PartitionKey":"mypartitionkey",  
   "RowKey":"myrowkey",  
   "Timestamp":"2013-08-22T01:12:06.2608595Z",  
   "Address":"Mountain View",  
   "Age":23,  
   "AmountDue":200.23,  
   "CustomerCode@odata.type":"Edm.Guid",  
   "CustomerCode":"c9da6455-213d-42c9-9a79-3e9149a57833",  
   "CustomerSince@odata.type":"Edm.DateTime",  
   "CustomerSince":"2008-07-10T00:00:00",  
   "IsActive":true,  
   "NumberOfOrders@odata.type":"Edm.Int64",  
   "NumberOfOrders":"255"  
}  
  
```  
  
 **Full metadata:**  
  
```  
{  
   "odata.metadata":"https://myaccount.table.core.windows.net/Customer/$metadata#Customers/@Element",  
   "odata.type":"myaccount.Customers",  
   "odata.id":" https://myaccount.table.core.windows.net/Customers(PartitionKey='mypartitionkey',RowKey='myrowkey')",  
   "odata.etag":"W/\"0x5B168C7B6E589D2\"",  
   "odata.editLink":"Customers(PartitionKey='mypartitionkey',RowKey='myrowkey')",  
   "PartitionKey":"mypartitionkey",  
   "RowKey":"myrowkey",  
   "Timestamp@odata.type":"Edm.DateTime",  
   "Timestamp":"2013-08-22T01:12:06.2608595Z",  
   "Address":"Mountain View",  
   "Age":23,  
   "AmountDue":200.23,  
   "CustomerCode@odata.type":"Edm.Guid",  
   "CustomerCode":"c9da6455-213d-42c9-9a79-3e9149a57833",  
   "CustomerSince@odata.type":"Edm.DateTime",  
   "CustomerSince":"2008-07-10T00:00:00",  
   "IsActive":true,  
   "NumberOfOrders@odata.type":"Edm.Int64",  
   "NumberOfOrders":"255"  
}  
```  
  
#### Atom Feed (versions prior to 2015-12-11)  
 Here is a sample Atom response body for the `Insert Entity` operation.  
  
```  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<entry xml:base="https://myaccount.table.core.windows.net/" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" m:etag="W/"0x5B168C7B6E589D2"" xmlns="http://www.w3.org/2005/Atom">  
  <id>https://myaccount.table.core.windows.net/mytable(PartitionKey='mypartitionkey',RowKey='myrowkey1')</id>  
  <title type="text"></title>  
  <updated>2008-09-18T23:46:19.3857256Z</updated>  
  <author>  
    <name />  
  </author>  
  <link rel="edit" title="mytable" href="mytable(PartitionKey='mypartitionkey',RowKey='myrowkey1')" />  
  <category term="myaccount.Tables" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />  
  <content type="application/xml">  
    <m:properties>  
      <d:PartitionKey>mypartitionkey</d:PartitionKey>  
      <d:RowKey>myrowkey1</d:RowKey>  
      <d:Timestamp m:type="Edm.DateTime">2008-09-18T23:46:19.4277424Z</d:Timestamp>  
      <d:Address>Mountain View</d:Address>  
      <d:Age m:type="Edm.Int32">23</d:Age>  
      <d:AmountDue m:type="Edm.Double">200.23</d:AmountDue>  
      <d:CustomerCode m:type="Edm.Guid">c9da6455-213d-42c9-9a79-3e9149a57833</d:CustomerCode>  
      <d:CustomerSince m:type="Edm.DateTime">2008-07-10T00:00:00</d:CustomerSince>  
      <d:IsActive m:type="Edm.Boolean">true</d:IsActive>  
      <d:NumOfOrders m:type="Edm.Int64">255</d:NumOfOrders>  
    </m:properties>  
  </content>  
</entry>  
```  
  
## Authorization  
 This operation can be performed by the account owner and by anyone with a shared access signature that has permission to perform this operation.  
  
## Remarks  
 When inserting an entity into a table, you must specify values for the `PartitionKey` and `RowKey` system properties. Together, these properties form the primary key and must be unique within the table.  
  
 Both the `PartitionKey` and `RowKey` values must be string values; each key value may be up to 64 KB in size. If you are using an integer value for the key value, you should convert the integer to a fixed-width string, because they are canonically sorted. For example, you should convert the value `1` to `0000001` to ensure proper sorting.  
  
 To explicitly type a property, specify the appropriate OData data type by setting the `m:type` attribute within the property definition in the Atom feed. For more information about typing properties, see [Inserting and Updating Entities](../StorageServicesREST/Inserting-and-Updating-Entities.md).  
  
 For information about performing batch insert operations, see [Performing Entity Group Transactions](../StorageServicesREST/Performing-Entity-Group-Transactions.md).  
  
## See Also  
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Setting the OData Data Service Version Headers](../StorageServicesREST/Setting-the-OData-Data-Service-Version-Headers.md)   
 [Inserting and Updating Entities](../StorageServicesREST/Inserting-and-Updating-Entities.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Table Service Error Codes](../StorageServicesREST/Table-Service-Error-Codes.md)
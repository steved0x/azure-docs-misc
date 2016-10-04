---
title: "Insert Or Merge Entity"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 2de2c193-befe-4b7f-864a-650f3d861939
caps.latest.revision: 26
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
# Insert Or Merge Entity
The `Insert Or Merge Entity` operation updates an existing entity or inserts a new entity if it does not exist in the table. Because this operation can insert or update an entity, it is also known as an *upsert* operation.  
  
## Request  
 The `Insert Or Merge Entity` request may be constructed as follows. HTTPS is recommended. Replace the following values with your own:  
  
-   `myaccount` with the name of your storage account  
  
-   `mytable` with the name of your table  
  
-   `myPartitionKey` and `myRowKey` with the name of the partition key and row key for entity to be updated  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`MERGE`|`https://myaccount.table.core.windows.net/mytable(PartitionKey='myPartitionKey', RowKey='myRowKey')`|HTTP/1.1|  
  
### Emulated Storage Service  
 When making a request against the emulated storage service, specify the emulator hostname and Table service port as 127.0.0.1:10002, followed by the emulated storage account name.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`MERGE`|`http://127.0.0.1:10002/devstoreaccount1/mytable(PartitionKey='myPartitionKey', RowKey='myRowKey')`|HTTP/1.1|  
  
 The Table service in the storage emulator differs from the Windows® Azure™ Table service in several ways. For more information, see [Differences Between the Storage Emulator and Azure Storage Services](assetId:///c60f2090-c0f4-4817-8559-e98786461dbe).  
  
### URI Parameters  
 None.  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Required. Must be set to 2011-08-18 or newer. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`Content-Type`|Required. Specifies the content type of the payload. Possible values are `application/atom+xml` and `application/json`.<br /><br /> For more formation about valid content types, see [Payload Format for Table Service Operations](../StorageServicesREST/Payload-Format-for-Table-Service-Operations.md).|  
|`Content-Length`|Required. The length of the request body.|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
### Request Body  
 The `Insert Or Merge Entity` operation sends the entity to be inserted as an OData entity set, which may be either an Atom or JSON payload. For more information, see [Inserting and Updating Entities](../StorageServicesREST/Inserting-and-Updating-Entities.md).  
  
> [!NOTE]
>  JSON is the recommended payload format, and is the only format supported for versions 2015-12-11 and later.  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 204 (`No Content`).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md) and [Table Service Error Codes](../StorageServicesREST/Table-Service-Error-Codes.md).  
  
### Response Headers  
 The response includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`ETag`|The ETag for the entity.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Table service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
### Response Body  
 None.  
  
## Authorization  
 This operation can be performed by the account owner and by anyone with a shared access signature that has permission to perform this operation.  
  
## Sample Request and Response  
 The examples below show sample requests using both JSON and Atom feeds.  
  
> [!NOTE]
>  JSON is the recommended payload format, and is the only format supported for versions 2015-12-11 and later.  
  
### JSON (versions 2013-08-15 and later)  
 The following is a sample request and response using JSON.  
  
```  
MERGE https://myaccount.table.core.windows.net/mytable(PartitionKey='myPartitionKey',RowKey='myRowKey')  
```  
  
 The request is sent with the following headers:  
  
```  
x-ms-version: 2013-08-15  
Content-Type: application/json  
x-ms-date: Tue, 30 Aug 2013 18:10:24 GMT  
Authorization: SharedKeyLite myaccount:u0sWZKmjBD1B7LY/CwXWCnHdqK4B1P4z8hKy9SVW49o=  
Content-Length: 1135  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
```  
  
 The request is sent with the following JSON body:  
  
```  
{  
   "Address":"Santa Clara",  
   "Age":23,  
   "AmountDue":200.23,  
   "CustomerCode@odata.type":"Edm.Guid",  
   "CustomerCode":"c9da6455-213d-42c9-9a79-3e9149a57833",  
   "CustomerSince@odata.type":"Edm.DateTime",  
   "CustomerSince":"2008-07-10T00:00:00",  
   "IsActive":false,  
   "NumberOfOrders@odata.type":"Edm.Int64",  
   "NumberOfOrders":"255",  
   "PartitionKey":"mypartitionkey",  
   "RowKey":"myrowkey"  
}  
```  
  
 After the request has been sent, the following response is returned:  
  
```  
  
HTTP/1.1 204 No Content  
  
Connection: Keep-Alive  
x-ms-request-id: 2c085f8f-11a4-4e1d-bd49-82c6bd87649d  
Content-Length: 0  
Cache-Control: no-cache  
Date: Tue, 30 Aug 2013 18:12:54 GMT  
ETag: W/"0x5B168C7B6E589D2"  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Server: Windows-Azure-Table/1.0 Microsoft-HTTPAPI/2.0  
```  
  
### Atom Feed (versions prior to 2015-12-11)  
 The following is a sample request and response using Atom:  
  
```  
MERGE https://myaccount.table.core.windows.net/mytable(PartitionKey='myPartitionKey',RowKey='myRowKey')  
```  
  
 The request is sent with the following headers:  
  
```  
x-ms-version: 2013-08-15  
Accept: application/atom+xml,application/xml  
Accept-Charset: UTF-8  
Content-Type: application/atom+xml  
x-ms-date: Tue, 12 Nov 2013 18:10:24 GMT  
Authorization: SharedKeyLite myaccount:u0sWZKmjBD1B7LY/CwXWCnHdqK4B1P4z8hKy9SVW49o=  
Content-Length: 1135  
DataServiceVersion: 1.0;NetFx  
MaxDataServiceVersion: 2.0;NetFx  
```  
  
 The request is sent with the following XML body:  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<entry xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">  
  <title />  
  <updated>2013-11-12T18:09:37.168836Z</updated>  
  <author>  
    <name />  
  </author>  
<id>https://myaccount.table.core.windows.net/mytable(PartitionKey='mypartitionkey',RowKey='myrowkey')</id>  
  <content type="application/xml">  
    <m:properties>  
      <d:Address>Santa Clara</d:Address>  
      <d:Age m:type="Edm.Int32">23</d:Age>  
      <d:AmountDue m:type="Edm.Double">200.23</d:AmountDue>  
      <d:CustomerCode m:type="Edm.Guid">c9da6455-213d-42c9-9a79-3e9149a57833</d:CustomerCode>  
      <d:CustomerSince m:type="Edm.DateTime">2008-07-10T00:00:00Z</d:CustomerSince>  
      <d:IsActive m:type="Edm.Boolean">false</d:IsActive>  
      <d:NumOfOrders m:type="Edm.Int64">255</d:NumOfOrders>  
      <d:PartitionKey>mypartitionkey</d:PartitionKey>  
      <d:RowKey>myrowkey1</d:RowKey>  
    </m:properties>  
  </content>  
</entry>  
```  
  
 After the request has been sent, the following response is returned:  
  
```  
HTTP/1.1 204 No Content  
  
Connection: Keep-Alive  
x-ms-request-id: 2c085f8f-11a4-4e1d-bd49-82c6bd87649d  
Content-Length: 0  
Cache-Control: no-cache  
Date: Tue, 12 Nov 2013 18:12:54 GMT  
ETag: W/"0x5B168C7B6E589D2"  
DataServiceVersion: 1.0;NetFx  
MaxDataServiceVersion: 2.0;NetFx  
Server: Windows-Azure-Table/1.0 Microsoft-HTTPAPI/2.0  
```  
  
## Remarks  
 The `Insert Or Merge Entity` operation uses the MERGE verb and must be called using the 2011-08-18 version or newer. In addition, it does not use the If-Match header. These attributes distinguish this operation from the `Update Entity` operation, though the request body is the same for both operations.  
  
 If the `Insert Or Merge Entity` operation is used to merge an entity, any properties from the previous entity will be retained if the request does not define or include them. Properties with a null value will also be retained.  
  
 When calling the `Insert or Merge Entity` operation, you must specify values for the `PartitionKey` and `RowKey` system properties. Together, these properties form the primary key and must be unique within the table.  
  
 Both the `PartitionKey` and `RowKey` values must be string values; each key value may be up to 64 KB in size. If you are using an integer value for the key value, you should convert the integer to a fixed-width string, because they are canonically sorted. For example, you should convert the value `1` to `0000001` to ensure proper sorting.  
  
 To explicitly type a property, specify the appropriate OData type by setting the `m:type` attribute within the property definition in the Atom feed. For more information about typing properties, see [Inserting and Updating Entities](../StorageServicesREST/Inserting-and-Updating-Entities.md).  
  
 Any application that can authenticate and send an HTTP MERGE request can insert or update an entity.  
  
 For information about performing batch upsert operations, see [Performing Entity Group Transactions](../StorageServicesREST/Performing-Entity-Group-Transactions.md).  
  
## See Also  
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Setting the OData Data Service Version Headers](../StorageServicesREST/Setting-the-OData-Data-Service-Version-Headers.md)   
 [Inserting and Updating Entities](../StorageServicesREST/Inserting-and-Updating-Entities.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Table Service Error Codes](../StorageServicesREST/Table-Service-Error-Codes.md)
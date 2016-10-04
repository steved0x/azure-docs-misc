---
title: "Create Table"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: e7b7c22f-39d1-46b1-9f3a-0ccaeabde95a
caps.latest.revision: 50
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
# Create Table
The `Create Table` operation creates a new table in the storage account.  
  
## Request  
 The `Create Table` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`POST`|`https://myaccount.table.core.windows.net/Tables`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Table service port as `127.0.0.1:10002`, followed by the emulated storage account name:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`POST`|`http://127.0.0.1:10002/devstoreaccount1/Tables`|HTTP/1.1|  
  
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
|`Content-Type`|Required. Specifies the content type of the payload. Possible values are:<br /><br /> -   `application/atom+xml` (versions prior to 2015-12-11 only)<br />-   `application/json`<br /><br /> For more information, see [Payload Format for Table Service Operations](../StorageServicesREST/Payload-Format-for-Table-Service-Operations.md).|  
|`Accept`|Optional. Specifies the accepted content-type of the response payload. Possible values are:<br /><br /> -   `application/atom+xml` (versions prior to 2015-12-11 only)<br />-   `application/json;odata=nometadata`<br />-   `application/json;odata=minimalmetadata`<br />-   `application/json;odata=fullmetadata`<br /><br /> For more information, see [Payload Format for Table Service Operations](../StorageServicesREST/Payload-Format-for-Table-Service-Operations.md).|  
|`Prefer`|Optional. Specifies whether the response should include the inserted entity in the payload. Possible values are `return-no-content` and `return-content`.<br /><br /> For more information about this header, see [Setting the Prefer Header to Manage Response Echo on Insert Operations](../StorageServicesREST/Setting-the-Prefer-Header-to-Manage-Response-Echo-on-Insert-Operations.md).|  
|`Content-Length`|Required. The length of the request body.|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
### Request Body  
 The request body specifies the name of the table to be created. Note that table names must conform to the naming restrictions described in [Understanding the Table Service Data Model](../StorageServicesREST/Understanding-the-Table-Service-Data-Model.md).  
  
 The request body is an OData entity set, which can be expressed as JSON or as an Atom feed.  
  
> [!NOTE]
>  JSON is the recommended payload format, and is the only format supported for versions 2015-12-11 and later.  
  
 For guidance on valid table names, see the **Table Names** section in [Understanding the Table Service Data Model](../StorageServicesREST/Understanding-the-Table-Service-Data-Model.md).  
  
#### JSON (versions 2013-08-15 and later)  
 The request body as a JSON feed has the following general format.  
  
```  
{   
    "TableName":"mytable"  
}  
```  
  
#### Atom Feed (versions prior to 2015-12-11)  
 The request body as an Atom feed has the following general format.  
  
```  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>     
  <entry xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices"   
    xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"  
    xmlns="http://www.w3.org/2005/Atom">   
    <title />   
    <updated>2009-03-18T11:48:34.9840639-07:00</updated>   
    <author>  
      <name/>   
    </author>   
      <id/>   
      <content type="application/xml">  
        <m:properties>  
          <d:TableName>mytable</d:TableName>  
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
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Table service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
|`Preference-Applied`|Indicates whether the `Prefer` request header was honored. If the response does not include this header, then the `Prefer` header was not honored. If this header is returned, its value will either be `return-content` or `return-no-content`.<br /><br /> For more information, see [Setting the Prefer Header to Manage Response Echo on Insert Operations](../StorageServicesREST/Setting-the-Prefer-Header-to-Manage-Response-Echo-on-Insert-Operations.md).|  
|`Content-Type`|Indicates the content type of the payload. The value depends on the value specified for the `Accept` request header. Possible values are:<br /><br /> -   `application/atom+xml`<br />-   `application/json;odata=nometadata`<br />-   `application/json;odata=minimalmetadata`<br />-   `application/json;odata=fullmetadata`<br /><br /> For more information about content types, see [Payload Format for Table Service Operations](../StorageServicesREST/Payload-Format-for-Table-Service-Operations.md).|  
  
### Response Body  
 If the request includes the `Prefer` header with the value `return-no-content`, no response body is returned. Otherwise, the response body is an OData entity set.  
  
> [!NOTE]
>  JSON is the recommended payload format, and is the only format supported for versions 2015-12-11 and later.  
  
#### JSON (versions 2013-08-15 and later)  
 Here are the response payloads in JSON for different control levels.  
  
 **Full Metadata**  
  
```  
{  
  
    "odata.metadata":"https://myaccount.table.core.windows.net/$metadata#Tables/@Element",  
  
    "odata.type":" myaccount.Tables",  
  
    "odata.id":"https://myaccount.table.core.windows.net/Tables('mytable')",  
  
    "odata.editLink":"Tables('mytable')",  
  
    "TableName":"mytable"  
  
}  
```  
  
 **Minimal Metadata**  
  
```  
{  
  
    "odata.metadata":"https://myaccount.table.core.windows.net/$metadata#Tables/@Element",  
  
    "TableName":"mytable"  
  
}  
  
```  
  
 **No Metadata**  
  
```  
{  
  
    "TableName":"mytable"  
  
}  
  
```  
  
#### Atom Feed (versions prior to 2015-12-11)  
 Here is a sample Atom response for the `Create Table` operation.  
  
```  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<entry xml:base="https://myaccount.table.core.windows.net/" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom"> <id>https://myaccount.table.core.windows.net/Tables('mytable')</id>  
  <title type="text"></title>  
  <updated>2013-10-24T17:18:54.7062347Z</updated>  
  <author>  
    <name />  
  </author>  
  <link rel="edit" title="Tables" href="Tables('mytable')" />  
  <category term="myaccount.Tables" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />  
  <content type="application/xml">  
    <m:properties>  
      <d:TableName>mytable</d:TableName>  
    </m:properties>  
  </content>  
</entry>  
```  
  
## Authorization  
 Only the account owner may call this operation.  
  
## Remarks  
 None.  
  
## See Also  
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Setting the OData Data Service Version Headers](../StorageServicesREST/Setting-the-OData-Data-Service-Version-Headers.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Table Service Error Codes](../StorageServicesREST/Table-Service-Error-Codes.md)
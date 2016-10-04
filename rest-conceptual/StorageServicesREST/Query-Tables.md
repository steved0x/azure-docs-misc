---
title: "Query Tables"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 7010b048-a7cb-4c3a-b45e-99debe1c9f70
caps.latest.revision: 61
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
# Query Tables
The `Query Tables` operation returns a list of tables under the specified account.  
  
## Request  
 The `Query Tables` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`GET`|`https://myaccount.table.core.windows.net/Tables`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Table service port as `127.0.0.1:10002`, followed by the emulated storage account name:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`GET`|`http://127.0.0.1:10002/devstoreaccount1/Tables`|HTTP/1.1|  
  
 The Table service in the emulated storage service differs from the Windows® Azure™ Table service in several ways. For more information, see [Differences Between the Storage Emulator and Azure Storage Services](assetId:///c60f2090-c0f4-4817-8559-e98786461dbe).  
  
### URI Parameters  
 The `Query Tables` operation supports the query options defined by the OData Protocol Specification. For more information, see [OData Protocol](http://www.odata.org/).  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Optional. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`Accept`|Optional. Specifies the accepted content type of the response payload. Possible values are:<br /><br /> -   `application/atom+xml` (versions prior to 2015-12-11 only)<br />-   `application/json;odata=nometadata`<br />-   `application/json;odata=minimalmetadata`<br />-   `application/json;odata=fullmetadata`<br /><br /> For more information, see [Payload Format for Table Service Operations](../StorageServicesREST/Payload-Format-for-Table-Service-Operations.md).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Windows Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
### Request Body  
 None.  
  
## Response  
 The response includes an HTTP status code, a set of response headers, and a response body.  
  
### Status Code  
 A successful operation returns status code 200 (OK).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md) and [Table Service Error Codes](../StorageServicesREST/Table-Service-Error-Codes.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`x-ms-continuation-NextTableName`|If the number of tables to be returned exceeds 1,000 or the query does not complete within the timeout interval, the response header includes the `x-ms-continuation-NextTableName` continuation header. This header returns the continuation token value. For more information about using the continuation token, see [Query Timeout and Pagination](../StorageServicesREST/Query-Timeout-and-Pagination.md).|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Table service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
|`Content-Type`|Indicates the content type of the payload. Value depends on the request `Accept` header. Possible values are:<br /><br /> -   `application/atom+xml`<br />-   `application/json;odata=nometadata`<br />-   `application/json;odata=minimalmetadata`<br />-   `application/json;odata=fullmetadata`<br /><br /> For more formation about valid content types, see [Payload Format for Table Service Operations](../StorageServicesREST/Payload-Format-for-Table-Service-Operations.md).|  
  
### Response Body  
 The `Query Tables` operation returns the list of tables in the account as an OData entity set. According to the value of the `Accept` header, the content is either JSON or an Atom feed.  
  
> [!NOTE]
>  JSON is the recommended payload format, and is the only format supported for versions 2015-12-11 and later.  
  
#### JSON (versions 2013-08-15 and later)  
 Here is a sample JSON response body for the `Query Tables` operations.  
  
 **Full Metadata**  
  
```  
{  
   "odata.metadata":"https://myaccount.table.core.windows.net/$metadata#Tables",  
   "value":[  
      {  
         "odata.type":"myaccount.Tables",  
         "odata.id":"https://myaccount.table.core.windows.net/Tables('mytable')",  
         "odata.editLink":"Tables('mytable')",  
         "TableName":"mytable"  
      }  
}  
```  
  
 **Minimal Metadata**  
  
```  
{  
    "odata.metadata":"https://myaccount.table.core.windows.net/$metadata#Tables",  
    "value":[{  
        "TableName":"mytable"  
    }]  
}  
```  
  
 **No Metadata**  
  
```  
{  
   "value":[{  
       "TableName":"mytable"  
   },  
}  
```  
  
#### Atom Feed (versions prior to 2015-12-11)  
 Here is a sample Atom response body for the `Query Tables` operation.  
  
```  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<feed xml:base="https://myaccount.table.core.windows.net/" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">  
  <title type="text">Tables</title>  
  <id>https://myaccount.table.core.windows.net/Tables</id>  
  <updated>2009-01-04T17:18:54.7062347Z</updated>  
  <link rel="self" title="Tables" href="Tables" />  
  <entry>  
    <id>https://myaccount.table.core.windows.net/Tables('mytable')</id>  
    <title type="text"></title>  
    <updated>2009-01-04T17:18:54.7062347Z</updated>  
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
</feed>   
```  
  
## Authorization  
 Only the account owner may call this operation.  
  
## Remarks  
 A query against the Table service may return a maximum of 1,000 tables at one time and may execute for a maximum of five seconds. If the result set contains more than 1,000 tables, if the query did not complete within five seconds, or if the query crosses the partition boundary, the response includes a custom header containing the `x-ms-continuation-NextTableName` continuation token. The continuation token may be used to construct a subsequent request for the next page of data. For more information about continuation tokens, see [Query Timeout and Pagination](../StorageServicesREST/Query-Timeout-and-Pagination.md).  
  
> [!NOTE]
>  When making subsequent requests that include continuation tokens, be sure to pass the original URI on the request. For example, if you have specified a `$filter`, `$select`, or `$top` query option as part of the original request, you will want to include that option on subsequent requests. Otherwise your subsequent requests may return unexpected results.  
>   
>  Note that the `$top` query option in this case specifies the maximum number of results per page, not the maximum number of results in the whole response set.  
>   
>  See [Querying Tables and Entities](../StorageServicesREST/Querying-Tables-and-Entities.md) for more details.  
  
 Note that the total time allotted to the request for scheduling and processing the query is 30 seconds, including the five seconds for query execution.  
  
 For more information about supported query operations against the Table service through LINQ, see [Query Operators Supported for the Table Service](../StorageServicesREST/Query-Operators-Supported-for-the-Table-Service.md) and [Writing LINQ Queries Against the Table Service](../StorageServicesREST/Writing-LINQ-Queries-Against-the-Table-Service.md).  
  
## See Also  
 [Addressing Table Service Resources](../StorageServicesREST/Addressing-Table-Service-Resources.md)   
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Setting the OData Data Service Version Headers](../StorageServicesREST/Setting-the-OData-Data-Service-Version-Headers.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Table Service Error Codes](../StorageServicesREST/Table-Service-Error-Codes.md)
---
title: "Query Entities"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 8cfef6f9-eb7f-40f0-9016-dff44d36b6e1
caps.latest.revision: 68
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
# Query Entities
The `Query Entities` operation queries entities in a table and includes the `$filter` and `$select` options.  
  
## Request  
 For requests using the `$select` query option, the request must be made using version 2011-08-18 or later. In addition, the `DataServiceVersion` and `MaxDataServiceVersion` headers must be set to **2.0**. The `Query Entities` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account, and `mytable` with the name of your table:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`GET`|`https://myaccount.table.core.windows.net/mytable(PartitionKey='<partition-key>',RowKey='<row-key>')?$select=<comma-separated-property-names>`<br /><br /> `https://myaccount.table.core.windows.net/mytable()?$filter=<query-expression>&$select=<comma-separated-property-names>`|HTTP/1.1|  
  
 The address of the entity set to be queried may take a number of forms on the request URI. For more information, see [Querying Tables and Entities](../StorageServicesREST/Querying-Tables-and-Entities.md).  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Table service port as `127.0.0.1:10002`, followed by the emulated storage account name:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`GET`|`http://127.0.0.1:10002/devstoreaccount1/mytable(PartitionKey='<partition-key>',RowKey='<row-key>')?$select=<comma-separated-property-names>`<br /><br /> `http://127.0.0.1:10002/devstoreaccount1/mytable()?$filter=<query-expression>?$select=<comma-separated-property-names>`|HTTP/1.1|  
  
 The Table service in the storage emulator differs from the Windows® Azure™ Table service in several ways. For more information, see [Differences Between the Storage Emulator and Azure Storage Services](assetId:///c60f2090-c0f4-4817-8559-e98786461dbe).  
  
### URI Parameters  
 The `Query Entities` operation supports the query options defined by the OData Protocol Specification. For more information, see [OData Protocol](http://www.odata.org/).  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Optional. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`Accept`|Optional. Specifies the accepted content type of the response payload. Possible values are:<br /><br /> -   `application/atom+xml` (versions prior to 2015-12-11 only)<br />-   `application/json;odata=nometadata`<br />-   `application/json;odata=minimalmetadata`<br />-   `application/json;odata=fullmetadata`<br /><br /> For more information, see [Payload Format for Table Service Operations](../StorageServicesREST/Payload-Format-for-Table-Service-Operations.md).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
### Request Body  
 None.  
  
### Sample Request  
  
```  
Request Syntax:  
GET /myaccount/Customers()?$filter=(Rating%20ge%203)%20and%20(Rating%20le%206)&$select=PartitionKey,RowKey,Address,CustomerSince  HTTP/1.1  
  
Request Headers:  
x-ms-version: 2015-12-11  
x-ms-date: Mon, 27 Jun 2016 15:25:14 GMT  
Authorization: SharedKeyLite myaccount:<some key>  
Accept: application/json;odata=nometadata  
Accept-Charset: UTF-8  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
```  
  
## Response  
 The response includes an HTTP status code, a set of response headers, and a response body.  
  
### Status Code  
 A successful operation returns status code 200 (OK).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md) and [Table Service Error Codes](../StorageServicesREST/Table-Service-Error-Codes.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`x-ms-continuation-NextPartitionKey`<br /><br /> `x-ms-continuation-NextRowKey`|The service returns the `x-ms-continuation-NextPartitionKey` and `x-ms-continuation-NextRowKey` continuation headers in the following cases:<br /><br /> -   When  the number of entities to be returned exceeds 1,000.<br />-   When the server timeout interval is exceeded.<br />-   When a server boundary is reached, if the query returns data that is spread across multiple servers.<br /><br /> For more information about using the continuation tokens, see [Query Timeout and Pagination](../StorageServicesREST/Query-Timeout-and-Pagination.md).|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Table service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
|`Content-Type`|Indicates the content type of the payload. The value of this header depends on the value of the `Accept` request header. Possible values are:<br /><br /> -   `application/atom+xml` (versions prior to 2015-12-11 only)<br />-   `application/json;odata=nometadata`<br />-   `application/json;odata=minimalmetadata`<br />-   `application/json;odata=fullmetadata`<br /><br /> For more information about valid content types, see [Payload Format for Table Service Operations](../StorageServicesREST/Payload-Format-for-Table-Service-Operations.md).|  
  
### Sample Response  
  
```  
Response Status:  
HTTP/1.1 200 OK  
  
Response Headers:  
Content-Type: application/json  
x-ms-request-id: 87f178c0-44fe-4123-a4c1-96c8fa6d9654  
Date: Mon, 27 Jun 2016 15:25:14 GMT  
x-ms-version: 2015-12-11  
Connection: close  
```  
  
### Response Body  
 The `Query Entities` operation returns the list of entities in a table as an OData entity set, either in a JSON format or an Atom feed, depending on the `Accept` header of the request.  
  
> [!NOTE]
>  JSON is the recommended payload format, and is the only format supported for versions 2015-12-11 and later.  
  
#### JSON (versions 2013-08-15 and later)  
 Here is a sample request URI for a `Query Entities` operation on a Customers table.  
  
```  
GET /myaccount/Customers()?$filter=(Rating%20ge%203)%20and%20(Rating%20le%206)&$select=PartitionKey,RowKey,Address,CustomerSince  
```  
  
 Here are the response payloads in JSON for different control levels.  
  
 **No Metadata:**  
  
```  
{  
   "value":[  
      {  
         "PartitionKey":"Customer",  
         "RowKey":"Name",  
         "Timestamp":"2013-08-22T00:20:16.3134645Z",  
         "CustomerSince":"2008-10-01T15:25:05.2852025Z"  
      }  
   ]  
}  
```  
  
 **Minimal Metadata:**  
  
```  
{  
   "odata.metadata":"https://myaccount.table.core.windows.net/$metadata#Customers",  
   "value":[  
      {  
         "PartitionKey":"Customer",  
         "RowKey":"Name",  
         "Timestamp":"2013-08-22T00:20:16.3134645Z",  
         "CustomerSince@odata.type":"Edm.DateTime",  
         "CustomerSince":"2008-10-01T15:25:05.2852025Z"  
      }  
   ]  
}  
```  
  
 **Full Metadata:**  
  
```  
{  
   "odata.metadata":" https://myaccount.table.core.windows.net/metadata#Customers",  
   "value":[  
      {  
         "odata.type":"myaccount.Customers",  
         "odata.id":"https://myaccount.table.core.windows.net/Customers(PartitionKey=Customer',RowKey='Name')",  
         "odata.etag":"W/\"0x5B168C7B6E589D2\"",  
         "odata.editLink":"Customers(PartitionKey=Customer',RowKey='Name')",  
         "PartitionKey":"Customer",  
         "RowKey":"Name",  
         "Timestamp@odata.type":"Edm.DateTime",  
         "Timestamp":"2013-08-22T00:20:16.3134645Z",  
         "CustomerSince@odata.type":"Edm.DateTime",  
         "CustomerSince":"2008-10-01T15:25:05.2852025Z"  
      }  
   ]  
}  
```  
  
#### Atom Feed (versions prior to 2015-12-11)  
 Here is a sample request URI for a `Query Entities` operation on a Customers table.  
  
```  
GET /myaccount/Customers()?$filter=(Rating%20ge%203)%20and%20(Rating%20le%206)&$select=PartitionKey,RowKey,Address,CustomerSince  
```  
  
 Here is a sample Atom response for the `Query Entities` operation.  
  
```  
<?xml version="1.0" encoding="UTF-8"?>  
<feed xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xml:base="https://myaccount.table.core.windows.net">  
   <id>https://myaccount.table.core.windows.net/Customers</id>  
   <title type="text">Customers</title>  
   <updated>2013-08-22T00:50:32Z</updated>  
   <link rel="self" title="Customers" href="Customers" />  
   <entry m:etag="W/"0x5B168C7B6E589D2"">  
      <id>https://myaccount.table.core.windows.net/Customers(PartitionKey='Customer',RowKey='Name')</id>  
      <category term="myaccount.Customers" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />  
      <link rel="edit" title="Customers" href="Customers(PartitionKey='Customer',RowKey='Name')" />  
      <title />  
      <updated>2013-08-22T00:50:32Z</updated>  
      <author>  
         <name />  
      </author>  
      <content type="application/xml">  
         <m:properties>  
            <d:PartitionKey>Customer</d:PartitionKey>  
            <d:RowKey>Name</d:RowKey>  
            <d:Timestamp m:type="Edm.DateTime">2013-08-22T00:20:16.3134645Z</d:Timestamp>  
            <d:CustomerSince m:type="Edm.DateTime">2008-10-01T15:25:05.2852025Z</d:CustomerSince>  
         </m:properties>  
      </content>  
   </entry>  
</feed>  
```  
  
## Authorization  
 This operation can be performed by the account owner and by anyone with a shared access signature that has permission to perform this operation.  
  
## Remarks  
 A query against the Table service may return a maximum of 1,000 entities at one time and may execute for a maximum of five seconds. If the result set contains more than 1,000 entities, if the query did not complete within five seconds, or if the query crosses the partition boundary, the response includes custom headers containing a set of continuation tokens. The continuation tokens may be used to construct a subsequent request for the next page of data. For more information about continuation tokens, see [Query Timeout and Pagination](../StorageServicesREST/Query-Timeout-and-Pagination.md).  
  
> [!NOTE]
>  When making subsequent requests that include continuation tokens, be sure to pass the original URI on the request. For example, if you have specified a `$filter`, `$select`, or `$top` query option as part of the original request, you will want to include that option on subsequent requests. Otherwise your subsequent requests may return unexpected results.  
>   
>  Note that the `$top` query option in this case specifies the maximum number of results per page, not the maximum number of results in the whole response set.  
>   
>  See [Querying Tables and Entities](../StorageServicesREST/Querying-Tables-and-Entities.md) for more details.  
  
 For projection requests using the `$select` query option, the request must be made using version 2011-08-18 or newer. The maximum number of returned properties is 255, and all projected properties will be included in the response body even if the property is not part of the returned entity. For example, if the request includes a property that the projected entity does not contain, the missing property is marked with a null attribute. The sample response body above includes the Address property, which is not part of the projected entity, so the property is null: `<d:Address m:null=”true” />`  
  
 The total time allotted to the request for scheduling and processing the query is 30 seconds, including the five seconds for query execution.  
  
 Note that the right-hand side of a query expression must be a constant; you cannot reference a property on the right-hand side of the expression. See [Querying Tables and Entities](../StorageServicesREST/Querying-Tables-and-Entities.md) for details on constructing query expressions.  
  
 A query expression may not contain `null` values. The following characters must be encoded if they are to be used in a query string:  
  
-   Forward slash (/)  
  
-   Question mark (?)  
  
-   Colon (:)  
  
-   'At' symbol (@)  
  
-   Ampersand (&)  
  
-   Equals sign (=)  
  
-   Plus sign (+)  
  
-   Comma (,)  
  
-   Dollar sign ($)  
  
 Any application that can authenticate and send an HTTP `GET` request can query entities in a table.  
  
 For more information about supported query operations against the Table service through LINQ, see [Query Operators Supported for the Table Service](../StorageServicesREST/Query-Operators-Supported-for-the-Table-Service.md) and [Writing LINQ Queries Against the Table Service](../StorageServicesREST/Writing-LINQ-Queries-Against-the-Table-Service.md).  
  
## See Also  
 [Table Service Error Codes](../StorageServicesREST/Table-Service-Error-Codes.md)   
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Addressing Table Service Resources](../StorageServicesREST/Addressing-Table-Service-Resources.md)   
 [Querying Tables and Entities](../StorageServicesREST/Querying-Tables-and-Entities.md)   
 [Setting the OData Data Service Version Headers](../StorageServicesREST/Setting-the-OData-Data-Service-Version-Headers.md)   
 [Insert Entity](../StorageServicesREST/Insert-Entity.md)   
 [Update Entity](../StorageServicesREST/Update-Entity2.md)   
 [Delete Entity](../StorageServicesREST/Delete-Entity1.md)
---
title: "List Queues1"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
H1: List Queues
ms.assetid: c7f6a4d1-65e8-4375-974a-d04d6e934bae
caps.latest.revision: 51
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
# List Queues1
This operation lists all of the queues in a given storage account.  
  
## Request  
 The `List Queues` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`GET`|`https://myaccount.queue.core.windows.net?comp=list`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Queue service port as `127.0.0.1:10001`, followed by the emulated storage account name:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`GET`|`http://127.0.0.1:10001/devstoreaccount1?comp=list`|HTTP/1.1|  
  
### URI Parameters  
 The following additional parameters may be specified on the request URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`prefix`|Filters the results to return only queues with names that begin with the specified prefix.|  
|`marker`|A string value that identifies the portion of the list to be returned with the next list operation. The operation returns a `NextMarker` element within the response body if the list returned was not complete. This value may then be used as a query parameter in a subsequent call to request the next portion of the list of queues.<br /><br /> The marker value is opaque to the client.|  
|`maxresults`|Specifies the maximum number of queues to return. If `maxresults` is not specified, the server will return up to 5,000 items.|  
|`include=metadata`|Optional. Include this parameter to specify that the container's metadata be returned as part of the response body.<br /><br /> Note that metadata requested with this parameter must be stored in accordance with the naming restrictions imposed by the 2009-09-19 version of the Queue service. Beginning with this version, all metadata names must adhere to the naming conventions for [C# identifiers](http://msdn.microsoft.com/library/aa664670%28VS.71%29.aspx).|  
|`timeout`|Optional. The `timeout` parameter is expressed in seconds. For more information, see [Setting Timeouts for Queue Service Operations](../StorageServicesREST/Setting-Timeouts-for-Queue-Service-Operations.md).|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Optional. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
### Request Body  
 None.  
  
### Sample Request  
 See the Sample Request and Response section below for a sample request.  
  
## Response  
 The response includes an HTTP status code, a set of response headers, and a response body containing the list of queues.  
  
### Status Code  
 A successful operation returns status code 200 (OK).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Queue service used to execute the request. This header is returned for requests made against version 2009-09-19 and above.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
### Response Body  
 The format of the response body is as follows. Note that the `Prefix`, `Marker`, and `MaxResults` elements are only present if they were specified on the URI. The `NextMarker` element has a value only if the list results are not complete.  
  
 For version 2013-08-15 and newer, the `AccountName` attribute for the `EnumerationResults` element has been renamed to `ServiceEndpoint`. In addition, the `Url` element under `Queue` has been removed.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<EnumerationResults ServiceEndpoint="https://myaccount.queue.core.windows.net/">  
  <Prefix>string-value</Prefix>  
  <Marker>string-value</Marker>  
  <MaxResults>int-value</MaxResults>  
  <Queues>  
    <Queue>  
      <Name>string-value</Name>  
      <Metadata>  
      <metadata-name>value</metadata-name>  
    <Metadata>  
    </Queue>  
  <NextMarker />  
</EnumerationResults>  
```  
  
 The `Metadata` element is present only if the `include=metadata` parameter was specified on the URI. Within the `Metadata` element, the value of each name-value pair is listed within an element corresponding to the pair's name.  
  
 If a metadata name-value pair violates the naming restrictions enforced by the 2009-09-19 version, the response body indicates the problematic name within an `x-ms-invalid-name` element, as shown in the following XML fragment:  
  
```  
  
…  
<Metadata>  
  <MyMetadata1>first value</MyMetadata1>  
  <MyMetadata2>second value</MyMetadata2>  
  <x-ms-invalid-name>invalid-metadata-name</x-ms-invalid-name>  
<Metadata>  
…  
  
```  
  
### Sample Response  
 See the Sample Request and Response section below for a sample response.  
  
## Authorization  
 Only the account owner may call this operation.  
  
## Remarks  
 If you specify a value for the `maxresults` parameter and the number of queues to return exceeds this value, or exceeds the default value for `maxresults`, the response body will contain a `NextMarker` element that indicates the next queue to return on a subsequent request. To return the next set of items, specify the value of `NextMarker` as the marker parameter on the URI for the subsequent request.  
  
 Note that the value of `NextMarker` should be treated as opaque.  
  
 Queues are listed in alphabetical order in the response body.  
  
## Sample Request and Response  
 Here is a sample URI that requests the list of queues for an account, setting the maximum results to return for the initial operation to 3.  
  
```  
GET https://myaccount.queue.core.windows.net?comp=list&maxresults=3&include=metadata HTTP/1.1  
```  
  
 The request is sent with these headers:  
  
```  
x-ms-version: 2013-08-15  
x-ms-date: Wed, 23 Oct 2013 00:55:16 GMT  
Authorization: SharedKey myaccount:Q7tar7qqM2LD/Wey7OQNPP3hMNap9wjg+g9AlAYeFls=  
```  
  
 The status code and response headers are returned as follows:  
  
```  
HTTP/1.1 200 OK  
Transfer-Encoding: chunked  
Content-Type: application/xml  
Date: Wed, 23 Oct 2013 00:56:38 GMT  
x-ms-version: 2013-08-15  
Server: Windows-Azure-Queue/1.0 Microsoft-HTTPAPI/2.0  
```  
  
 The response XML for this request is as follows. Note that the `NextMarker` element follows the set of queues and includes the name of the next queue to be returned.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<EnumerationResults ServiceEndpoint="https://myaccount.queue.core.windows.net/">  
  <Prefix>q</Prefix>  
  <MaxResults>3</MaxResults>  
  <Queues>  
    <Queue>  
      <Name>q1</Name>  
      <Metadata>  
        <Color>red</Color>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      <Metadata>  
    </Queue>  
    <Queue>  
      <Name>q2</Name>  
      <Metadata>  
        <Color>blue</Color>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      <Metadata>  
    </Queue>  
    <Queue>  
      <Name>q3</Name>  
      <Metadata>  
        <Color>yellow</Color>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      <Metadata>  
    </Queue>  
  </Queues>  
  <NextMarker>q4</NextMarker>  
</EnumerationResults>  
```  
  
 The subsequent list operation specifies the marker on the request URI, as follows. The next set of results is returned beginning with the queue specified by the marker. Here is the URI for the subsequent request:  
  
```  
https://myaccount.queue.core.windows.net?comp=list&maxresults=3&include=metadata&prefix=q&marker=q4  
```  
  
 The response body for this operation is as follows:  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<EnumerationResults ServiceEndpoint="https://myaccount.queue.core.windows.net/">  
  <Prefix>q</Prefix>  
  <Marker>q4</Marker>  
  <MaxResults>3</MaxResults>  
  <Queues>  
    <Queue>  
      <Name>q4</Name>  
      <Metadata>  
        <Color>green</Color>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      <Metadata>  
    </Queue>  
    <Queue>  
      <Name>q5</Name>  
      <Metadata>  
        <Color>violet</Color>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      <Metadata>  
    </Queue>  
  </Queues>  
  <NextMarker />  
</EnumerationResults>  
```  
  
## See Also  
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Queue Service Error Codes](../StorageServicesREST/Queue-Service-Error-Codes.md)
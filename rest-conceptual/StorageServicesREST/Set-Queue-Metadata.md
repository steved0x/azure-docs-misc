---
title: "Set Queue Metadata"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 103b2fb9-8cb6-48dd-b185-d1454b08acce
caps.latest.revision: 46
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
# Set Queue Metadata
The `Set Queue Metadata` operation sets user-defined metadata on the specified queue. Metadata is associated with the queue as name-value pairs.  
  
## Request  
 The `Set Queue Metadata` request may be constructed as follows. HTTPS is recommended.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`PUT`|`https://myaccount.queue.core.windows.net/myqueue?comp=metadata`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Queue service port as `127.0.0.1:10001`, followed by the emulated storage account name:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`PUT`|`http://127.0.0.1:10001/devstoreaccount1/myqueue?comp=metadata`|HTTP/1.1|  
  
### URI Parameters  
 The following additional parameters may be specified on the request URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`timeout`|Optional. The `timeout` parameter is expressed in seconds. For more information, see [Setting Timeouts for Queue Service Operations](../StorageServicesREST/Setting-Timeouts-for-Queue-Service-Operations.md).|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Optional. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-meta-name:string-value`|Optional. A name-value pair to associate with the queue as metadata.<br /><br /> Each call to this operation replaces all existing metadata attached to the queue. To remove all metadata from the queue, call this operation with no metadata headers.<br /><br /> Note that beginning with version 2009-09-19, metadata names must adhere to the naming rules for [C# identifiers](http://msdn.microsoft.com/library/aa664670%28VS.71%29.aspx).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
### Request Body  
 None.  
  
### Sample Request  
  
```  
Request Syntax:  
PUT https://myaccount.queue.core.windows.net/myqueue?comp=metadata HTTP/1.1  
  
Request Headers:  
x-ms-version: 2011-08-18  
x-ms-date: Fri, 16 Sep 2011 01:47:14 GMT  
x-ms-meta-meta-sample1: sample1  
x-ms-meta-meta-sample2: sample2  
Authorization: SharedKey myaccount:u6PSIebDltGW5xHpO77epRpiUhcsTkWMvcM4GTmfqqA=  
```  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 204 (No Content).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Queue service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
### Response Body  
 None.  
  
## Authorization  
 Only the account owner may call this operation.  
  
## Remarks  
 To delete queue metadata, call `Set Queue Metadata` without specifying any metadata headers.  
  
## See Also  
 [Queue Service Error Codes](../StorageServicesREST/Queue-Service-Error-Codes.md)   
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)
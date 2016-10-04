---
title: "Delete Container"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 739dce1a-fc67-4655-8033-aa8ea72cded4
caps.latest.revision: 57
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
# Delete Container
The `Delete Container` operation marks the specified container for deletion. The container and any blobs contained within it are later deleted during garbage collection.  
  
## Request  
 The `Delete Container` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`DELETE`|`https://myaccount.blob.core.windows.net/mycontainer?restype=container`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Blob service port as `127.0.0.1:10000`, followed by the emulated storage account name:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`DELETE`|`http://127.0.0.1:10000/devstoreaccount1/mycontainer?restype=container`|HTTP/1.1|  
  
 For more information, see [Using the Azure Storage Emulator for Development and Testing](assetId:///f0e3acde-f019-4148-9544-34cf2ff27211).  
  
### URI Parameters  
 The following additional parameters may be specified on the request URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`timeout`|Optional. The `timeout` parameter is expressed in seconds. For more information, see [Setting Timeouts for Blob Service Operations](../StorageServicesREST/Setting-Timeouts-for-Blob-Service-Operations.md).|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-lease-id: <ID>`|Required for version 2012-02-12 and newer if the container has an active lease. To call `Delete Container` on a container that has an active lease, specify the lease ID in this header. If this header is not specified when there is an active lease, `Delete Container` will return `409 (Conflict)`.  If you specify the wrong lease ID, or a lease ID on a container that does not have an active lease, `Delete Container` will return `412 (Precondition failed)`.|  
|`x-ms-version`|Required for all authenticated requests. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
 This operation also supports the use of conditional headers to delete the container only if a specified condition is met. For more information, see [Specifying Conditional Headers for Blob Service Operations](../StorageServicesREST/Specifying-Conditional-Headers-for-Blob-Service-Operations.md).  
  
### Request Body  
 None.  
  
### Sample Request  
  
```  
Request Syntax:  
DELETE https://myaccount.blob.core.windows.net/mycontainer?restype=container HTTP/1.1  
  
Request Headers:  
x-ms-version: 2011-08-18  
x-ms-date: Sun, 25 Sep 2011 21:44:34 GMT  
Authorization: SharedKey devstoreaccount1:t7mf5htNuwLFX9g0S2LDdRtRn1FQzMAluBvHy1QPpnM=  
```  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 202 (Accepted).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?LinkId=73147).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Blob service used to execute the request. This header is returned for requests made against version 2009-09-19 and above.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
### Response Body  
 None.  
  
### Sample Response  
  
```  
Response Status:  
HTTP/1.1 202 Accepted  
  
Response Headers:  
Transfer-Encoding: chunked  
Content-Type: application/xml  
Date: Sun, 25 Sep 2011 21:45:00 GMT  
x-ms-version: 2011-08-18  
Server: Windows-Azure-Blob/1.0 Microsoft-HTTPAPI/2.0  
```  
  
## Authorization  
 Only the account owner may call this operation.  
  
## Remarks  
 When a container is deleted, a container with the same name cannot be created for at least 30 seconds; the container may not be available for more than 30 seconds if the service is still processing the request. While the container is being deleted, attempts to create a container of the same name will fail with status code 409 (Conflict), with the service returning additional error information indicating that the container is being deleted. All other operations, including operations on any blobs under the container, will fail with status code 404 (Not Found) while the container is being deleted.  
  
## See Also  
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Blob Service Error Codes](../StorageServicesREST/Blob-Service-Error-Codes.md)   
 [Specifying Conditional Headers for Blob Service Operations](../StorageServicesREST/Specifying-Conditional-Headers-for-Blob-Service-Operations.md)
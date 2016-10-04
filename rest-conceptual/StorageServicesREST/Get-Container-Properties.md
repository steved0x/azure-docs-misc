---
title: "Get Container Properties"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 34898af6-cde6-4de2-8ab9-a3c889771ef3
caps.latest.revision: 62
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
# Get Container Properties
The `Get Container Properties` operation returns all user-defined metadata and system properties for the specified container. The data returned does not include the container's list of blobs.  
  
## Request  
 The `Get Container Properties` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`GET/HEAD`|`https://myaccount.blob.core.windows.net/mycontainer?restype=container`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Blob service port as `127.0.0.1:10000`, followed by the emulated storage account name:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`GET/HEAD`|`http://127.0.0.1:10000/devstoreaccount1/mycontainer?restype=container`|HTTP/1.1|  
  
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
|`x-ms-lease-id: <ID>`|Optional, version 2012-02-12 and newer. If specified, `Get Container Properties` only succeeds if the container’s lease is active and matches this ID. If there is no active lease or the ID does not match, `412 (Precondition Failed)` is returned.|  
|`x-ms-version`|Required for all authenticated requests, optional for anonymous requests. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
### Request Body  
 None.  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 200 (OK).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`x-ms-meta-name:value`|Returns a string containing a name/value pair associated with the container as metadata.|  
|`ETag`|The entity tag for the container. If the request version is 2011-08-18 or newer, the ETag value will be in quotes.|  
|`Last-Modified`|Returns the date and time the container was last modified. The date format follows RFC 1123. For more information, see [Representation of Date-Time Values in Headers](../StorageServicesREST/Representation-of-Date-Time-Values-in-Headers.md).<br /><br /> Any operation that modifies the container or its properties or metadata updates the last modified time. Operations on blobs do not affect the last modified time of the container.|  
|`x-ms-lease-status: <locked &#124; unlocked>`|Version 2012-02-12 and newer. The lease status of the container.|  
|`x-ms-lease-state: <available &#124; leased &#124; expired &#124; breaking &#124; broken>`|Version 2012-02-12 and newer. Lease state of the container.|  
|`x-ms-lease-duration: <infinite &#124; fixed >`|Version 2012-02-12 and newer, only when the container is leased. Specifies whether the lease on a container is of infinite or fixed duration.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Version 2009-09-19 and newer. Indicates the version of the Blob service used to execute the request.<br /><br /> Also returned for anonymous requests without a version specified if the container was marked for public access using the 2009-09-19 version of the Blob service.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
### Response Body  
 None.  
  
### Sample Response  
  
```  
Response Status:  
HTTP/1.1 200 OK  
  
Response Headers:  
Transfer-Encoding: chunked  
x-ms-meta-Name: StorageSample  
Date: Sun, 25 Sep 2011 12:43:08 GMT  
ETag: "0x8CAFB82EFF70C46"  
Last-Modified: Sun, 25 Sep 2011 10:42:18 GMT  
x-ms-version: 2011-08-18  
Server: Windows-Azure-Blob/1.0 Microsoft-HTTPAPI/2.0  
```  
  
## Authorization  
 If the container's access control list (ACL) is set to allow anonymous access to the container, any client may call this operation. If the container is private, this operation can be performed by the account owner.  
  
## Remarks  
 None.  
  
## See Also  
 [Operations on Containers](../StorageServicesREST/Operations-on-Containers.md)
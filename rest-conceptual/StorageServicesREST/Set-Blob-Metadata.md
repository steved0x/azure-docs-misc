---
title: "Set Blob Metadata"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 81fdc0ec-78d5-477c-9cb9-e8f722ec2fd3
caps.latest.revision: 54
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
# Set Blob Metadata
The `Set Blob Metadata` operation sets user-defined metadata for the specified blob as one or more name-value pairs.  
  
## Request  
 The `Set Blob Metadata` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
||PUT Method Request URI|HTTP Version|  
|-|----------------------------|------------------|  
||`https://myaccount.blob.core.windows.net/mycontainer/myblob?comp=metadata`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Blob service port as `127.0.0.1:10000`, followed by the emulated storage account name:  
  
||PUT Method Request URI|HTTP Version|  
|-|----------------------------|------------------|  
||`http://127.0.0.1:10000/devstoreaccount1/mycontainer/myblob?comp=metadata`|HTTP/1.1|  
  
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
|`x-ms-version`|Required for all authenticated requests. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-meta-name:value`|Optional. Sets a name-value pair for the blob.<br /><br /> Each call to this operation replaces all existing metadata attached to the blob. To remove all metadata from the blob, call this operation with no metadata headers.<br /><br /> Note that beginning with version 2009-09-19, metadata names must adhere to the naming rules for [C# identifiers](http://msdn.microsoft.com/library/aa664670%28VS.71%29.aspx).|  
|`x-ms-lease-id:<ID>`|Required if the blob has an active lease. To perform this operation on a blob with an active lease, specify the valid lease ID for this header.|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
 This operation also supports the use of conditional headers to set blob metadata only if a specified condition is met. For more information, see [Specifying Conditional Headers for Blob Service Operations](../StorageServicesREST/Specifying-Conditional-Headers-for-Blob-Service-Operations.md).  
  
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
|`ETag`|The ETag contains a value that you can use to perform operations conditionally. See [Specifying Conditional Headers for Blob Service Operations](../StorageServicesREST/Specifying-Conditional-Headers-for-Blob-Service-Operations.md) for more information. If the request version is 2011-08-18 or newer, the ETag value will be in quotes.|  
|`Last-Modified`|The date/time that the blob was last modified. The date format follows RFC 1123. For more information, see [Representation of Date-Time Values in Headers](../StorageServicesREST/Representation-of-Date-Time-Values-in-Headers.md).<br /><br /> Any write operation on the blob (including updates on the blob's metadata or properties) changes the last modified time of the blob.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Blob service used to execute the request. This header is returned for requests made against version 2009-09-19 and above.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
|`x-ms-request-server-encrypted: true/false`|Version 2015-12-11 or newer. The value of this header is set to `true` if the contents of the request are successfully encrypted using the specified algorithm, and `false` otherwise.|  
  
### Response Body  
 None.  
  
## Authorization  
 This operation can be called by the account owner and by anyone with a Shared Access Signature that has permission to write to this blob or its container.  
  
## Remarks  
 If the blob has an active lease, the client must specify a valid lease ID on the request in order to write metadata to the blob.  If the client does not specify a lease ID, or specifies an invalid lease ID, the Blob service returns status code 412 (Precondition Failed). If the client specifies a lease ID but the blob does not have an active lease, the Blob service also returns status code 412 (Precondition Failed).  
  
## See Also  
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Blob Service Error Codes](../StorageServicesREST/Blob-Service-Error-Codes.md)
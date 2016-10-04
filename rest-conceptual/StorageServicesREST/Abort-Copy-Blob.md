---
title: "Abort Copy Blob"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 1bb2695e-5fe2-4394-9b61-0c67fa07c240
caps.latest.revision: 18
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
# Abort Copy Blob
The `Abort Copy Blob` operation aborts a pending `Copy Blob` operation, and leaves a destination blob with zero length and full metadata. Version 2012-02-12 and newer.  
  
## Request  
 Construct the `Abort Copy Blob` as follows. HTTPS is recommended. Replace `myaccount` with the name of your storage account, `mycontainer` with the name of your container, `myblob` with the name of your destination blob, and `<id>` with the copy identifier provided in the `x-ms-copy-id` header of the original `Copy Blob` operation.  
  
 Beginning with version 2013-08-15, you may specify a shared access signature for the destination blob if it is in the same account as the source blob. Beginning with version 2015-04-05, you may also specify a shared access signature for the destination blob if it is in a different storage account.  
  
|PUT Method Request URI|HTTP Version|  
|----------------------------|------------------|  
|`https://myaccount.blob.core.windows.net/mycontainer/myblob?comp=copy&copyid=<id>`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the local storage service, specify the local hostname and Blob service port as `127.0.0.1:10000`, followed by the local storage account name:  
  
|PUT Method Request URI|HTTP Version|  
|----------------------------|------------------|  
|`http://127.0.0.1:10000/devstoreaccount1/mycontainer/myblob?comp=copy&copyid=<id>`|HTTP/1.1|  
  
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
|`x-ms-version`|Required for all authenticated requests. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-lease-id:<ID>`|Required if the destination blob has an active infinite lease.|  
|`x-ms-copy-action: abort`|Required.|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
### Request Body  
 None.  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 204 (No Content).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Blob service used to execute the request.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
## Authorization  
 Only the account owner may call this operation.  
  
## Remarks  
 When you abort a pending `Copy Blob` operation, the destination blob’s `x-ms-copy-status` header is set to `aborted`. Aborting a copy operation results in a destination blob of zero length for block blobs, append blobs, and page blobs. However, the metadata for the destination blob will have the new values copied from the source blob or set explicitly in the `Copy Blob` operation call. To keep the original metadata from before the copy, make a snapshot of the destination blob before calling `Copy Blob`.  
  
 You can only abort a copy operation that is pending. Trying to abort a copy that has completed or failed results in **409 Conflict**. Trying to abort a copy operation using an incorrect copy ID also results in **409 Conflict**.  
  
## See Also  
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Blob Service Error Codes](../StorageServicesREST/Blob-Service-Error-Codes.md)   
 [Copy Blob](../StorageServicesREST/Copy-Blob.md)
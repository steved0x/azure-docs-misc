---
title: "Delete Blob"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 7f64072c-fcc6-4e7d-8653-5017dc8da7be
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
# Delete Blob
The `Delete Blob` operation marks the specified blob or snapshot for deletion. The blob is later deleted during garbage collection.  
  
 Note that in order to delete a blob, you must delete all of its snapshots. You can delete both at the same time with the `Delete Blob` operation.  
  
## Request  
 The `Delete Blob` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
||DELETE Method Request URI|HTTP Version|  
|-|-------------------------------|------------------|  
||`https://myaccount.blob.core.windows.net/mycontainer/myblob`<br /><br /> `https://myaccount.blob.core.windows.net/mycontainer/myblob?snapshot=<DateTime>`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Blob service port as `127.0.0.1:10000`, followed by the emulated storage account name:  
  
||DELETE Method Request URI|HTTP Version|  
|-|-------------------------------|------------------|  
||`http://127.0.0.1:10000/devstoreaccount1/mycontainer/myblob`|HTTP/1.1|  
  
 For more information, see [Using the Azure Storage Emulator for Development and Testing](assetId:///f0e3acde-f019-4148-9544-34cf2ff27211).  
  
### URI Parameters  
 The following additional parameters may be specified on the request URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`snapshot`|Optional. The snapshot parameter is an opaque `DateTime` value that, when present, specifies the blob snapshot to delete. For more information on working with blob snapshots, see [Creating a Snapshot of a Blob](../StorageServicesREST/Creating-a-Snapshot-of-a-Blob.md).|  
|`timeout`|Optional. The `timeout` parameter is expressed in seconds. For more information, see [Setting Timeouts for Blob Service Operations](../StorageServicesREST/Setting-Timeouts-for-Blob-Service-Operations.md).|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Required for all authenticated requests. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-lease-id:<ID>`|Required if the blob has an active lease.<br /><br /> To perform this operation on a blob with an active lease, specify the valid lease ID for this header. If a valid lease ID is not specified on the request, the operation will fail with status code 403 (Forbidden).|  
|`x-ms-delete-snapshots: {include, only}`|Required if the blob has associated snapshots. Specify one of the following two options:<br /><br /> -   `include`: Delete the base blob and all of its snapshots.<br />-   `only`: Delete only the blob's snapshots and not the blob itself.<br /><br /> This header should be specified only for a request against the base blob resource. If this header is specified on a request to delete an individual snapshot, the Blob service returns status code 400 (Bad Request).<br /><br /> If this header is not specified on the request and the blob has associated snapshots, the Blob service returns status code 409 (Conflict).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
 This operation also supports the use of conditional headers to delete the blob only if a specified condition is met. For more information, see [Specifying Conditional Headers for Blob Service Operations](../StorageServicesREST/Specifying-Conditional-Headers-for-Blob-Service-Operations.md).  
  
### Request Body  
 None.  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 202 (Accepted).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Blob service used to execute the request. This header is returned for requests made against version 2009-09-19 and above.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
## Authorization  
 This operation can be performed by the account owner or by anyone using a Shared Access Signature that has permission to delete the blob.  
  
## Remarks  
 When a blob is successfully deleted, it is immediately removed from the storage account's index and is no longer accessible to clients. The blob's data is later removed from the service during garbage collection.  
  
 If the blob has an active lease, the client must specify a valid lease ID on the request in order to delete it.  
  
 If a blob has a large number of snapshots, it's possible that the `Delete Blob` operation will time out. If this happens, the client should retry the request.  
  
 For version 2013-08-15 and later, the client may call `Delete Blob` to delete uncommitted blobs. An uncommitted blob is a blob that was created with calls to the [Put Block](../StorageServicesREST/Put-Block.md) operation but never committed using the [Put Block List](../StorageServicesREST/Put-Block-List.md) operation. For earlier versions, the client must commit the blob first before deleting it.  
  
## See Also  
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Blob Service Error Codes](../StorageServicesREST/Blob-Service-Error-Codes.md)
---
title: "Get Page Ranges"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 6f176ace-8f1b-4e99-8eef-5c7ea22fcc22
caps.latest.revision: 28
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
# Get Page Ranges
The `Get Page Ranges` operation returns the list of valid page ranges for a page blob or snapshot of a page blob.  
  
## Request  
 The `Get Page Ranges` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
|GET Method Request URI|HTTP Version|  
|----------------------------|------------------|  
|`https://myaccount.blob.core.windows.net/mycontainer/myblob?comp=pagelist`<br /><br /> `https://myaccount.blob.core.windows.net/mycontainer/myblob?comp=pagelist&snapshot=<DateTime>`<br /><br /> `https://myaccount.blob.core.windows.net/mycontainer/myblob?comp=p  agelist&snapshot=<DateTime>&prevsnapshot=<DateTime>`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Blob service port as `127.0.0.1:10000`, followed by the emulated storage account name:  
  
|GET Method Request URI|HTTP Version|  
|----------------------------|------------------|  
|`http://127.0.0.1:10000/devstoreaccount1/mycontainer/myblob?comp=pagelist`|HTTP/1.1|  
  
 For more information, see [Using the Azure Storage Emulator for Development and Testing](assetId:///f0e3acde-f019-4148-9544-34cf2ff27211).  
  
### URI Parameters  
 The following additional parameters may be specified on the request URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`snapshot`|Optional. The snapshot parameter is an opaque `DateTime` value that, when present, specifies the blob snapshot to retrieve information from. For more information on working with blob snapshots, see [Creating a Snapshot of a Blob](../StorageServicesREST/Creating-a-Snapshot-of-a-Blob.md).|  
|`timeout`|Optional. The `timeout` parameter is expressed in seconds. For more information, see [Setting Timeouts for Blob Service Operations](../StorageServicesREST/Setting-Timeouts-for-Blob-Service-Operations.md).|  
|`prevsnapshot`|Optional in version 2015-07-08 and newer. The `prevsnapshot` parameter is a `DateTime` value that specifies that the response will contain only pages that were changed between target blob and previous snapshot.  Changed pages include both updated and cleared pages. The target blob may be a snapshot, as long as the snapshot specified by `prevsnapshot` is the older of the two.<br /><br /> Note that incremental snapshots are currently supported only for blobs created on or after January 1, 2016.|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Required for all authenticated requests, optional for anonymous requests. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`Range`|Optional. Specifies the range of bytes over which to list ranges, inclusively. If omitted, then all ranges for the blob are returned.|  
|`x-ms-range`|Optional. Specifies the range of bytes over which to list ranges, inclusively.<br /><br /> If both `Range` and `x-ms-range` are specified, the service uses the value of `x-ms-range`. See [Specifying the Range Header for Blob Service Operations](../StorageServicesREST/Specifying-the-Range-Header-for-Blob-Service-Operations.md) for more information.|  
|`x-ms-lease-id:<ID>`|Optional. If this header is specified, the operation will be performed only if both of the following conditions are met:<br /><br /> -   The blob's lease is currently active.<br />-   The lease ID specified in the request matches that of the blob.<br /><br /> If this header is specified and both of these conditions are not met, the request will fail and the operation will fail with status code 412 (Precondition Failed).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
 This operation also supports the use of conditional headers to get page ranges only if a specified condition is met. For more information, see [Specifying Conditional Headers for Blob Service Operations](../StorageServicesREST/Specifying-Conditional-Headers-for-Blob-Service-Operations.md).  
  
### Request Body  
 None.  
  
## Response  
 The response includes an HTTP status code, a set of response headers, and the response body.  
  
### Status Code  
 A successful operation returns status code 200 (OK).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Syntax|Description|  
|------------|-----------------|  
|`Last-Modified`|The date/time that the blob was last modified. The date format follows RFC 1123.<br /><br /> Any operation that modifies the blob, including an update of the blob's metadata or properties, changes the blob's last modified time.|  
|ETag|The ETag contains a value that the client can use to perform the operation conditionally. If the request version is 2011-08-18 or newer, the ETag value will be in quotes.|  
|`x-ms-blob-content-length`|The size of the blob in bytes.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Blob service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.<br /><br /> This header is also returned for anonymous requests without a version specified if the container was marked for public access using the 2009-09-19 version of the Blob service.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
### Response Body  
 The response body includes a list of non-overlapping valid page ranges, sorted by increasing address page range. The format of the response body is as follows.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<PageList>  
   <PageRange>  
      <Start>Start Byte</Start>  
      <End>End Byte</End>  
   </PageRange>  
   <PageRange>  
      <Start>Start Byte</Start>  
      <End>End Byte</End>  
   </PageRange>  
</PageList>  
```  
  
 If the blob's entire set of pages has been cleared, the response body will not include any page ranges.  
  
 If the `prevsnapshot` parameter was specified, the response will include only the pages that differ between the target snapshot or blob and the previous snapshot. The pages returned  include both pages that were updated or that were cleared. The format of this response body is as follows:  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<PageList>  
   <PageRange>  
      <Start>Start Byte</Start>  
      <End>End Byte</End>  
   </PageRange>  
   <ClearRange>  
      <Start>Start Byte</Start>  
      <End>End Byte</End>  
   </ClearRange>  
   <PageRange>  
      <Start>Start Byte</Start>  
      <End>End Byte</End>  
   </PageRange>  
</PageList>  
  
```  
  
 If the blob's entire set of pages has been cleared and the `prevsnapshot` parameter was not specified, the response body will not include any page ranges.  
  
## Authorization  
 This operation can be performed by the account owner or by anyone using a Shared Access Signature that has permission to read the blob. If the container's ACL is set to allow anonymous access, any client may call this operation.  
  
## Remarks  
 The start and end byte offsets for each page range are inclusive.  
  
 In a highly fragmented page blob with a large number of writes, a `Get Page Ranges` request can fail due to an internal server timeout. Applications retrieving ranges of a page blob with a large number of write operations should retrieve a subset of page ranges at a time. For more information, see [Getting the Page Ranges of a Large Page Blob in Segments](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/03/26/getting-the-page-ranges-of-a-large-page-blob-in-segments.aspx).  
  
 Beginning with version 2015-07-08, you can call `Get Page Ranges` with the `prevsnapshot` parameter to return the pages that differ between the base blob and a snapshot, or between two snapshots of the blob. Using these page differences, you can save an incremental snapshot of a page blob. Incremental snapshots are a cost-effective way to back up virtual machine disks if you wish to implement your own backup solution.  
  
 Calling `Get Page Ranges` with the `prevsnapshot` parameter returns pages that have been updated or cleared since the snapshot specified by `prevsnapshot` was taken. You can then copy the pages returned to a backup page blob in another storage account, using [Put Page](../StorageServicesREST/Put-Page.md).  
  
 Certain operations on a blob will cause `Get Page Ranges` to fail when called to return an incremental snapshot. `Get Pages Ranges` will fail with error code 409 (Conflict) if it is called on a blob that was the target of a [Put Blob](../StorageServicesREST/Put-Blob.md) or [Copy Blob](../StorageServicesREST/Copy-Blob.md) request after the snapshot specified by `prevsnapshot` was taken. If the target of the `Get Page Ranges` operation is itself a snapshot, then the call will succeed as long as the snapshot specified by `prevsnapshot` is older, and no `Put Blob` or `Copy Blob` operation was called in the interval between the two snapshots.  
  
> [!NOTE]
>  Incremental snapshots are currently supported only for blobs created on or after January 1, 2016. Attempting to use this feature on an older blob will result in the `BlobGenerationMismatch` error, which is HTTP error code 409 (Conlfict).  
  
## See Also  
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Setting Timeouts for Blob Service Operations](../StorageServicesREST/Setting-Timeouts-for-Blob-Service-Operations.md)   
 [Getting the Page Ranges of a Large Page Blob in Segments](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/03/26/getting-the-page-ranges-of-a-large-page-blob-in-segments.aspx)
---
title: "Snapshot Blob"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 64468b0e-315a-42ca-a090-e32e9bade1d7
caps.latest.revision: 30
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
# Snapshot Blob
The `Snapshot Blob` operation creates a read-only snapshot of a blob.  
  
## Request  
 The `Snapshot Blob` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
||PUT Method Request URI|HTTP Version|  
|-|----------------------------|------------------|  
||`https://myaccount.blob.core.windows.net/mycontainer/myblob?comp=snapshot`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Blob service port as `127.0.0.1:10000`, followed by the emulated account name:  
  
||PUT Method Request URI|HTTP Version|  
|-|----------------------------|------------------|  
||`http://127.0.0.1:10000/devstoreaccount1/mycontainer/myblob?comp=snapshot`|HTTP/1.1|  
  
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
|`x-ms-meta-name:value`|Optional. Specifies a user-defined name-value pair associated with the blob. If no name-value pairs are specified, the operation will copy the base blob metadata to the snapshot. If one or more name-value pairs are specified, the snapshot is created with the specified metadata, and metadata is not copied from the base blob.<br /><br /> Note that beginning with version 2009-09-19, metadata names must adhere to the naming rules for [C# identifiers](http://msdn.microsoft.com/library/aa664670%28VS.71%29.aspx). See [Naming and Referencing Containers, Blobs, and Metadata](../StorageServicesREST/Naming-and-Referencing-Containers--Blobs--and-Metadata.md) for more information.|  
|`If-Modified-Since`|Optional. A `DateTime` value. Specify this conditional header to snapshot the blob only if it has been modified since the specified date/time. If the base blob has not been modified, the Blob service returns status code 412 (Precondition Failed).|  
|`If-Unmodified-Since`|Optional. A `DateTime` value. Specify this conditional header to snapshot the blob only if it has not been modified since the specified date/time. If the base blob has been modified, the Blob service returns status code 412 (Precondition Failed).|  
|`If-Match`|Optional. An ETag value. Specify an ETag value for this conditional header to snapshot the blob only if its ETag value matches the value specified. If the values do not match, the Blob service returns status code 412 (Precondition Failed).|  
|`If-None-Match`|Optional. An ETag value.<br /><br /> Specify an ETag value for this conditional header to snapshot the blob only if its ETag value does not match the value specified. If the values are identical, the Blob service returns status code 412 (Precondition Failed).|  
|`x-ms-lease-id:<ID>`|Optional. If this header is specified, the operation will be performed only if both of the following conditions are met:<br /><br /> -   The blob's lease is currently active.<br />-   The lease ID specified in the request matches that of the blob.<br /><br /> If this header is specified and both of these conditions are not met, the request will fail and the `Snapshot Blob` operation will fail with status code 412 (Precondition Failed).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
 This operation also supports the use of conditional headers to execute the operation only if a specified condition is met. For more information, see [Specifying Conditional Headers for Blob Service Operations](../StorageServicesREST/Specifying-Conditional-Headers-for-Blob-Service-Operations.md).  
  
### Request Body  
 None.  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 201 (Created).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Syntax|Description|  
|------------|-----------------|  
|`x-ms-snapshot: <DateTime>`|This header returns a DateTime value that uniquely identifies the snapshot. The value of this header indicates the snapshot version, and may be used in subsequent requests to access the snapshot. Note that this value is opaque.|  
|`ETag`|The ETag of the snapshot. If the request version is 2011-08-18 or newer, the ETag value will be in quotes. Note that a snapshot cannot be written to, so the ETag of a given snapshot will never change.  However, the ETag of the snapshot will differ from that of the base blob if new metadata was supplied with the `Snaphot Blob` request. If no metadata was specified with the request, the ETag of the snapshot will be identical to that of the base blob at the time the snapshot was taken.|  
|`Last-Modified`|The last modified time of the snapshot. The date format follows RFC 1123. For more information, see [Representation of Date-Time Values in Headers](../StorageServicesREST/Representation-of-Date-Time-Values-in-Headers.md).<br /><br /> Note that a snapshot cannot be written to, so the last modified time of a given snapshot will never change. However, the last modified time of the snapshot will differ from that of the base blob if new metadata was supplied with the `Snaphot Blob` request. If no metadata was specified with the request, the last modified time of the snapshot will be identical to that of the base blob at the time the snapshot was taken.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Blob service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
### Response Body  
 None.  
  
## Authorization  
 Only the account owner may call this operation.  
  
## Remarks  
 Snapshots provide read-only versions of blobs. Once a snapshot has been created, it can be read, copied, or deleted, but not modified.  
  
 A snapshot provides a convenient way to back up blob data. You can use a snapshot to restore a blob to an earlier version by calling [Copy Blob](../StorageServicesREST/Copy-Blob.md) to overwrite a base blob with its snapshot.  
  
 When you create a snapshot, the Blob service returns a DateTime value that uniquely identifies the snapshot relative to its base blob. You can use this value to perform further operations on the snapshot. Note that you should treat this DateTime value as opaque.  
  
 The DateTime value identifies the snapshot on the URI. For example, a base blob and its snapshots have URIs similar to the following:  
  
-   **Base blob:** `http://myaccount.blob.core.windows.net/mycontainer/myblob`  
  
-   **Snapshot:** `http://myaccount.blob.core.windows.net/mycontainer/myblob?snapshot=<DateTime>`  
  
 Note that each time you call the `Snapshot Blob` operation, a new snapshot is created, with a unique DateTime value. A blob can support any number of snapshots. Existing snapshots are never overwritten, but must be deleted explicitly by calling [Delete Blob](../StorageServicesREST/Delete-Blob.md) and setting the `x-ms-include-snapshots` header to the appropriate value.  
  
 **Reading, Copying, and Deleting Snapshots**  
  
 A successful call to `Snapshot Blob` returns a DateTime value in the `x-ms-snapshot` response header. You can then use this DateTime value to perform read, delete, or copy operations on a particular snapshot version. Any Blob service operation that is valid for a snapshot can be called by specifying `?snapshot=<DateTime>` after the blob name.  
  
 **Copying Blob Properties and Metadata**  
  
 When you create a snapshot of a blob, the following system properties are copied to the snapshot with the same values:  
  
-   `Content-Type`  
  
-   `Content-Encoding`  
  
-   `Content-Language`  
  
-   `Content-Length`  
  
-   `Cache-Control`  
  
-   `Content-MD5`  
  
-   `x-ms-blob-sequence-number (for page blobs only)`  
  
-   `x-ms-blob-committed-block-count (for append blobs only)`  
  
-   `x-ms-copy-id` (version 2012-02-12 and newer)  
  
-   `x-ms-copy-status` (version 2012-02-12 and newer)  
  
-   `x-ms-copy-source` (version 2012-02-12 and newer)  
  
-   `x-ms-copy-progress` (version 2012-02-12 and newer)  
  
-   `x-ms-copy-completion-time` (version 2012-02-12 and newer)  
  
-   `x-ms-copy-status-description` (version 2012-02-12 and newer)  
  
 The base blob's committed block list is also copied to the snapshot, if the blob is a block blob. Any uncommitted blocks are not copied.  
  
 The snapshot blob is always the same size as the base blob at the time the snapshot is taken, so the value of the `Content-Length` header for the snapshot blob will be the same as that for the base blob.  
  
 You can specify one or more new metadata values for the snapshot by specifying the `x-ms-meta-name:value` header on the request. If this header is not specified, the metadata associated with the base blob is copied to the snapshot.  
  
 **Specifying Conditional Headers**  
  
 You can specify conditional headers on the request to snapshot the blob only if a condition is met. If the specified condition is not met, the snapshot is not created, and the Blob service returns status code 412 (Precondition Failed), along with additional error information about the unmet condition.  
  
 **Creating a Snapshot of a Leased Blob**  
  
 If the base blob has an active lease, you can snapshot the blob as long as either of the following conditions are true of the request:  
  
-   The conditional `x-ms-lease-id` header is specified, and the active lease ID for the base blob is included in the request. This condition specifies that the snapshot be created only if the lease is active and the specified lease ID matches that associated with the blob.  
  
-   The `x-ms-lease-id` header is not specified at all, in which case the exclusive-write lease is ignored.  
  
 Note that a lease associated with the base blob is not copied to the snapshot. Snapshots cannot be leased.  
  
 **Copying Snapshots**  
  
 When a base blob is copied using the [Copy Blob](../StorageServicesREST/Copy-Blob.md) operation, any snapshots of the base blob are not copied to the destination blob. When a destination blob is overwritten with a copy, any snapshots associated with the destination blob stay intact under its name.  
  
 You can copy a snapshot blob over its base blob to restore an earlier version of a blob. The snapshot remains, but the base blob is overwritten with a copy that can be both read and written.  
  
> [!NOTE]
>  Promoting a snapshot in this way does not incur an additional charge for storage resources, since blocks or pages are shared between the snapshot and the base blob.  
  
 **Snapshots in Premium Storage Accounts**  
  
 There are a few differences between Azure Premium Storage accounts and standard storage accounts in terms of snapshots:  
  
-   The number of snapshots per page blob in a Premium Storage account is limited to 100. If that limit is exceeded, the `Snapshot Blob` operation returns error code 409 (SnapshotCountExceeded).  
  
-   A snapshot of a page blob in a Premium Storage account may be taken once every ten minutes. If that rate is exceeded, the `Snapshot Blob` operation returns error code 409 (SnaphotOperationRateExceeded).  
  
-   Reading a snapshot of a page blob in a Premium Storage account via [Get Blob](../StorageServicesREST/Get-Blob.md) is not supported. Calling `Get Blob` on a snapshot in a Premium Storage account returns error code 400 (Invalid Operation). However, calling [Get Blob Properties](../StorageServicesREST/Get-Blob-Properties.md) and [Get Blob Metadata](../StorageServicesREST/Get-Blob-Metadata.md) against a snapshot is supported.  
  
     To read a snapshot, you can use the [Copy Blob](../StorageServicesREST/Copy-Blob.md) operation to copy a snapshot to another page blob in the account. The destination blob for the copy operation must not have any existing snapshots. If the destination blob does have snapshots, then `Copy Blob` returns error code 409 (SnapshotsPresent).  
  
 For more information on calling REST operations on Azure Premium Storage resources, see [Using Blob Service Operations with Azure Premium Storage](../StorageServicesREST/Using-Blob-Service-Operations-with-Azure-Premium-Storage.md).  
  
## See Also  
 [Creating a Snapshot of a Blob](../StorageServicesREST/Creating-a-Snapshot-of-a-Blob.md)   
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Blob Service Error Codes](../StorageServicesREST/Blob-Service-Error-Codes.md)
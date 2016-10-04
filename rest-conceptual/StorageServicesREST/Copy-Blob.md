---
title: "Copy Blob"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: b022aff3-053b-4bd7-9ebe-3f06e7e8f801
caps.latest.revision: 74
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
# Copy Blob
The `Copy Blob` operation copies a blob to a destination within the storage account. In version 2012-02-12 and later, the source for a Copy Blob operation can be a committed blob in any Azure storage account.  
  
 Beginning with version 2015-02-21, the source for a `Copy Blob` operation can be an Azure file in any Azure storage account.  
  
> [!NOTE]
>  Only storage accounts created on or after June 7th, 2012 allow the `Copy Blob` operation to copy from another storage account.  
  
## Request  
 The `Copy Blob` request may be constructed as follows. HTTPS is recommended. Replace `myaccount` with the name of your storage account, `mycontainer` with the name of your container, and `myblob` with the name of your destination blob.  
  
 Beginning with version 2013-08-15, you may specify a shared access signature for the destination blob if it is in the same account as the source blob. Beginning with version 2015-04-05, you may also specify a shared access signature for the destination blob if it is in a different storage account.  
  
||PUT Method Request URI|HTTP Version|  
|-|----------------------------|------------------|  
||`https://myaccount.blob.core.windows.net/mycontainer/myblob`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Blob service port as `127.0.0.1:10000`, followed by the emulated storage account name:  
  
||PUT Method Request URI|HTTP Version|  
|-|----------------------------|------------------|  
||`http://127.0.0.1:10000/devstoreaccount1/mycontainer/myblob`|HTTP/1.1|  
  
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
|`x-ms-meta-name:value`|Optional. Specifies a user-defined name-value pair associated with the blob. If no name-value pairs are specified, the operation will copy the metadata from the source blob or file to the destination blob. If one or more name-value pairs are specified, the destination blob is created with the specified metadata, and metadata is not copied from the source blob or file.<br /><br /> Note that beginning with version 2009-09-19, metadata names must adhere to the naming rules for [C# identifiers](http://msdn.microsoft.com/library/aa664670%28VS.71%29.aspx).  See [Naming and Referencing Containers, Blobs, and Metadata](../StorageServicesREST/Naming-and-Referencing-Containers--Blobs--and-Metadata.md) for more information.|  
|`x-ms-source-if-modified-since`|Optional. A `DateTime` value. Specify this conditional header to copy the blob only if the source blob has been modified since the specified date/time. If the source blob has not been modified, the Blob service returns status code 412 (Precondition Failed). This header cannot be specified if the source is an Azure File.|  
|`x-ms-source-if-unmodified-since`|Optional. A `DateTime` value. Specify this conditional header to copy the blob only if the source blob has not been modified since the specified date/time. If the source blob has been modified, the Blob service returns status code 412 (Precondition Failed). This header cannot be specified if the source is an Azure File.|  
|`x-ms-source-if-match`|Optional. An ETag value. Specify this conditional header to copy the source blob only if its ETag matches the value specified. If the ETag values do not match, the Blob service returns status code 412 (Precondition Failed). This header cannot be specified if the source is an Azure File.|  
|`x-ms-source-if-none-match`|Optional. An ETag value. Specify this conditional header to copy the blob only if its ETag does not match the value specified. If the values are identical, the Blob service returns status code 412 (Precondition Failed). This header cannot be specified if the source is an Azure File.|  
|`If-Modified-Since`|Optional. A `DateTime` value. Specify this conditional header to copy the blob only if the destination blob has been modified since the specified date/time. If the destination blob has not been modified, the Blob service returns status code 412 (Precondition Failed).|  
|`If-Unmodified-Since`|Optional. A `DateTime` value. Specify this conditional header to copy the blob only if the destination blob has not been modified since the specified date/time. If the destination blob has been modified, the Blob service returns status code 412 (Precondition Failed).|  
|`If-Match`|Optional. An ETag value. Specify an ETag value for this conditional header to copy the blob only if the specified ETag value matches the `ETag` value for an existing destination blob. If the ETag for the destination blob does not match the ETag specified for `If-Match`, the Blob service returns status code 412 (Precondition Failed).|  
|`If-None-Match`|Optional. An ETag value, or the wildcard character (*).<br /><br /> Specify an ETag value for this conditional header to copy the blob only if the specified ETag value does not match the ETag value for the destination blob.<br /><br /> Specify the wildcard character (\*) to perform the operation only if the destination blob does not exist.<br /><br /> If the specified condition isn't met, the Blob service returns status code 412 (Precondition Failed).|  
|`x-ms-copy-source:name`|Required. Specifies the name of the source blob or file.<br /><br /> Beginning with version 2012-02-12, this value may be a URL of up to 2 KB in length that specifies a blob. The value should be URL-encoded as it would appear in a request URI. A source blob in the same storage account can be authenticated via Shared Key. However, if the source is a blob in another account, the source blob must either be public or must be authenticated via a shared access signature. If the source blob is blob is public, no authentication is required to perform the copy operation.<br /><br /> Beginning with version 2015-02-21, the source object may be a file in the Azure File service. If the source object is a file that is to be copied to a blob, then the source file must be authenticated usign a shared access signature, whether it resides in the same account or in a different account.<br /><br /> Only storage accounts created on or after June 7th, 2012 allow the `Copy Blob` operation to copy from another storage account.<br /><br /> Here are some examples of source object URLs:<br /><br /> -   `https://myaccount.blob.core.windows.net/mycontainer/myblob`<br />-   `https://myaccount.blob.core.windows.net/mycontainer/myblob?snapshot=<DateTime>`<br /><br /> When the source object is a file in the Azure File service, the source URL uses the following format; note that the URL must include a valid SAS token for the file:<br /><br /> -   `https://myaccount.file.core.windows.net/myshare/mydirectorypath/myfile?sastoken`<br /><br /> In versions before 2012-02-12, blobs can only be copied within the same account, and a source name can use these formats:<br /><br /> -   Blob in named container: `/accountName/containerName/blobName`<br />-   Snapshot in named container: `/accountName/containerName/blobName?snapshot=<DateTime>`<br />-   Blob in root container: `/accountName/blobName`<br />-   Snapshot in root container: `/accountName/blobName?snapshot=<DateTime>`|  
|`x-ms-lease-id:<ID>`|Required if the destination blob has an active lease. The lease ID specified for this header must match the lease ID of the destination blob. If the request does not include the lease ID or it is not valid, the operation fails with status code 412 (Precondition Failed).<br /><br /> If this header is specified and the destination blob does not currently have an active lease, the operation will also fail with status code 412 (Precondition Failed).<br /><br /> In version 2012-02-12 and newer, this value must specify an active, infinite lease for a leased blob. A finite-duration lease ID fails with 412 (Precondition Failed).|  
|`x-ms-source-lease-id: <ID>`|Optional, versions before 2012-02-12 (unsupported in 2012-02-12 and newer). Specify this header to perform the `Copy Blob` operation only if the lease ID given matches the active lease ID of the source blob.<br /><br /> If this header is specified and the source blob does not currently have an active lease, the operation will also fail with status code 412 (Precondition Failed).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
### Request Body  
 None.  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 In version 2012-02-12 and newer, a successful operation returns status code 202 (Accepted).  
  
 In versions before 2012-02-12, a successful operation returns status code 201 (Created).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`ETag`|In version 2012-02-12 and newer, if the copy is complete, contains the ETag of the destination blob. If the copy isn’t complete, contains the ETag of the empty blob created at the start of the copy.<br /><br /> In versions before 2012-02-12, returns the ETag for the destination blob.<br /><br /> In version 2011-08-18 and newer, the ETag value will be in quotes.|  
|`Last-Modified`|Returns the date/time that the copy operation to the destination blob completed.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Blob service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
|`x-ms-copy-id: <id>`|Version 2012-02-12 and newer. String identifier for this copy operation. Use with `Get Blob` or `Get Blob Properties` to check the status of this copy operation, or pass to `Abort Copy Blob` to abort a pending copy.|  
|`x-ms-copy-status: <success &#124; pending>`|Version 2012-02-12 and newer. State of the copy operation, with these values:<br /><br /> -   `success`: the copy completed successfully.<br />-   `pending`: the copy is in progress.|  
  
## Response Body  
 None.  
  
## Sample Response  
 The following is a sample response for a request to copy a blob:  
  
```  
Response Status:  
HTTP/1.1 202 Accepted  
  
Response Headers:   
Last-Modified: <date>   
ETag: "0x8CEB669D794AFE2"  
Server: Windows-Azure-Blob/1.0 Microsoft-HTTPAPI/2.0  
x-ms-request-id: cc6b209a-b593-4be1-a38a-dde7c106f402  
x-ms-version: 2015-02-21  
x-ms-copy-id: 1f812371-a41d-49e6-b123-f4b542e851c5  
x-ms-copy-status: pending  
Date: <date>  
  
```  
  
## Authorization  
 This operation can be called by the account owner. For requests made against version 2013-08-15 and later, a shared access signature that has permission to write to the destination blob or its container is supported for copy operations within the same account. Note that the shared access signature specified on the request applies only to the destination blob.  
  
 Access to the source blob or file is authorized separately, as described in the details for the request header `x-ms-copy-source`.  
  
 The following table describes how the destination and source objects for a [Copy Blob](assetId:///Copy Blob?qualifyHint=False&autoUpgrade=True) operation may be authenticated.  
  
||Authentication with Shared Key/Shared Key Lite|Authentication with Shared Access Signature|Public Object Not Requiring Authentication|  
|-|-----------------------------------------------------|-------------------------------------------------|------------------------------------------------|  
|Destination blob|Yes|Yes|No|  
|Source blob in same account|Yes|Yes|Yes|  
|Source blob in another account|No|Yes|Yes|  
|Source file in the same account or another account|No|Yes|N/A|  
  
## Remarks  
 In version 2012-02-12 and newer, the `Copy Blob` operation can complete asynchronously. This operation returns a copy ID you can use to check or abort the copy operation. The Blob service copies blobs on a best-effort basis.  
  
 The source blob for a copy operation may be a block blob, an append blob, or a page blob, or a snapshot. If the destination blob already exists, it must be of the same blob type as the source blob. Any existing destination blob will be overwritten. The destination blob cannot be modified while a copy operation is in progress.  
  
 In version 2015-02-21 and newer, the source for the copy operation may also be a file in the Azure File service. If the source is a file, the destination must be a block blob.  
  
 Multiple pending `Copy Blob` operations within an account might be processed sequentially. A destination blob can only have one outstanding copy blob operation. In other words, a blob cannot be the destination for multiple pending `Copy Blob` operations. An attempt to `Copy Blob` to a destination blob that already has a copy pending fails with status code 409 (Conflict).  
  
 Only storage accounts created on or after June 7th, 2012 allow the `Copy Blob` operation to copy from another storage account. An attempt to copy from another storage account to an account created before June 7th, 2012 fails with status code 400 (Bad Request).  
  
 The `Copy Blob` operation always copies the entire source blob or file; copying a range of bytes or set of blocks is not supported.  
  
 A `Copy Blob` operation can take any of the following forms:  
  
-   You can copy a source blob to a destination blob with a different name. The destination blob can be an existing blob of the same blob type (block, append, or page), or can be a new blob created by the copy operation.  
  
-   You can copy a source blob to a destination blob with the same name, effectively replacing the destination blob. Such a copy operation removes any uncommitted blocks and overwrites the blob's metadata.  
  
-   You can copy a source file in the Azure File service to a destination blob. The destination blob can be an existing block blob, or can be a new block blob created by the copy operation. Copying from files to page blobs or append blobs is not supported.  
  
-   You can copy a snapshot over its base blob. By promoting a snapshot to the position of the base blob, you can restore an earlier version of a blob.  
  
-   You can copy a snapshot to a destination blob with a different name. The resulting destination blob is a writeable blob and not a snapshot.  
  
 When copying from a page blob, the Blob service creates a destination page blob of the source blob’s length, initially containing all zeroes. Then the source page ranges are enumerated, and non-empty ranges are copied.  
  
 For a block blob or an append blob, the Blob service creates a committed blob of zero length before returning from this operation.  
  
 When copying from a block blob, all committed blocks and their block IDs are copied. Uncommitted blocks are not copied. At the end of the copy operation, the destination blob will have the same committed block count as the source.  
  
 When copying from an append blob, all committed blocks are copied. At the end of the copy operation, the destination blob will have the same committed block count as the source.  
  
 For all blob types, you can call `Get Blob` or `Get Blob Properties` on the destination blob to check the status of the copy operation. The final blob will be committed when the copy completes.  
  
 When the source of a copy operation provides ETags, if there are any changes to the source while the copy is in progress, the copy will fail. An attempt to change the destination blob while a copy is in progress will fail with 409 Conflict. If the destination blob has an infinite lease, the lease ID must be passed to `Copy Blob`. Finite-duration leases are not allowed.  
  
 The ETag for a block blob changes when the `Copy Blob` operation is initiated and when the copy finishes.  The ETag for a page blob changes when the `Copy Blob` operation is initiated, and continues to change frequently during the copy. The contents of a block blob are only visible using a GET after the full copy completes.  
  
 **Copying Blob Properties and Metadata**  
  
 When a blob is copied, the following system properties are copied to the destination blob with the same values:  
  
-   `Content-Type`  
  
-   `Content-Encoding`  
  
-   `Content-Language`  
  
-   `Content-Length`  
  
-   `Cache-Control`  
  
-   `Content-MD5`  
  
-   `Content-Disposition`  
  
-   `x-ms-blob-sequence-number (for page blobs only)`  
  
-   `x-ms- committed-block-count (for append blobs only, and for version 2015-02-21 only)`  
  
 The source blob's committed block list is also copied to the destination blob, if the blob is a block blob. Any uncommitted blocks are not copied.  
  
 The destination blob is always the same size as the source blob, so the value of the `Content-Length` header for the destination blob matches that for the source blob.  
  
 When the source blob and destination blob are the same, `Copy Blob` removes any uncommitted blocks. If metadata is specified in this case, the existing metadata is overwritten with the new metadata.  
  
 **Copying a Leased Blob**  
  
 The `Copy Blob` operation only reads from the source blob so the lease state of the source blob does not matter. However, the `Copy Blob` operation saves the ETag of the source blob when the copy is initiated. If the ETag value changes before the copy completes, the copy fails. You can prevent changes to the source blob by leasing it during the copy operation.  
  
 If the destination blob has an active infinite lease, you must specify its lease ID in the call to the `Copy Blob` operation. If the lease you specify is an active finite-duration lease, this call fails with a status code 412 (Precondition Failed). While the copy is pending, any lease operation on the destination blob will fail with status code 409 (Conflict).  An infinite lease on the destination blob is locked in this way during the copy operation whether you are copying to a destination blob with a different name from the source, copying to a destination blob with the same name as the source, or promoting a snapshot over its base blob. If the client specifies a lease ID on a blob that does not yet exist, the Blob service will return status code 412 (Precondition Failed) for requests made against version 2013-08-15 and later; for prior versions the Blob service will return status code 201 (Created).  
  
 **Copying Snapshots**  
  
 When a source blob is copied, any snapshots of the source blob are not copied to the destination. When a destination blob is overwritten with a copy, any snapshots associated with the destination blob stay intact under its name.  
  
 You can perform a copy operation to promote a snapshot blob over its base blob. In this way you can restore an earlier version of a blob. The snapshot remains, but its destination is overwritten with a copy that can be both read and written.  
  
 **Working with a Pending Copy (version 2012-02-12 and newer)**  
  
 The `Copy Blob` operation completes the copy asynchronously. Use the following table to determine the next step based on the status code returned by `Copy Blob`:  
  
|Status Code|Meaning|  
|-----------------|-------------|  
|202 (Accepted), x-ms-copy-status: success|Copy completed successfully.|  
|202 (Accepted), x-ms-copy-status: pending|Copy has not completed. Poll the destination blob using `Get Blob Properties` to examine the x-ms-copy-status until copy completes or fails.|  
|4xx, 500, or 503|Copy failed.|  
  
 During and after a `Copy Blob` operation, the properties of the destination blob contain the copy ID of the `Copy Blob` operation and URL of the source blob. When the copy completes, the Blob service writes the time and outcome value (`success`, `failed`, or `aborted`) to the destination blob properties. If the operation `failed`, the `x-ms-copy-status-description` header contains an error detail string.  
  
 A pending `Copy Blob` operation has a 2 week timeout. A copy attempt that has not completed after 2 weeks times out and leaves an empty blob with the `x-ms-copy-status` field set to `failed` and the `x-ms-copy-status-description` set to 500 (OperationCancelled). Intermittent, non-fatal errors that can occur during a copy might impede progress of the copy but not cause it to fail. In these cases, `x-ms-copy-status-description` describes the intermittent errors.  
  
 Any attempt to modify or snapshot the destination blob during the copy will fail with **409 (Conflict) Copy Blob in Progress**.  
  
 If you call the `Abort Copy Blob` operation, you will see a `x-ms-copy-status:aborted` header and the destination blob will have intact metadata and a blob length of zero bytes. You can repeat the original call to `Copy Blob` to try the copy again.  
  
 **Billing**  
  
 The destination account of a `Copy Blob` operation is charged for one transaction to initiate the copy, and also incurs one transaction for each request to abort or request the status of the copy operation.  
  
 When the source blob is in another account, the source account incurs transaction costs. In addition, if the source and destination accounts reside in different regions (e.g., US North and US South), bandwidth used to transfer the request is charged to the source storage account as egress. Egress between accounts within the same region is free.  
  
 When you copy a source blob to a destination blob with a different name within the same account, you use additional storage resources for the new blob, so the copy operation results in a charge against the storage account’s capacity usage for those additional resources. However, if the source and destination blob name are the same within the same account (for example, when you promote a snapshot to its base blob), no additional charge is incurred other than the extra copy metadata stored in version 2012-02-12 and newer.  
  
 When you promote a snapshot to replace its base blob, the snapshot and base blob become identical. They share blocks or pages, so the copy operation does not result in an additional charge against the storage account's capacity usage. However, if you copy a snapshot to a destination blob with a different name, an additional charge is incurred for the storage resources used by the new blob that results. Two blobs with different names cannot share blocks or pages even if they are identical. For more information about snapshot cost scenarios, see [Understanding How Snapshots Accrue Charges](../StorageServicesREST/Understanding-How-Snapshots-Accrue-Charges.md).  
  
## See Also  
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Blob Service Error Codes](../StorageServicesREST/Blob-Service-Error-Codes.md)   
 [Understanding How Snapshots Accrue Charges](../StorageServicesREST/Understanding-How-Snapshots-Accrue-Charges.md)   
 [Abort Copy Blob](../StorageServicesREST/Abort-Copy-Blob.md)
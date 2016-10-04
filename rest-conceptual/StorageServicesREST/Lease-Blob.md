---
title: "Lease Blob"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 68b74877-5678-46c1-bdbf-f6a68a73f75b
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
# Lease Blob
The `Lease Blob` operation establishes and manages a lock on a blob for write and delete operations. The lock duration can be 15 to 60 seconds, or can be infinite. In versions prior to 2012-02-12, the lock duration is 60 seconds.  
  
> [!IMPORTANT]
>  Starting in version 2012-02-12, some behaviors of the `Lease Blob` operation differ from previous versions. For example, in previous versions of the `Lease Blob` operation you could renew a lease after releasing it. Starting in version 2012-02-12, this lease request will fail, while calls using older versions of `Lease Blob` still succeed. See the `Changes to Lease Blob introduced in version 2012-02-12` section under `Remarks` for a list of changes to the behavior of this operation.  
  
 The `Lease Blob` operation can be called in one of five modes:  
  
-   `Acquire`, to request a new lease.  
  
-   `Renew`, to renew an existing lease.  
  
-   `Change`, to change the ID of an existing lease.  
  
-   `Release`, to free the lease if it is no longer needed so that another client may immediately acquire a lease against the blob.  
  
-   `Break`, to end the lease but ensure that another client cannot acquire a new lease until the current lease period has expired.  
  
## Request  
 The `Lease Blob` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
||PUT Method Request URI|HTTP Version|  
|-|----------------------------|------------------|  
||`https://myaccount.blob.core.windows.net/mycontainer/myblob?comp=lease`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Blob service port as `127.0.0.1:10000`, followed by the emulated storage account name:  
  
||PUT Method Request URI|HTTP Version|  
|-|----------------------------|------------------|  
||`http://127.0.0.1:10000/devstoreaccount1/mycontainer/myblob?comp=lease`|HTTP/1.0<br /><br /> HTTP/1.1|  
  
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
|`x-ms-version`|Optional. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-lease-id: <ID>`|Required to renew, change, or release the lease.<br /><br /> The value of x-ms-lease-id can be specified in any valid GUID string format. See [Guid Constructor (String)](http://msdn.microsoft.com/en-us/library/96ff78dc.aspx) for a list of valid GUID string formats.|  
|`x-ms-lease-action: <acquire &#124; renew &#124; change &#124; release &#124; break>`|`acquire`: Requests a new lease. If the blob does not have an active lease, the Blob service creates a lease on the blob and returns a new lease ID.  If the blob has an active lease, you can only request a new lease using the active lease ID, but you can specify a new `x-ms-lease-duration`, including negative one (-1) for a lease that never expires.<br /><br /> `renew`: Renews the lease. The lease can be renewed if the lease ID specified on the request matches that associated with the blob. Note that the lease may be renewed even if it has expired as long as the blob has not been modified or leased again since the expiration of that lease. When you renew a lease, the lease duration clock resets.<br /><br /> `change`: Version 2012-02-12 and newer. Changes the lease ID of an active lease. A `change` must include the current lease ID in x-ms-lease-id and a new lease ID in x-ms-proposed-lease-id.<br /><br /> `release`: Releases the lease. The lease may be released if the lease ID specified on the request matches that associated with the blob. Releasing the lease allows another client to immediately acquire the lease for the blob as soon as the release is complete.<br /><br /> `break`: Breaks the lease, if the blob has an active lease. Once a lease is broken, it cannot be renewed. Any authorized request can break the lease; the request is not required to specify a matching lease ID. When a lease is broken, the lease break period is allowed to elapse, during which time no lease operation except `break` and `release` can be performed on the blob. When a lease is successfully broken, the response indicates the interval in seconds until a new lease can be acquired.<br /><br /> A lease that has been broken can also be released, in which case another client may immediately acquire the lease on the blob.|  
|`x-ms-lease-break-period: N`|Version 2012-02-12 and newer, optional. For a `break` operation, this is the proposed duration of seconds that the lease should continue before it is broken, between 0 and 60 seconds. This break period is only used if it is shorter than the time remaining on the lease. If longer, the time remaining on the lease is used. A new lease will not be available before the break period has expired, but the lease may be held for longer than the break period. If this header does not appear with a `break` operation, a fixed-duration lease breaks after the remaining lease period elapses, and an infinite lease breaks immediately.|  
|`x-ms-lease-duration: -1 &#124; N`|Version 2012-02-12 and newer, only allowed and required on an `acquire` operation. Specifies the duration of the lease, in seconds, or negative one (-1) for a lease that never expires.  A non-infinite lease can be between 15 and 60 seconds. A lease duration cannot be changed using `renew` or `change`.|  
|`x-ms-proposed-lease-id: <ID>`|Version 2012-02-12 and newer, optional for `acquire`, required for `change`. Proposed lease ID, in a GUID string format. The Blob service returns `400 (Invalid request)` if the proposed lease ID is not in the correct format. See [Guid Constructor (String)](http://msdn.microsoft.com/library/96ff78dc.aspx) for a list of valid GUID string formats.|  
|`Origin`|Optional. Specifies the origin from which the request is issued. The presence of this header results in cross-origin resource sharing headers on the response. See [CORS Support for the Storage Services](../StorageServicesREST/Cross-Origin-Resource-Sharing--CORS--Support-for-the-Azure-Storage-Services.md) for details.|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
 This operation also supports the use of conditional headers to execute the operation only if a specified condition is met. For more information, see [Specifying Conditional Headers for Blob Service Operations](../StorageServicesREST/Specifying-Conditional-Headers-for-Blob-Service-Operations.md).  
  
### Request Body  
 None.  
  
### Sample Request  
 The following sample request shows how to acquire a lease:  
  
```  
  
Request Syntax:  
PUT https://myaccount.blob.core.windows.net/mycontainer/myblob?comp=lease HTTP/1.1  
  
Request Headers:  
x-ms-version: 2015-02-21  
x-ms-lease-action: acquire  
x-ms-lease-duration: -1  
x-ms-proposed-lease-id: 1f812371-a41d-49e6-b123-f4b542e851c5  
x-ms-date: <date>  
Authorization: SharedKey testaccount1:esSKMOYdK4o+nGTuTyeOLBI+xqnqi6aBmiW4XI699+o=  
  
```  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 The success status codes returned for lease operations are the following:  
  
-   `Acquire`: A successful operation returns status code 201 (Created).  
  
-   `Renew`: A successful operation returns status code 200 (OK).  
  
-   `Change`: A successful operation returns status code 200 (OK).  
  
-   `Release`: A successful operation returns status code 200 (OK).  
  
-   `Break`: A successful operation returns status code 202 (Accepted).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Syntax|Description|  
|------------|-----------------|  
|`ETag`|The `ETag` header contains a value that you can use to perform operations conditionally. See [Specifying Conditional Headers for Blob Service Operations](../StorageServicesREST/Specifying-Conditional-Headers-for-Blob-Service-Operations.md) for more information.<br /><br /> This header is returned for requests made against version 2013-08-15 and later, and the ETag value will be in quotes.<br /><br /> The `Lease Blob` operation does not modify this property.|  
|`Last-Modified`|The date/time that the blob was last modified. The date format follows RFC 1123. For more information, see [Representation of Date-Time Values in Headers](../StorageServicesREST/Representation-of-Date-Time-Values-in-Headers.md).<br /><br /> Any write operation on the blob, including updates on the blob's metadata or properties, changes the last-modified time of the blob. The `Lease Blob` operation does not modify this property.|  
|`x-ms-lease-id: <id>`|When you request a lease, the Blob service returns a unique lease ID. While the lease is active, you must include the lease ID with any request to write to the blob, or to renew, change, or release the lease.<br /><br /> A successful renew operation also returns the lease ID for the active lease.|  
|`x-ms-lease-time: seconds`|Approximate time remaining in the lease period, in seconds. This header is returned only for a successful request to break the lease. If the break is immediate, 0 is returned.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Blob service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.|  
|Date|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
|`Access-Control-Allow-Origin`|Returned if the request includes an `Origin` header and CORS is enabled with a matching rule. This header returns the value of the origin request header in case of a match.|  
|`Access-Control-Expose-Headers`|Returned if the request includes an `Origin` header and CORS is enabled with a matching rule. Returns the list of response headers that are to be exposed to the client or issuer of the request.|  
|`Access-Control-Allow-Credentials`|Returned if the request includes an `Origin` header and CORS is enabled with a matching rule that does not allow all origins. This header will be set to true.|  
  
### Response Body  
 None.  
  
### Sample Response  
 The following is a sample response for a request to acquire a lease:  
  
```  
Response Status:  
HTTP/1.1 201 Created  
  
Response Headers:  
Server: Windows-Azure-Blob/1.0 Microsoft-HTTPAPI/2.0  
x-ms-request-id: cc6b209a-b593-4be1-a38a-dde7c106f402  
x-ms-version: 2015-02-21  
x-ms-lease-id: 1f812371-a41d-49e6-b123-f4b542e851c5  
Date: <date>  
  
```  
  
## Authorization  
 This operation can be called by the account owner and by any client with a shared access signature that has permission to write to this blob or its container.  
  
## Remarks  
 A lease on a blob provides exclusive write and delete access to the blob. To write to a blob with an active lease, a client must include the active lease ID with the write request. The lease is granted for the duration specified when the lease is acquired, which can be between 15 seconds and one minute, or an infinite duration.  
  
 When a client acquires a lease, a lease ID is returned. The Blob service will generate a lease ID if one is not specified in the acquire request. The client may use this lease ID to renew the lease, change its lease ID, or release the lease.  
  
 When a lease is active, the lease ID must be included in the request for any of the following operations:  
  
-   [Put Blob](../StorageServicesREST/Put-Blob.md)  
  
-   [Set Blob Metadata](../StorageServicesREST/Set-Blob-Metadata.md)  
  
-   [Set Blob Properties](../StorageServicesREST/Set-Blob-Properties.md)  
  
-   [Delete Blob](../StorageServicesREST/Delete-Blob.md)  
  
-   [Put Block](../StorageServicesREST/Put-Block.md)  
  
-   [Put Block List](../StorageServicesREST/Put-Block-List.md)  
  
-   [Put Page](../StorageServicesREST/Put-Page.md)  
  
-   [Append Block](../StorageServicesREST/Append-Block.md)  
  
-   [Copy Blob](../StorageServicesREST/Copy-Blob.md) (lease ID needed for destination blob)  
  
 If the lease ID is not included, these operations will fail on a leased blob with `412 – Precondition failed`.  
  
 The following operations succeed on a leased blob without including the lease ID:  
  
-   [Get Blob](../StorageServicesREST/Get-Blob.md)  
  
-   [Get Blob Metadata](../StorageServicesREST/Get-Blob-Metadata.md)  
  
-   [Get Blob Properties](../StorageServicesREST/Get-Blob-Properties.md)  
  
-   [Get Block List](../StorageServicesREST/Get-Block-List.md)  
  
-   [Get Page Ranges](../StorageServicesREST/Get-Page-Ranges.md)  
  
-   [List Blobs](../StorageServicesREST/List-Blobs.md)  
  
-   [Copy Blob](../StorageServicesREST/Copy-Blob.md) (No lease ID needed for source blob.)  
  
-   [Lease Blob (REST API)](../StorageServicesREST/Lease-Blob.md) (No lease ID needed for `x-ms-lease-action: break`.)  
  
 It's not necessary to include the lease ID for GET operations on a blob that has an active lease. However, all GET operations support a conditional lease parameter, where the operation only proceeds if the lease ID included with the request is valid.  
  
 All container operations are permitted on a container that includes blobs with an active lease, including [Delete Container](../StorageServicesREST/Delete-Container.md). Therefore a container may be deleted even if blobs within it have active leases. Use the [Lease Container](../StorageServicesREST/Lease-Container.md) operation to control rights to delete a container.  
  
 The following diagram shows the five states of a lease, and the commands or events that cause lease state changes.  
  
 ![Blob lease states and state change triggers](../StorageServicesREST/media/BlobLeaseStates.png "BlobLeaseStates")  
  
 **Lease States**  
  
 A lease can be in 5 states, based on whether the lease is locked or unlocked, and whether the lease is renewable in that state. The lease actions above cause state transitions.  
  
||Locked Lease|Unlocked Lease|  
|-|------------------|--------------------|  
|**Renewable Lease**|Leased|Expired|  
|**Non-renewable Lease**|Breaking|Broken, Available|  
  
-   `Available`, the lease is unlocked and can be acquired. Allowed action: `acquire`.  
  
-   `Leased`, the lease is locked. Allowed actions: `acquire` (same lease ID only), `renew`, `change`, `release`, and `break`.  
  
-   `Expired`, the lease duration has expired. Allowed actions: `acquire`, `renew`, `release`, and `break`.  
  
-   `Breaking`, lease has been broken, but the lease will continue to be locked until the break period has expired. Allowed actions: `release` and `break`.  
  
-   `Broken`, lease has been broken, and the break period has expired. Allowed actions: `acquire`, `release`, and `break`.  
  
 Once a lease has expired, the lease ID is maintained by the Blob service until the blob is modified or leased again. A client may attempt to renew or release their lease using their expired lease ID and know that if the operation is successful, the blob has not been changed since the lease ID was last valid.  
  
 If the client attempts to renew or release a lease with their previous lease ID and the request fails, the client then knows that the blob was modified or leased again since their lease was last active. The client must then acquire a new lease on the blob.  
  
 If a lease expires rather than being explicitly released, a client may need to wait up to one minute before a new lease can be acquired for the blob. However, the client can renew the lease with their lease ID immediately if the blob has not been modified.  
  
 Note that a lease cannot be granted for a blob snapshot, since snapshots are read-only. Requesting a lease against a snapshot results in status code 400 (Bad Request).  
  
 The blob's `Last-Modified-Time` property is not updated by calls to `Lease Blob`.  
  
 The following tables show outcomes of actions on blobs with leases in various lease states. Letters (A), (B), and (C) represent lease IDs, and (X) represents a lease ID generated by the Blob service.  
  
### Outcomes of use attempts on blobs by lease state  
  
||Available|Leased (A)|Breaking (A)|Broken (A)|Expired (A)|  
|-|---------------|------------------|--------------------|------------------|-------------------|  
|Write using (A)|Fails (412)|Leased (A), write succeeds|Breaking (A), write succeeds|Fails (412)|Fails (412)|  
|Write using (B)|Fails (412)|Fails (409)|Fails (412)|Fails (412)|Fails (412)|  
|Write, no lease specified|Available, write succeeds|Fails (412)|Fails (412)|Available, write succeeds|Available, write succeeds|  
|Read using (A)|Fails (412)|Leased (A), read succeeds|Breaking (A), read succeeds|Fails (412)|Fails (412)|  
|Read using (B)|Fails (412)|Fails (409)|Fails (409)|Fails (412)|Fails (412)|  
o lease specified|Available, read succeeds|Leased (A), read succeeds|Breaking (A), read succeeds|Broken (A), read succeeds|Expired (A), read succeeds|  
  
### Outcomes of lease operations on blobs by lease state  
  
||Available|Leased (A)|Breaking (A)|Broken (A)|Expired (A)|  
|-|---------------|------------------|--------------------|------------------|-------------------|  
|`Acquire`, no proposed lease ID|Leased (X)|Fails (409)|Fails (409)|Leased (X)|Leased (X)|  
|`Acquire` (A)|Leased (A)|Leased (A), new duration|Fails (409)|Leased (A)|Leased (A)|  
|`Acquire` (B)|Leased (B)|Fails (409)|Fails (409)|Leased (B)|Leased (B)|  
|`Break`, period=0|Fails (409)|Broken (A)|Broken (A)|Broken (A)|Broken (A)|  
|`Break`, period>0|Fails (409)|Breaking (A)|Breaking (A)|Broken (A)|Broken (A)|  
`, (A) to (B)|Fails (409)|Leased (B)|Fails (409)|Fails (409)|Fails (409)|  
|`Change`, (B) to (A)|Fails (409)|Leased (A)|Fails (409)|Fails (409)|Fails (409)|  
|`Change`, (B) to (C)|Fails (409)|Fails (409)|Fails (409)|Fails (409)|Fails (409)|  
|`Renew` (A)|Fails (409)|Leased (A), expiration clock reset|Fails (409)|Fails (409)|Leased(A), if blob has not been modified.<br /><br /> Fails (409) if blob has been modified.|  
 (B)|Fails (409)|Fails (409)|Fails (409)|Fails (409)|Fails (409)|  
|`Release` (A)|Fails (409)|Available|Available|Available|Available|  
|`Release` (B)|Fails (409)|Fails (409)|Fails (409)|Fails (409)|Fails (409)|  
|Duration expires|Available|Expired (A)|Broken (A)|Broken (A)|Expired (A)|  
  
 `Changes to Lease Blob introduced in version 2012-02-12`  
  
 The following list specifies changes to Lease Blob behavior introduced in version 2012-02-12.  
  
-   A call to Lease Blob to acquire a lease now must include a lease duration header. Trying to acquire a lease without specifying a lease duration will fail with `400 Bad Request – Missing required header`.  
  
-   You can no longer renew a lease after releasing it. Trying to do so will fail with `409 Conflict – The lease ID specified did not match the lease ID for the blob`. Applications that called release and then called renew must now save the ETag from the release call and then call acquire with an `If-Match` conditional header to only acquire the lease when the blob is unchanged.  
  
-   You can no longer break a lease after releasing it.  Attempting to do this will now fail with `409 Conflict – There is currently no lease on the blob`.  
  
-   You can now break a breaking or broken lease, making break operations idempotent. In previous versions, this failed with `409 Conflict – The lease has already been broken and cannot be broken again`. This change allows you to shorten the duration of a break. If you break a lease that is in breaking state and include a shorter duration than the remaining break period, your shorter duration is used.  
  
## See Also  
 [New Blob Lease Features: Infinite Leases, Smaller Lease Times, and More](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/new-blob-lease-features-infinite-leases-smaller-lease-times-and-more.aspx)   
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Blob Service Error Codes](../StorageServicesREST/Blob-Service-Error-Codes.md)   
 [Lease Container](../StorageServicesREST/Lease-Container.md)
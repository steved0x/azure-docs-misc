---
title: "Lease Container"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: ce8d6a62-dbc9-475c-acb4-666a5a9370c8
caps.latest.revision: 27
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
# Lease Container
The `Lease Container` operation establishes and manages a lock on a container for delete operations. The lock duration can be 15 to 60 seconds, or can be infinite.  
  
 The `Lease Container` operation can be called in one of five modes:  
  
-   `Acquire`, to request a new lease.  
  
-   `Renew`, to renew an existing lease.  
  
-   `Change`, to change the ID of an existing lease.  
  
-   `Release`, to free the lease if it is no longer needed so that another client may immediately acquire a lease against the container.  
  
-   `Break`, to end the lease but ensure that another client cannot acquire a new lease until the current lease period has expired.  
  
> [!NOTE]
>  The `Lease Container` operation is available in version 2012-02-12 and newer.  
  
## Request  
 The `Lease Container` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`PUT`|`https://myaccount.blob.core.windows.net/mycontainer?comp=lease&restype=container`|HTTP/1.1|  
  
 To specify the root container, enter `$root` as the container name.  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Blob service port as `127.0.0.1:10000`, followed by the emulated storage account name:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`PUT`|`http://127.0.0.1:10000/mycontainer?comp=lease&restype=container`|HTTP/1.0<br /><br /> HTTP/1.1|  
  
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
|`x-ms-lease-id: <ID>`|Required to renew, change, or release the lease.<br /><br /> The value of `x-ms-lease-id` can be specified in any valid GUID string format. See [Guid Constructor (String)](http://msdn.microsoft.com/library/96ff78dc.aspx) for a list of valid GUID string formats.|  
|`x-ms-lease-action: <acquire &#124; renew &#124; change &#124; release &#124; break>`|`acquire`: Requests a new lease. If the container does not have an active lease, the Blob service creates a lease on the container and returns a new lease ID.  If the container has an active lease, you can only request a new lease using the active lease ID, but you can specify a new `x-ms-lease duration`, including negative one (-1) for a lease that never expires.<br /><br /> `renew`: Renews the lease. The lease can be renewed if the lease ID specified on the request matches that associated with the container. Note that the lease may be renewed even if it has expired as long as the container has not been leased again since the expiration of that lease. When you renew a lease, the lease duration clock resets.<br /><br /> `change`: Change the lease ID of an active lease. A `change` must include the current lease ID in x-ms-lease-id and a new lease ID in x-ms-proposed-lease-id.<br /><br /> `release`: Release the lease. The lease may be released if the lease ID specified on the request matches that associated with the container. Releasing the lease allows another client to immediately acquire the lease for the container as soon as the release is complete.<br /><br /> `break`: Break the lease, if the container has an active lease. Once a lease is broken, it cannot be renewed. Any authorized request can break the lease; the request is not required to specify a matching lease ID. When a lease is broken, the lease break period is allowed to elapse, during which time no lease operation except `break` and `release` can be performed on the container. When a lease is successfully broken, the response indicates the interval in seconds until a new lease can be acquired.<br /><br /> A lease that has been broken can also be released. A client can immediately acquire a container lease that has been released.|  
|`x-ms-lease-break-period: N`|Optional. For a `break` operation, proposed duration the lease should continue before it is broken, in seconds, between 0 and 60. This break period is only used if it is shorter than the time remaining on the lease. If longer, the time remaining on the lease is used. A new lease will not be available before the break period has expired, but the lease may be held for longer than the break period. If this header does not appear with a `break` operation, a fixed-duration lease breaks after the remaining lease period elapses, and an infinite lease breaks immediately.|  
|`x-ms-lease-duration: -1 &#124; N`|Required for `acquire`. Specifies the duration of the lease, in seconds, or negative one (-1) for a lease that never expires.  A non-infinite lease can be between 15 and 60 seconds. A lease duration cannot be changed using `renew` or `change`.|  
|`x-ms-proposed-lease-id: <ID>`|Optional for `acquire`, required for `change`. Proposed lease ID, in a GUID string format. The Blob service returns `400 (Invalid request)` if the proposed lease ID is not in the correct format. See [Guid Constructor (String)](http://msdn.microsoft.com/library/96ff78dc.aspx) for a list of valid GUID string formats.|  
|`Origin`|Optional. Specifies the origin from which the request is issued. The presence of this header results in cross-origin resource sharing headers on the response. See [CORS Support for the Storage Services](../StorageServicesREST/Cross-Origin-Resource-Sharing--CORS--Support-for-the-Azure-Storage-Services.md) for details.|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
 This operation also supports the use of conditional headers to execute the operation only if a specified condition is met. For more information, see [Specifying Conditional Headers for Blob Service Operations](../StorageServicesREST/Specifying-Conditional-Headers-for-Blob-Service-Operations.md).  
  
### Request Body  
 None.  
  
### Sample Request  
 The following sample request shows how to acquire a lease:  
  
```  
  
Request Syntax:  
PUT https://myaccount.blob.core.windows.net/mycontainer?restype=container&comp=lease HTTP/1.1  
  
Request Headers:  
x-ms-version: 2012-02-12  
x-ms-lease-action: acquire  
x-ms-lease-duration: -1  
x-ms-proposed-lease-id: 1f812371-a41d-49e6-b123-f4b542e851c5  
x-ms-date: Thu, 26 Jan 2012 23:30:18 GMT  
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
|`ETag`|The ETag for the container. This header is returned for requests made against version 2013-08-15 and later, and the ETag value will be in quotes. `Lease Container` operations made against version 2013-08-15 and later do not modify this property, but prior versions will.|  
|`Last-Modified`|This header is returned for requests made against version 2013-08-15 and later. Returns the date and time the container was last modified. The date format follows RFC 1123. For more information, see [Representation of Date-Time Values in Headers](../StorageServicesREST/Representation-of-Date-Time-Values-in-Headers.md).<br /><br /> Any operation that modifies the container or its properties or metadata updates the last-modified time, including setting the container's permissions. Operations on blobs do not affect the last-modified time of the container. `Lease Container` operations made against version 2013-08-15 and later do not modify this property, but prior versions do.|  
|`x-ms-lease-id: <id>`|When you request a lease, the Blob service returns a unique lease ID. While the lease is active, you must include the lease ID with any request to delete the container, or to renew, change, or release the lease.<br /><br /> A successful renew operation also returns the lease ID for the active lease.|  
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
x-ms-version: 2012-02-12  
x-ms-lease-id: 1f812371-a41d-49e6-b123-f4b542e851c5  
Date: Thu, 26 Jan 2012 23:30:18 GMT  
  
```  
  
## Authorization  
 Only the account owner may call this operation.  
  
## Remarks  
 A lease on a container provides exclusive delete access to the container. A container lease only controls the ability to delete the container using the [Delete Container](../StorageServicesREST/Delete-Container.md) operation. To delete a container with an active lease, a client must include the active lease ID with the delete request. If the lease ID is not included, the operation fails with 412 (Precondition failed). All other container operations succeed on a leased container without including the lease ID. The lease is granted for the duration specified when the lease is acquired, which can be between 15 seconds and one minute, or an infinite duration.  
  
 When a client acquires a lease, a lease ID is returned. The Blob service will generate a lease ID if one is not specified in the acquire request. The client may use this lease ID to renew the lease, change its lease ID, or release the lease. The following diagram shows the five states of a lease, and the commands or events that cause lease state changes.  
  
 The following diagram shows the five states of a lease, and the commands or events that cause lease state changes.  
  
 ![Container lease states and state change triggers](../StorageServicesREST/media/ContainerLeaseStates.png "ContainerLeaseStates")  
  
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
  
 The lease ID is maintained by the Blob service after a container lease has expired. A client can renew or release their lease using their expired lease ID. If the client attempts to renew or release an expired lease with their previous lease ID and the request fails, the client then knows that the container was leased again or deleted since their lease was last active. If a lease expires rather than being explicitly released, a client may need to wait up to one minute before a new lease can be acquired for the container. However, the client can renew the lease with the expired lease ID immediately.  
  
 The container's `Last-Modified-Time` property is not updated by calls to `Lease Container`.  
  
 The following tables show outcomes of actions on containers with leases in various lease states. Letters (A), (B), and (C) represent lease IDs, and (X) represents a lease ID generated by the Blob service.  
  
### Outcomes of use attempts on containers by lease state  
  
||Available|Leased (A)|Breaking (A)|Broken (A)|Expired (A)|  
|-|---------------|------------------|--------------------|------------------|-------------------|  
|Delete using (A)|Fails (412)|Leased (A), delete succeeds|Breaking (A), delete succeeds|Fails (412)|Fails (412)|  
|Delete using (B)|Fails (412)|Fails (409)|Fails (412)|Fails (412)|Fails (412)|  
|Delete, no lease specified|Available, delete succeeds|Fails (412)|Fails (412)|Available, delete succeeds|Available, delete succeeds|  
|Other operations using (A)|Fails (412)|Leased (A), operation succeeds|Breaking (A), operation succeeds|Fails (412)|Fails (412)|  
|Other operations using (B)|Fails (412)|Fails (409)|Fails (409)|Fails (412)|Fails (412)|  
perations, no lease specified|Available, operation succeeds|Leased (A), operation succeeds|Breaking (A), operation succeeds|Broken (A), operation succeeds|Expired (A), operation succeeds|  
  
### Outcomes of lease operations on containers by lease state  
  
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
|`Renew` (A)|Fails (409)|Leased (A), expiration clock reset|Fails (409)|Fails (409)|Leased (A)|  
 (B)|Fails (409)|Fails (409)|Fails (409)|Fails (409)|Fails (409)|  
|`Release` (A)|Fails (409)|Available|Available|Available|Available|  
|`Release` (B)|Fails (409)|Fails (409)|Fails (409)|Fails (409)|Fails (409)|  
|Duration expires|Available|Expired (A)|Broken (A)|Broken (A)|Expired (A)|  
  
## See Also  
 [New Blob Lease Features: Infinite Leases, Smaller Lease Times, and More](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/new-blob-lease-features-infinite-leases-smaller-lease-times-and-more.aspx)   
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Blob Service Error Codes](../StorageServicesREST/Blob-Service-Error-Codes.md)   
 [Lease Blob](../StorageServicesREST/Lease-Blob.md)
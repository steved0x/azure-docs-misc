---
title: "Get Blob Properties"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 56a87f11-8f6b-44c8-b46f-7531d359875e
caps.latest.revision: 75
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
# Get Blob Properties
The `Get Blob Properties` operation returns all user-defined metadata, standard HTTP properties, and system properties for the blob. It does not return the content of the blob.  
  
## Request  
 The `Get Blob Properties` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
||HEAD Method Request URI|HTTP Version|  
|-|-----------------------------|------------------|  
||`https://myaccount.blob.core.windows.net/mycontainer/myblob`<br /><br /> `https://myaccount.blob.core.windows.net/mycontainer/myblob?snapshot=<DateTime>`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Blob service port as `127.0.0.1:10000`, followed by the emulated storage account name:  
  
||HEAD Method Request URI|HTTP Version|  
|-|-----------------------------|------------------|  
||`http://127.0.0.1:10000/devstoreaccount1/mycontainer/myblob`|HTTP/1.1|  
  
 For more information, see [Using the Azure Storage Emulator for Development and Testing](assetId:///f0e3acde-f019-4148-9544-34cf2ff27211).  
  
### URI Parameters  
 The following additional parameters may be specified on the request URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`snapshot`|Optional. The snapshot parameter is an opaque `DateTime` value that, when present, specifies the blob snapshot to retrieve. For more information on working with blob snapshots, see [Creating a Snapshot of a Blob](../StorageServicesREST/Creating-a-Snapshot-of-a-Blob.md)|  
|`timeout`|Optional. The `timeout` parameter is expressed in seconds. For more information, see [Setting Timeouts for Blob Service Operations](../StorageServicesREST/Setting-Timeouts-for-Blob-Service-Operations.md).|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Required for all authenticated requests, optional for anonymous requests. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-lease-id: <ID>`|Optional. If this header is specified, the `Get Blob Properties` operation will be performed only if both of the following conditions are met:<br /><br /> -   The blob's lease is currently active.<br />-   The lease ID specified in the request matches that of the blob.<br /><br /> If both of these conditions are not met, the request will fail and the `Get Blob Properties` operation will fail with status code 412 (Precondition Failed).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
 This operation also supports the use of conditional headers to return blob properties and metadata only if a specified condition is met. For more information, see [Specifying Conditional Headers for Blob Service Operations](../StorageServicesREST/Specifying-Conditional-Headers-for-Blob-Service-Operations.md).  
  
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
|`Last-Modified`|The date/time that the blob was last modified. The date format follows RFC 1123. For more information, see [Representation of Date-Time Values in Headers](../StorageServicesREST/Representation-of-Date-Time-Values-in-Headers.md).<br /><br /> Any operation that modifies the blob, including an update of the blob's metadata or properties, changes the last modified time of the blob.|  
|`x-ms-meta-name:value`|A set of name-value pairs that correspond to the user-defined metadata associated with this blob.|  
|`x-ms-blob-type:<BlockBlob&#124;PageBlob&#124;AppendBlob>`|The blob type.|  
|`x-ms-copy-completion-time:<datetime>`|Version 2012-02-12 and newer. Conclusion time of the last attempted `Copy Blob` operation where this blob was the destination blob. This value can specify the time of a completed, aborted, or failed copy attempt. This header does not appear if a copy is pending, if this blob has never been the destination in a `Copy Blob` operation, or if this blob has been modified after a concluded `Copy Blob` operation using `Set Blob Properties`, `Put Blob`, or `Put Block List`.|  
|`x-ms-copy-status-description: <error string>`|Version 2012-02-12 and newer, only appears when `x-ms-copy-status` is `failed` or `pending`. Describes cause of fatal or non-fatal copy operation failure. This header does not appear if this blob has never been the destination in a `Copy Blob` operation, or if this blob has been modified after a concluded `Copy Blob` operation using `Set Blob Properties`, `Put Blob`, or `Put Block List`.|  
|`x-ms-copy-id: <id>`|Version 2012-02-12 and newer. String identifier for the last attempted `Copy Blob` operation where this blob was the destination blob. This header does not appear if this blob has never been the destination in a `Copy Blob` operation, or if this blob has been modified after a concluded `Copy Blob` operation using `Set Blob Properties`, `Put Blob`, or `Put Block List`.|  
|`x-ms-copy-progress: <bytes copied/bytes total>`|Version 2012-02-12 and newer. Contains the number of bytes copied and the total bytes in the source in the last attempted `Copy Blob` operation where this blob was the destination blob. Can show between 0 and `Content-Length` bytes copied. This header does not appear if this blob has never been the destination in a `Copy Blob` operation, or if this blob has been modified after a concluded `Copy Blob` operation using `Set Blob Properties`, `Put Blob`, or `Put Block List`.|  
|`x-ms-copy-source: url`|Version 2012-02-12 and newer. URL up to 2 KB in length that specifies the source blob used in the last attempted `Copy Blob` operation where this blob was the destination blob. This header does not appear if this blob has never been the destination in a `Copy Blob` operation, or if this blob has been modified after a concluded `Copy Blob` operation using `Set Blob Properties`, `Put Blob`, or `Put Block List`.|  
|`x-ms-copy-status: <pending &#124; success &#124; aborted &#124; failed>`|Version 2012-02-12 and newer. State of the copy operation identified by x-ms-copy-id, with these values:<br /><br /> -   `success`: Copy completed successfully.<br />-   `pending`: Copy is in progress. Check `x-ms-copy-status-description` if intermittent, non-fatal errors impede copy progress but don’t cause failure.<br />-   `aborted`: Copy was ended by `Abort Copy Blob`.<br />-   `failed`: Copy failed. See `x-ms-copy-status-description` for failure details.<br /><br /> This header does not appear if this blob has never been the destination in a `Copy Blob` operation, or if this blob has been modified after a completed `Copy Blob` operation using `Set Blob Properties`, `Put Blob`, or `Put Block List`.|  
|`x-ms-lease-duration: <infinite &#124; fixed>`|When a blob is leased, specifies whether the lease is of infinite or fixed duration. Included for requests using version 2012-02-12 and newer.|  
|`x-ms-lease-state: <available &#124; leased &#124; expired &#124; breaking &#124; broken>`|Lease state of the blob. Included for requests made using version 2012-02-12 and newer.|  
|`x-ms-lease-status:<locked&#124; unlocked>`|The lease status of the blob.|  
|`Content-Length`|The size of the blob in bytes. For a page blob, this header returns the value of the `x-ms-blob-content-length` header that is stored with the blob.|  
|`Content-Type`|The content type specified for the blob. If no content type was specified, the default content type is `application/octet-stream`.|  
|`Etag`|The ETag contains a value that you can use to perform operations conditionally. See [Specifying Conditional Headers for Blob Service Operations](../StorageServicesREST/Specifying-Conditional-Headers-for-Blob-Service-Operations.md) for more information. If the request version is 2011-08-18 or newer, the ETag value will be in quotes.|  
|`Content-MD5`|If the `Content-MD5` header has been set for the blob, this response header is returned so that the client can check for message content integrity.<br /><br /> In version 2012-02-12 and newer, `Put Blob` sets a block blob’s MD5 value even when the `Put Blob` request doesn’t include an MD5 header.|  
|`Content-Encoding`|If the `Content-Encoding` request header has previously been set for the blob, that value is returned in this header.|  
|`Content-Language`|If the `Content-Language` request header has previously been set for the blob, that value is returned in this header.|  
|`Content-Disposition`|If the `Content-Disposition` request header has previously been set for the blob, that value is returned in this header, for requests against version 2013-08-15 and later.<br /><br /> The `Content-Disposition` response header field conveys additional information about how to process the response payload, and also can be used to attach additional metadata. For example, if set to `attachment`, it indicates that the user-agent should not display the response, but instead show a Save As dialog.|  
|`Cache-Control`|If the `Cache-Control` request header has previously been set for the blob, that value is returned in this header.|  
|`x-ms-blob-sequence-number`|The current sequence number for a page blob.<br /><br /> This header is not returned for block blobs or append blobs.<br /><br /> This header is not returned for block blobs.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Blob service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.<br /><br /> This header is also returned for anonymous requests without a version specified if the container was marked for public access using the 2009-09-19 version of the Blob service.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
|`Accept-Ranges: bytes`|Indicates that the service supports requests for partial blob content. Included for requests made using version 2013-08-15 and newer.|  
|`x-ms-blob-committed-block-count`|The number of committed blocks present in the blob. This header is returned only for append blobs.|  
|`x-ms-server-encrypted: true/false`|Version 2015-12-11 or newer. The value of this header is set to `true` if the blob data and application metadata are completely encrypted using the specified algorithm. Otherwise, the value is set to `false` (when the blob is unencrypted, or if only parts of the blob/application metadata are encrypted).|  
  
### Response Body  
 None.  
  
### Sample Response  
  
```  
Response Status:  
HTTP/1.1 200 OK  
  
Response Headers:  
x-ms-meta-Name: myblob.txt  
x-ms-meta-DateUploaded: <date>  
x-ms-blob-type: AppendBlob  
x-ms-lease-status: unlocked  
x-ms-lease-state: available  
Content-Length: 11  
Content-Type: text/plain; charset=UTF-8  
Date: <date>  
ETag: "0x8CAE97120C1FF22"  
Accept-Ranges: bytes  
x-ms-blob-committed–block-count: 1  
x-ms-version: 2015-02-21  
Last-Modified: <date>  
Server: Windows-Azure-Blob/1.0 Microsoft-HTTPAPI/2.0  
x-ms-copy-id: 36650d67-05c9-4a24-9a7d-a2213e53caf6  
x-ms-copy-source: <url>  
x-ms-copy-status: success  
x-ms-copy-progress: 11/11  
x-ms-copy-completion-time: <date>  
  
```  
  
## Authorization  
 If the container's access control list (ACL) is set to allow anonymous access to the blob, any client may call this operation. If the container is private, this operation can be performed by the account owner and by anyone with a Shared Access Signature that has permission to read the blob.  
  
## Remarks  
 To determine if a `Copy Blob` operation has completed, first check that the `x-ms-copy-id` header value matches the copy ID provided by the original call to `Copy Blob`. A match assures that another application did not abort the copy and start a new `Copy Blob` operation. Then check for the `x-ms-copy-status: success` header. However, be aware that all write operations on a blob except `Lease`, `Put Page` and `Put Block` operations remove all `x-ms-copy-*` properties from the blob. These properties are also not copied by `Copy Blob` operations that use versions before 2012-02-12.  
  
 `x-ms-copy-status-description` contains more information about the `Copy Blob` failure. The following table shows `x-ms-copy-status-description` values and their meaning.  
  
 The following table describes the three fields of every `x-ms-copy-status-description` value.  
  
|Component|Description|  
|---------------|-----------------|  
|HTTP status code|Standard 3-digit integer specifying the failure.|  
|Error code|Keyword describing error that is provided by Azure in the <ErrorCode\> element. If no <ErrorCode\> element appears, a keyword containing standard error text associated with the 3-digit HTTP status code in the HTTP specification is used. See [Common REST API Error Codes](../StorageServicesREST/Common-REST-API-Error-Codes.md).|  
|Information|Detailed description of failure, in quotes.|  
  
 The following table describes the `x-ms-copy-status` and `x-ms-copy-status-description` values of common failure scenarios.  
  
> [!IMPORTANT]
>  Description text shown here can change without warning, even without a version change, so do not rely on matching this exact text.  
  
|Scenario|x-ms-copy-status value|x-ms-copy-status-description value|  
|--------------|-------------------------------|--------------------------------------------|  
|Copy operation completed successfully.|success|empty|  
|User aborted copy operation before it completed.|aborted|empty|  
|A failure occurred when reading from the source blob during a copy operation, but the operation will be retried.|pending|502 BadGateway "Encountered a retryable error when reading the source. Will retry. Time of failure: <time\>"|  
|A failure occurred when writing to the destination blob of a copy operation, but the operation will be retried.|pending|500 InternalServerError "Encountered a retryable error. Will retry. Time of failure: <time\>"|  
|An unrecoverable failure occurred when reading from the source blob of a copy operation.|failed|404 ResourceNotFound "Copy failed when reading the source." **Note:**  When reporting this underlying error, Azure returns `ResourceNotFound` in the <ErrorCode\> element. If no <ErrorCode\> element appeared in the response, a standard string representation of the HTTP status such as `NotFound` would appear.|  
|The timeout period limiting all copy operations elapsed. (Currently the timeout period is 2 weeks.)|failed|500 OperationCancelled "The copy exceeded the maximum allowed time."|  
|The copy operation failed too often when reading from the source, and didn’t meet a minimum ratio of attempts to successes. (This timeout prevents retrying a very poor source over 2 weeks before failing).|failed|500 OperationCancelled "The copy failed when reading the source."|  
  
## See Also  
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Blob Service Error Codes](../StorageServicesREST/Blob-Service-Error-Codes.md)
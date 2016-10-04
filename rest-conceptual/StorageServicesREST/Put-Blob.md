---
title: "Put Blob"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: b213c30f-8d30-4718-ba77-2030f3009719
caps.latest.revision: 86
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
# Put Blob
The `Put Blob` operation creates a new block, page, or append blob, or updates the content of an existing block blob.  
  
 Updating an existing block blob overwrites any existing metadata on the blob. Partial updates are not supported with **Put Blob**; the content of the existing blob is overwritten with the content of the new blob. To perform a partial update of the content of a block blob, use the [Put Block List](../StorageServicesREST/Put-Block-List.md) operation.  
  
 Note that you can create an append blob only in version 2015-02-21 and later.  
  
 A call to a `Put Blob` to create a page blob or an append blob only initializes the blob. To add content to a page blob, call the [Put Page](../StorageServicesREST/Put-Page.md) operation. To add content to an append blob, call the [Append Block](../StorageServicesREST/Append-Block.md) operation.  
  
## Request  
 The `Put Blob` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
||PUT Method Request URI|HTTP Version|  
|-|----------------------------|------------------|  
||`https://myaccount.blob.core.windows.net/mycontainer/myblob`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Blob service port as `127.0.0.1:10000`, followed by the emulated storage account name:  
  
||PUT Method Request URI|HTTP Version|  
|-|----------------------------|------------------|  
||`http://127.0.0.1:10000/devstoreaccount1/mycontainer/myblob`|HTTP/1.1|  
  
 Note that the storage emulator only supports blob sizes up to 2 GB.  
  
 For more information, see [Using the Azure Storage Emulator for Development and Testing](assetId:///f0e3acde-f019-4148-9544-34cf2ff27211).  
  
### URI Parameters  
 The following additional parameters may be specified on the request URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`timeout`|Optional. The<br /><br /> timeout parameter is expressed in seconds. For more information, see [Setting Timeouts for Blob Service Operations](../StorageServicesREST/Setting-Timeouts-for-Blob-Service-Operations.md).|  
  
### Request Headers (All Blob Types)  
 The following table describes required and optional request headers for all blob types.  
  
|Request header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Required for all authenticated requests. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`Content-Length`|Required. The length of the request.<br /><br /> For a page blob or an append blob, the value of this header must be set to zero, as [Put Blob](../StorageServicesREST/Put-Blob.md) is used only to initialize the blob. To write content to an existing page blob, call [Put Page](../StorageServicesREST/Put-Page.md). To write content to an append blob, call [Append Block](../StorageServicesREST/Append-Block.md).|  
|`Content-Type`|Optional. The MIME content type of the blob. The default type is `application/octet-stream`.|  
|`Content-Encoding`|Optional. Specifies which content encodings have been applied to the blob. This value is returned to the client when the [Get Blob](../StorageServicesREST/Get-Blob.md) operation is performed on the blob resource. The client can use this value when returned to decode the blob content.|  
|`Content-Language`|Optional. Specifies the natural languages used by this resource.|  
|`Content-MD5`|Optional. An MD5 hash of the blob content. This hash is used to verify the integrity of the blob during transport. When this header is specified, the storage service checks the hash that has arrived with the one that was sent. If the two hashes do not match, the operation will fail with error code 400 (Bad Request).<br /><br /> When omitted in version 2012-02-12 and later, the Blob service generates an MD5 hash.<br /><br /> Results from [Get Blob](../StorageServicesREST/Get-Blob.md), [Get Blob Properties](../StorageServicesREST/Get-Blob-Properties.md), and [List Blobs](../StorageServicesREST/List-Blobs.md) include the MD5 hash.|  
|`Cache-Control`|Optional. The Blob service stores this value but does not use or modify it.|  
|`x-ms-blob-content-type`|Optional. Set the blob’s content type.|  
|`x-ms-blob-content-encoding`|Optional. Set the blob’s content encoding.|  
|`x-ms-blob-content-language`|Optional. Set the blob's content language.|  
|`x-ms-blob-content-md5`|Optional. Set the blob’s MD5 hash.|  
|`x-ms-blob-cache-control`|Optional. Sets the blob's cache control.|  
|`x-ms-blob-type:<BlockBlob &#124; PageBlob &#124; AppendBlob>`|Required. Specifies the type of blob to create: block blob, page blob, or append blob.  Support for creating an append blob is available only in version 2015-02-21 and later.|  
|`x-ms-meta-name:value`|Optional. Name-value pairs associated with the blob as metadata.<br /><br /> Note that beginning with version 2009-09-19, metadata names must adhere to the naming rules for [C# identifiers](http://msdn.microsoft.com/library/aa664670%28VS.71%29.aspx).|  
|`x-ms-lease-id:<ID>`|Required if the blob has an active lease. To perform this operation on a blob with an active lease, specify the valid lease ID for this header.|  
|`x-ms-blob-content-disposition`|Optional. Sets the blob’s `Content-Disposition` header. Available for versions 2013-08-15 and later.<br /><br /> The `Content-Disposition` response header field conveys additional information about how to process the response payload, and also can be used to attach additional metadata. For example, if set to `attachment`, it indicates that the user-agent should not display the response, but instead show a **Save As** dialog with a filename other than the blob name specified.<br /><br /> The response from the [Get Blob](../StorageServicesREST/Get-Blob.md) and [Get Blob Properties](../StorageServicesREST/Get-Blob-Properties.md) operations includes the `content-disposition` header.|  
|`Origin`|Optional. Specifies the origin from which the request is issued. The presence of this header results in cross-origin resource sharing headers on the response. See [CORS Support for the Storage Services](../StorageServicesREST/Cross-Origin-Resource-Sharing--CORS--Support-for-the-Azure-Storage-Services.md) for details.|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
 This operation also supports the use of conditional headers to write the blob only if a specified condition is met. For more information, see [Specifying Conditional Headers for Blob Service Operations](../StorageServicesREST/Specifying-Conditional-Headers-for-Blob-Service-Operations.md).  
  
### Request Headers (Page Blobs Only)  
 The following table describes request headers applicable only for operations on page blobs.  
  
|Request header|Description|  
|--------------------|-----------------|  
|`x-ms-blob-content-length: bytes`|Required for page blobs. This header specifies the maximum size for the page blob, up to 1 TB. The page blob size must be aligned to a 512-byte boundary.<br /><br /> If this header is specified for a block blob or an append blob, the Blob service returns status code 400 (Bad Request).|  
|`x-ms-blob-sequence-number: <num>`|Optional. Set for page blobs only. The sequence number is a user-controlled value that you can use to track requests. The value of the sequence number must be between 0 and 2<sup>^63</sup> - 1.The default value is 0.|  
  
### Request Body  
 For a block blob, the request body contains the content of the blob.  
  
 For a page blob or an append blob, the request body is empty.  
  
### Sample Request  
 The following example shows a request to create a block blob:  
  
```  
Request Syntax:  
PUT https://myaccount.blob.core.windows.net/mycontainer/myblockblob HTTP/1.1  
  
Request Headers:  
x-ms-version: 2015-02-21  
x-ms-date: <date>  
Content-Type: text/plain; charset=UTF-8  
x-ms-blob-content-disposition: attachment; filename="fname.ext"  
x-ms-blob-type: BlockBlob  
x-ms-meta-m1: v1  
x-ms-meta-m2: v2  
Authorization: SharedKey myaccount:YhuFJjN4fAR8/AmBrqBz7MG2uFinQ4rkh4dscbj598g=  
Content-Length: 11  
  
Request Body:  
hello world  
  
```  
  
 This sample request creates a page blob and specifies its maximum size as 1024 bytes. Note that you must call [Put Page](../StorageServicesREST/Put-Page.md) to add content to a page blob:  
  
```  
Request Syntax:  
PUT https://myaccount.blob.core.windows.net/mycontainer/mypageblob HTTP/1.1  
  
Request Headers:  
x-ms-version: 2015-02-21  
x-ms-date: <date>  
Content-Type: text/plain; charset=UTF-8  
x-ms-blob-type: PageBlob  
x-ms-blob-content-length: 1024  
x-ms-blob-sequence-number: 0  
Authorization: SharedKey   
Origin: http://contoso.com  
Vary: Origin  
myaccount:YhuFJjN4fAR8/AmBrqBz7MG2uFinQ4rkh4dscbj598g=  
Content-Length: 0  
```  
  
 This sample request creates an append blob. Note that you must call [Append Block](../StorageServicesREST/Append-Block.md) to add content to the append blob:  
  
```  
Request Syntax:  
PUT https://myaccount.blob.core.windows.net/mycontainer/myappendblob HTTP/1.1  
  
Request Headers:  
x-ms-version: 2015-02-21  
x-ms-date: <date>  
Content-Type: text/plain; charset=UTF-8  
x-ms-blob-type: AppendBlob  
Authorization: SharedKey myaccount:YhuFJjN4fAR8/AmBrqBz7MG2uFinQ4rkh4dscbj598g=  
Origin: http://contoso.com  
Vary: Origin  
Content-Length: 0  
  
```  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 201 (Created).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response can also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`ETag`|The ETag contains a value that the client can use to perform conditional `PUT` operations by using the `If-Match` request header. If the request version is 2011-08-18 or newer, the ETag value will be in quotes.|  
|`Last-Modified`|The date/time that the blob was last modified. The date format follows RFC 1123. For more information, see [Representation of Date-Time Values in Headers](../StorageServicesREST/Representation-of-Date-Time-Values-in-Headers.md).<br /><br /> Any write operation on the blob (including updates on the blob's metadata or properties) changes the last modified time of the blob.|  
|`Content-MD5`|This header is returned for a block blob so the client can check the integrity of message content. The `Content-MD5` value returned is computed by the Blob service. In version 2012-02-12 and later, this header is returned even when the request does not include `Content-MD5` or `x-ms-blob-content-md5` headers.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Blob service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
|`Access-Control-Allow-Origin`|Returned if the request includes an `Origin` header and CORS is enabled with a matching rule. This header returns the value of the origin request header in case of a match.|  
|`Access-Control-Expose-Headers`|Returned if the request includes an `Origin` header and CORS is enabled with a matching rule. Returns the list of response headers that are to be exposed to the client or issuer of the request.|  
|`Access-Control-Allow-Credentials`|Returned if the request includes an `Origin` header and CORS is enabled with a matching rule that does not allow all origins. This header will be set to true.|  
|`x-ms-request-server-encrypted: true/false`|Version 2015-12-11 or newer. The value of this header is set to `true` if the contents of the request are successfully encrypted using the specified algorithm, and `false` otherwise.|  
  
### Response Body  
 None.  
  
### Sample Response  
  
```  
Response Status:  
HTTP/1.1 201 Created  
  
Response Headers:  
Transfer-Encoding: chunked  
Content-MD5: sQqNsWTgdUEFt6mb5y4/5Q==  
Date: <date>  
ETag: "0x8CB171BA9E94B0B"  
Last-Modified: <date>  
Access-Control-Allow-Origin: http://contoso.com  
Access-Control-Expose-Headers: Content-MD5  
Access-Control-Allow-Credentials: True  
Server: Windows-Azure-Blob/1.0 Microsoft-HTTPAPI/2.0  
```  
  
## Authorization  
 This operation can be called by the account owner and by any client with a shared access signature that has permission to write to this blob or its container.  
  
## Remarks  
 When you create a blob, you must specify whether it is a block blob, append blob, or page blob by specifying the value of the `x-ms-blob-type` header. Once a blob has been created, the type of the blob cannot be changed unless it is deleted and re-created.  
  
 The maximum size for a block blob created via `Put Blob` is 64 MB. If your blob is larger than 64 MB, you must upload it as a set of blocks. For more information, see the [Put Block](../StorageServicesREST/Put-Block.md) and [Put Block List](../StorageServicesREST/Put-Block-List.md) operations. It's not necessary to also call `Put Blob` if you upload the blob as a set of blocks.  
  
 If you attempt to upload a block blob that is larger than 64 MB, or a page blob larger than 1 TB, the service returns status code 413 (Request Entity Too Large). The Blob service also returns additional information about the error in the response, including the maximum blob size permitted in bytes.  
  
 To create a new page blob, first initialize the blob by calling `Put Blob` and specify its maximum size, up to 1 TB. When creating a page blob, do not include content in the request body. Once the blob has been created, call [Put Page](../StorageServicesREST/Put-Page.md) to add content to the blob or to modify it.  
  
 To create a new append blob, call `Put Blob` to create a blob with a content-length of zero bytes. Once the append blob is created, call [Append Block](../StorageServicesREST/Append-Block.md) to add content to the end of the blob.  
  
 If you call `Put Blob` to overwrite an existing blob with the same name, any snapshots associated with the original blob are retained. To remove associated snapshots, call [Delete Blob](../StorageServicesREST/Delete-Blob.md) first, then `Put Blob` to re-create the blob.  
  
 A blob has custom properties (set via headers) that you can use to store values associated with standard HTTP headers. These values can subsequently be read by calling [Get Blob Properties](../StorageServicesREST/Get-Blob-Properties.md), or modified by calling [Set Blob Properties](../StorageServicesREST/Set-Blob-Properties.md). The custom property headers and corresponding standard HTTP header are listed in the following table:  
  
|HTTP header|Custom blob property header|  
|-----------------|---------------------------------|  
|`Content-Type`|`x-ms-blob-content-type`|  
|`Content-Encoding`|`x-ms-blob-content-encoding`|  
|`Content-Language`|`x-ms-blob-content-language`|  
|`Content-MD5`|`x-ms-blob-content-md5`|  
|`Cache-Control`|`x-ms-blob-cache-control`|  
  
 The semantics for setting persisting these property values with the blob as follows:  
  
-   If the client specifies a custom property header, as indicated by the `x-ms-blob` prefix, this value is stored with the blob.  
  
-   If the client specifies a standard HTTP header, but not the custom property header, the value is stored in the corresponding custom property associated with the blob, and is returned by a call to `Get Blob Properties`. For example, if the client sets the `Content-Type` header on the request, that value is stored in the blob's `x-ms-blob-content-type` property.  
  
-   If the client sets both the standard HTTP header and the corresponding property header on the same request, the PUT request uses the value provided for the standard HTTP header, but the value specified for the custom property header is persisted with the blob and returned by subsequent GET requests.  
  
 If the blob has an active lease, the client must specify a valid lease ID on the request in order to overwrite the blob. If the client does not specify a lease ID, or specifies an invalid lease ID, the Blob service returns status code 412 (Precondition Failed). If the client specifies a lease ID but the blob does not have an active lease, the Blob service also returns status code 412 (Precondition Failed). If the client specifies a lease ID on a blob that does not yet exist, the Blob service will return status code 412 (Precondition Failed) for requests made against version 2013-08-15 and later; for prior versions the Blob service will return status code 201 (Created).  
  
 If an existing blob with an active lease is overwritten by a `Put Blob` operation, the lease persists on the updated blob, until it expires or is released.  
  
 A `Put Blob` operation is permitted 10 minutes per MB to complete. If the operation is taking longer than 10 minutes per MB on average, the operation will timeout.  
  
## See Also  
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Blob Service Error Codes](../StorageServicesREST/Blob-Service-Error-Codes.md)   
 [Setting Timeouts for Blob Service Operations](../StorageServicesREST/Setting-Timeouts-for-Blob-Service-Operations.md)
---
title: "Put Range"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 39424f85-a00a-4291-ab9d-1bc6488a8f06
caps.latest.revision: 9
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
# Put Range
The `Put Range` operation writes a range of bytes to a file.  
  
## Request  
 The `Put Range` request may be constructed as follows. HTTPS is recommended.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|PUT|`https://myaccount.file.core.windows.net/myshare/mydirectorypath/myfile?comp=range`|HTTP/1.1|  
  
 Replace the path components shown in the request URI with your own, as follows:  
  
|Path Component|Description|  
|--------------------|-----------------|  
|*myaccount*|The name of your storage account.|  
|*myshare*|The name of your file share.|  
|*mydirectorypath*|Optional. The path to the parent directory.|  
|*myfile*|The name of the file.|  
  
 For details on path naming restrictions, see [Naming and Referencing Shares, Directories, Files, and Metadata](../StorageServicesREST/Naming-and-Referencing-Shares--Directories--Files--and-Metadata.md).  
  
### URI Parameters  
 The following additional parameters may be specified on the request URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`timeout`|Optional. The `timeout` parameter is expressed in seconds. For more information, see [Setting Timeouts for File Service Operations](../StorageServicesREST/Setting-Timeouts-for-File-Service-Operations.md).|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Required for all authenticated requests. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`Range` or `x-ms-range`|Either `Range` or `x-ms-range` is required.<br /><br /> Specifies the range of bytes to be written. Both the start and end of the range must be specified. This header is defined by the [HTTP/1.1 protocol specification](http://www.w3.org/Protocols/rfc2616/rfc2616.html).<br /><br /> For an update operation, the range can be up to 4 MB in size. For a clear operation, the range can be up to the value of the file's full size.<br /><br /> The File service accepts only a single byte range for the `Range` and `x-ms-range` headers, and the byte range must be specified in the following format: `bytes=startByte-endByte`.<br /><br /> If both `Range` and `x-ms-range` are specified, the service uses the value of `x-ms-range`. See [Specifying the Range Header for File Service Operations](../StorageServicesREST/Specifying-the-Range-Header-for-File-Service-Operations.md) for more information.|  
|`Content-Length`|Required. Specifies the number of bytes being transmitted in the request body. When the `x-ms-write` header is set to `clear`, the value of this header must be set to zero.|  
|`Content-MD5`|Optional. An MD5 hash of the content. This hash is used to verify the integrity of the data during transport. When the `Content-MD5` header is specified, the File service compares the hash of the content that has arrived with the header value that was sent. If the two hashes do not match, the operation will fail with error code 400 (Bad Request).<br /><br /> The `Content-MD5` header is not permitted when the `x-ms-write` header is set to `clear`. If it is included with the request, the File service returns status code 400 (Bad Request).|  
|`x-ms-write: {update &#124; clear}`|Required. You may specify one of the following options:<br /><br /> -   `Update`: Writes the bytes specified by the request body into the specified range. The `Range` and `Content-Length` headers must match to perform the update.<br />-   `Clear`: Clears the specified range and releases the space used in storage for that range. To clear a range, set the `Content-Length` header to zero, and set the `Range` header to a value that indicates the range to clear, up to maximum file size.|  
  
### Request Body  
 None.  
  
### Sample Request: Update Byte Range  
  
```  
Request Syntax:  
PUT https://myaccount.file.core.windows.net/myshare/myfile?comp=range HTTP/1.1  
  
Request Headers:  
x-ms-write: update  
x-ms-date: Mon, 27 Jan 2014 22:15:50 GMT  
x-ms-version: 2014-02-14  
x-ms-range: bytes=0-65535  
Authorization: SharedKey myaccount:4KdWDiTdA9HmIF9+WF/8WfYOpUrFhieGIT7f0av+GEI=  
Content-Length: 65536  
```  
  
### Sample Request: Clear Byte Range  
  
```  
Request Syntax:  
PUT https://myaccount.file.core.windows.net/myshare/myfile?comp=range HTTP/1.1  
  
Request Headers:  
Range: bytes=1024-2048  
x-ms-write: clear  
x-ms-date: Mon, 27 Jan 2014 23:37:35 GMT  
x-ms-version: 2014-02-14  
Authorization: SharedKey myaccount:4KdWDiTdA9HmIF9+WF/8WfYOpUrFhieGIT7f0av+GEI=  
```  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 201 (Created).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response Header|Description|  
|---------------------|-----------------|  
|`ETag`|The ETag contains a value which represents the version of the file, in quotes.|  
|`Last-Modified`|Returns the date and time the directory was last modified. The date format follows RFC 1123. For more information, see [Representation of Date-Time Values in Headers](../StorageServicesREST/Representation-of-Date-Time-Values-in-Headers.md). Any operation that modifies the share or its properties or metadata updates the last modified time. Operations on files do not affect the last modified time of the share.|  
|`Content-MD5`|This header is returned so that the client can check for message content integrity. The value of this header is computed by the File service; it is not necessarily the same value as may have been specified in the request headers.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the File service used to execute the request.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
### Response Body  
 None.  
  
### Sample Response  
  
```  
  
Response Status:  
HTTP/1.1 201 Created  
  
Response Headers:  
Transfer-Encoding: chunked  
Content-MD5: sQqNsWTgdUEFt6mb5y4/5Q==  
Date:Mon, 27 Jan 2014 22:33:35 GMT  
ETag: "0x8CB171BA9E94B0B"  
Last-Modified: Mon, 27 Jan 2014 12:13:31 GMT  
x-ms-version: 2014-02-14  
Content-Length: 0  
Server: Windows-Azure-File/1.0 Microsoft-HTTPAPI/2.0  
  
```  
  
## Authorization  
 Only the account owner may call this operation.  
  
## Remarks  
 The `Put Range` operation writes a range of byte to a file. This operation can only be called on an existing file. It cannot be called to create a new file. Calling `Put Range` with a file name that does not currently exist returns status code 404 (Not Found).  
  
 To create a new file, call [Create File](../StorageServicesREST/Create-File.md). A file may be up to 1 TB in size.  
  
 A `Put Range` operation is permitted 10 minutes per MB to complete. If the operation is taking longer than 10 minutes per MB on average, the operation will timeout.  
  
 **Range Update Operations**  
  
 Calling `Put Range` with the `Update` option performs an in-place write on the specified file. Any content in the specified range is overwritten with the update. Each range submitted with `Put Range` for an update operation may be up to 4 MB in size. If you attempt to upload a range that is larger than 4 MB, the service returns status code 413 (Request Entity Too Large).  
  
 **Range Clear Operations**  
  
 Calling `Put Range` with the `Clear` option releases the space in storage as long as the specified range is 512-byte aligned. Ranges that have been cleared are no longer tracked as part of the file and will not be returned in the [List Ranges](../StorageServicesREST/List-Ranges.md) response. If the specified range is not 512-byte aligned, the operation will write zeros to the start or end of the range that is not 512-byte aligned and free the rest of the range inside that is 512-byte aligned.  
  
 Any ranges that have not been cleared will be returned in the [List Ranges](../StorageServicesREST/List-Ranges.md) response. For an example, see **Sample Unaligned Clear Range** below.  
  
 **SMB Client Byte Range Locks**  
  
 While the SMB protocol allows byte range locks to manage read and write access to regions of a file, the `Put Range` operation does not leverage this capability for the specified `x-ms-range` value. Instead, `Put Range` requires write access to the entire file. This also means that `Put Range` will fail if an SMB client has a lock on any range within the file. For more details, see [Managing File Locks](../StorageServicesREST/Managing-File-Locks.md).  
  
 **SMB Client Directory Change Notifications**  
  
 The SMB protocol supports the [FindFirstChangeNotification](msdn.microsoft.com/library/windows/desktop/aa364417.aspx) API function that allows applications to detect when changes occur in the file system. It can detect when a file or directory is added, changed, deleted, and when a file’s size, attributes, or security descriptors change. SMB clients using this API will not receive notifications when a file or directory change happens via the File service REST API. However, changes caused by other SMB clients will propagate notifications.  
  
 **Sample Unaligned Clear Range**  
  
 Suppose a file is created with [Create File](../StorageServicesREST/Create-File.md) and a single range is written with `Put Range`, as follows:  
  
```  
  
Request Syntax:  
PUT https://myaccount.file.core.windows.net/myshare/myfile?comp=range HTTP/1.1  
  
Request Headers:  
x-ms-write: updte  
x-ms-date: Mon, 27 Jan 2014 22:15:50 GMT  
x-ms-version: 2014-02-14  
x-ms-range: bytes=0-65536  
Authorization: SharedKey myaccount:4KdWDiTdA9HmIF9+WF/8WfYOpUrFhieGIT7f0av+GEI=  
Content-Length: 65536  
  
```  
  
 Performing a [List Ranges](../StorageServicesREST/List-Ranges.md) operation on the file will return the following response body:  
  
```xml  
<?xml version="1.0" ecoding="utf-8"?>  
<Ranges>  
 <Range>  
  <Start>0</Start>  
  <End>65536</End>  
 </Range>  
</Ranges>  
```  
  
 Now suppose an unaligned clear range byte range operation is performed:  
  
```  
Request Syntax:  
PUT https://myaccount.file.core.windows.net/myshare/myfile?comp=range HTTP/1.1  
  
Request Headers:  
Range: bytes=768-2304  
x-ms-write: clear  
x-ms-date: Mon, 27 Jan 2014 23:37:35 GMT  
x-ms-version: 2014-02-14  
Authorization: SharedKey myaccount:4KdWDiTdA9HmIF9+WF/8WfYOpUrFhieGIT7f0av+GEI=  
```  
  
 A subsequent [List Ranges](../StorageServicesREST/List-Ranges.md) operation on the file will return the following response body:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<Ranges>  
 <Range>  
  <Start>0</Start>  
  <End>1024</End>  
 </Range>  
 <Range>  
  <Start>2048</Start>  
  <End>65535</End>  
 </Range>  
</Ranges>  
```  
  
 Note that zeros have been written to the unaligned space from 768-1024 and 2048-2304.  
  
## See Also  
 [Operations on Files](../StorageServicesREST/Operations-on-Files.md)
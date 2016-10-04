---
title: "Get File Properties"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 668f1c01-d54f-408b-b628-c8ab43e8eb85
caps.latest.revision: 15
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
# Get File Properties
The `Get File Properties` operation returns all user-defined metadata, standard HTTP properties, and system properties for the file. It does not return the content of the file.  
  
## Request  
 The `Get File Properties` request may be constructed as follows. HTTPS is recommended.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`HEAD`|`https://myaccount.file.core.windows.net/myshare/mydirectorypath/myfile`|HTTP/1.1|  
  
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
|`timeout`|Optional. The `timeout` parameter is expressed in seconds. For more information, see [Setting Timeouts for File Service Operations](../StorageServicesREST/Setting-Timeouts-for-File-Service-Operations.md)|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|Authorization|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Required for all authenticated requests. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
  
### Request Body  
 None.  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 200 (OK).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response Header|Description|  
|---------------------|-----------------|  
|`Last-Modified`|Returns the date and time the file was last modified. The date format follows RFC 1123. For more information, see [Representation of Date-Time Values in Headers](../StorageServicesREST/Representation-of-Date-Time-Values-in-Headers.md). Any operation that modifies the file or its properties updates the last modified time.|  
|`x-ms-meta-name:value`|A set of name-value pairs associated with this file as user-defined metadata.|  
|`x-ms-type: <File>`|Returns the type `File`. Reserved for future use.|  
|`Content-Length`|The size of the file in bytes. This header returns the value of the `x-ms-content-length` header that is stored with the file.|  
|`Content-Type`|The content type specified for the file. If no content type was specified, the default content type is `application/octet-stream`.|  
|`ETag`|The ETag contains a value that you can use to perform operations conditionally, in quotes.|  
|`Content-MD5`|If the `Content-MD5` header has been set for the file, the `Content-MD5` response header is returned so that the client can check for message content integrity.|  
|`Content-Encoding`|If the `Content-Encoding` request header has previously been set for the file, the `Content-Encoding` value is returned in this header.|  
|`Content-Language`|If the `Content-Language` request header has previously been set for the file, the `Content-Language` value is returned in this header.|  
|`Cache-Control`|If the `Cache-Control` request header has previously been set for the file, the `Cache-Control` value is returned in this header.|  
|`Content-Disposition`|Returns the value that was specified for the `x-ms-content-disposition` header and specifies how to process the response.<br /><br /> The `Content-Disposition` response header field conveys additional information about how to process the response payload, and also can be used to attach additional metadata. For example, if set to `attachment`, `Content-Disposition` indicates that the user-agent should not display the response, but instead show a **Save As** dialog.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the File service used to execute the request.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
|`x-ms-copy-completion-time:<datetime>`|Version 2015-02-21 and newer. Conclusion time of the last attempted **Copy File** operation where this file was the destination file. This value can specify the time of a completed, aborted, or failed copy attempt. This header does not appear if a copy is pending, if this file has never been the destination in a **Copy File** operation, or if this file has been modified after a concluded **Copy File** operation using **Set File Properties** or **Create File**.|  
|`x-ms-copy-status-description: <error string>`|Version 2015-02-21 and newer. Only appears when `x-ms-copy-status` is *failed* or *pending*. Describes cause of fatal or non-fatal copy operation failure. This header does not appear if this file has never been the destination in a **Copy File** operation, or if this file has been modified after a concluded **Copy File** operation using **Set File Properties** or **Create File**.|  
|`x-ms-copy-id: <id>`|Version 2015-02-21 and newer. String identifier for the last attempted **Copy File** operation where this file was the destination file. This header does not appear if the file has never been the destination in a **Copy File** operation, or if this file has been modified after a concluded **Copy File** operation using **Set File Properties** or **Create File**.|  
|`x-ms-copy-progress: <bytes copied/bytes total>`|Version 2015-02-21 and newer. Contains the number of bytes copied and the total bytes in the source in the last attempted **Copy File** operation where this file was the destination file. Can show between 0 and `Content-Length` bytes copied. This header does not appear if this file has never been the destination in a **Copy File** operation, or if this file has been modified after a concluded **Copy File** operation using **Set File Properties** or **Create File**.|  
|`x-ms-copy-source: url`|Version 2015-02-21 and newer. URL up to 2KB in length that specifies the source file used in the last attempted **Copy File** operation where this file was the destination file. This header does not appear if this file has never been the destination in a **Copy File** operation or if this file has been modified after a concluded **Copy File** operation using **Set File Properties** or **Create File**.|  
|`x-ms-copy-status: <pending &#124; success &#124; aborted &#124; failed>`|Version 2015-02-21 and newer. State of the copy operation identified by `x-ms-copy-id`, with these values:<br /><br /> -   *success:* Copy completed successfully.<br />-   *pending:* Copy is in progress. Check `x-ms-copy-status-description` if intermittent, non-fatal errors impede copy progress but don't cause failure.<br />-   *aborted:* Copy was ended by **Abort Copy File**.<br />-   *failed:* Copy failed. See `x-ms-copy-status-description` for failure details.<br /><br /> This header does not appear if this file has never been the destination in a **Copy File** operation, or if this file has been modified after a completed **Copy File** operation using **Set File Properties** or **Create File**.|  
  
### Response Body  
 None.  
  
### Sample Response  
  
```  
Response Status:  
HTTP/1.1 200 OK  
  
Response Headers:  
x-ms-type: File  
x-ms-meta-m1: v1  
x-ms-meta-m2: v2  
Content-Length: 11  
Content-Type: text/plain; charset=UTF-8  
Date: <date>  
ETag: "0x8CB171DBEAD6A6B"  
Last-Modified: <date>  
x-ms-version: 2015-02-21  
Server: Windows-Azure-File/1.0 Microsoft-HTTPAPI/2.0  
x-ms-copy-id: 36650d67-05c9-4a24-9a7d-a2213e53caf6  
x-ms-copy-source: <url>  
x-ms-copy-status: success  
x-ms-copy-progress: 11/11  
x-ms-copy-completion-time: <date>  
  
```  
  
## Authorization  
 Only the account owner may call this operation.  
  
## Remarks  
  
## See Also  
 [Operations on Files](../StorageServicesREST/Operations-on-Files.md)
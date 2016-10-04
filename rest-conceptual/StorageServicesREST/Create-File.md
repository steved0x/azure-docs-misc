---
title: "Create File"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 211d8e61-05b5-420d-bd4b-8cee40e0c3de
caps.latest.revision: 12
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
# Create File
The `Create File` operation creates a new file or replaces a file. Note that calling `Create File` only initializes the file. To add content to a file, call the `Put Range` operation.  
  
## Request  
 The `Create File` request may be constructed as follows. HTTPS is recommended.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`PUT`|`https://myaccount.file.core.windows.net/myshare/mydirectorypath/myfile`|HTTP/1.1|  
  
 Replace the path components shown in the request URI with your own, as follows:  
  
|Path Component|Description|  
|--------------------|-----------------|  
|*myaccount*|The name of your storage account.|  
|*myshare*|The name of your file share.|  
|*mydirectorypath*|Optional. The path to the directory where the file is to be created. If the directory path is omitted, the file will be created within the specified share.<br /><br /> If specified, the directory must already exist within the share before the file can be created.|  
|*myfile*|The name of the file to create.|  
  
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
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) time for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Required for all authenticated requests. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`Content-Length`|Optional. Must be zero if present.|  
|`x-ms-content-length: byte value`|Required. This header specifies the maximum size for the file, up to 1 TB.|  
|`Content-Type &#124; x-ms-content-type`|Optional. The MIME content type of the file. The default type is `application/octet-stream`.|  
|`Content-Encoding &#124; x-ms-content-encoding`|Optional. Specifies which content encodings have been applied to the file. This value is returned to the client when the [Get File](../StorageServicesREST/Get-File.md) operation is performed on the file resource and can be used to decode file content.|  
|`Content-Language &#124; x-ms-content-language`|Optional. Specifies the natural languages used by this resource.|  
|`Cache-Control &#124; x-ms-cache-control`|Optional. The File service stores this value but does not use or modify it.|  
|`x-ms-content-md5`|Optional. Sets the file's MD5 hash.|  
|`x-ms-content-disposition`|Optional. Sets the file’s `Content-Disposition` header.|  
|`x-ms-type: file`|Required. Set this header to `file`.|  
|`x-ms-meta-name:value`|Optional. Name-value pairs associated with the file as metadata. Metadata names must adhere to the naming rules for [C# identifiers](http://msdn.microsoft.com/library/aa664670%28VS.71%29.aspx).<br /><br /> Note that file metadata specified via the File service is not accessible from an SMB client.|  
  
### Request Body  
 None.  
  
### Sample Request  
  
```  
Request Syntax:  
PUT https://myaccount.file.core.windows.net/myshare/myfile HTTP/1.1  
  
Request Headers:  
x-ms-version: 2014-02-14  
x-ms-date: Mon, 27 Jan 2014 22:41:55 GMT  
Content-Type: text/plain; charset=UTF-8  
x-ms-content-length: 1024  
Authorization: SharedKey myaccount:YhuFJjN4fAR8/AmBrqBz7MG2uFinQ4rkh4dscbj598g=  
  
```  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 201 (Created).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`ETag`|The ETag contains a value which represents the version of the file, in quotes.|  
|`Last-Modified`|Returns the date and time the share was last modified. The date format follows RFC 1123. For more information, see [Representation of Date-Time Values in Headers](../StorageServicesREST/Representation-of-Date-Time-Values-in-Headers.md).<br /><br /> Any operation that modifies the directory or its properties updates the last modified time. Operations on files do not affect the last modified time of the directory.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md)|  
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
Date: Mon, 27 Jan 2014 23:00:12 GMT  
ETag: "0x8CB14C3E29B7E82"  
Last-Modified: Mon, 27 Jan 2014 23:00:06 GMT  
x-ms-version: 2014-02-14  
Server: Windows-Azure-File/1.0 Microsoft-HTTPAPI/2.0  
```  
  
## Authorization  
 Only the account owner may call this operation.  
  
## Remarks  
 To create a new file, first initialize the file by calling `Create File` and specify its maximum size, up to 1 TB. When performing this operation, do not include content in the request body. Once the file has been created, call `Put Range` to add content to the file or to modify it.  
  
 You can change the size of the file by calling `Set File Properties`.  
  
 If the share or parent directory does not exist, then the operation fails with status code 412 (Precondition Failed).  
  
 Note that the file properties `cache-control`, `content-type`, `content-md5`, `content-encoding` and `content-language` are discrete from the file system properties available to SMB clients. SMB clients are not able to read, write or modify these property values.  
  
## See Also  
 [Operations on Files](../StorageServicesREST/Operations-on-Files.md)
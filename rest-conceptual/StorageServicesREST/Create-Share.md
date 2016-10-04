---
title: "Create Share"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: dfc2c537-f05d-4647-a71e-952f2dc1f24f
caps.latest.revision: 13
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
# Create Share
The `Create Share` operation creates a new share under the specified account. If the share with the same name already exists, the operation fails.  
  
 The share resource includes metadata and properties for that share. It does not include a list of the files contained by the share.  
  
## Request  
 The `Create Share` request may be constructed as follows. HTTPS is recommended.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`PUT`|`https://myaccount.file.core.windows.net/myshare?restype=share`|HTTP/1.1|  
  
 Replace the path components shown in the request URI with your own, as follows:  
  
|Path Component|Description|  
|--------------------|-----------------|  
|*myaccount*|The name of your storage account.|  
|*myshare*|The name of your file share. Note that it may include only lower-case characters.|  
  
 For details on path naming restrictions, see [Naming and Referencing Shares, Directories, Files, and Metadata](../StorageServicesREST/Naming-and-Referencing-Shares--Directories--Files--and-Metadata.md).  
  
### URI Parameters  
 The following additional parameters may be specified on the request URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`timeout`|Optional. The timeout parameter is expressed in seconds. For more information, see [Setting Timeouts for File Service Operations](../StorageServicesREST/Setting-Timeouts-for-File-Service-Operations.md).|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) time for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Required for all authenticated requests. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-meta-name:value`|Optional. A name-value pair to associate with the share as metadata.<br /><br /> Metadata names must adhere to the naming rules for [C# identifiers](http://msdn.microsoft.com/library/aa664670%28VS.71%29.aspx).|  
|`x-ms-share-quota`|Optional. Supported in version 2015-02-21 and above. Specifies the maximum size of the share, in gigabytes. Must be greater than 0, and less than or equal to 5TB (5120).|  
  
### Request Body  
 None.  
  
### Sample Request  
  
```  
PUT https://myaccount.file.core.windows.net/myshare?restype=share HTTP/1.1  
  
Request Headers:  
x-ms-version: 2015-02-21  
x-ms-date: <date>  
x-ms-meta-Name: StorageSample  
Authorization: SharedKey myaccount:Z5043vY9MesKNh0PNtksNc9nbXSSqGHueE00JdjidOQ=  
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
|`ETag`|The ETag contains a value which represents the version of the share, in quotes.|  
|`Last-Modified`|Returns the date and time the share was last modified. The date format follows RFC 1123. For more information, see [Representation of Date-Time Values in Headers](../StorageServicesREST/Representation-of-Date-Time-Values-in-Headers.md).<br /><br /> Any operation that modifies the share or its properties or metadata updates the last modified time. Operations on files do not affect the last modified time of the share.|  
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
Date: <date>  
ETag: "0x8CB14C3E29B7E82"  
Last-Modified: <date>  
x-ms-version: 2015-02-21  
Server: Windows-Azure-File/1.0 Microsoft-HTTPAPI/2.0  
```  
  
## Authorization  
 Only the account owner may call this operation.  
  
## Remarks  
 Shares are created immediately beneath the storage account. It's not possible to nest one share beneath another.  
  
 You can specify metadata for a share at the time it is created by including one or more metadata headers on the request. The format for the metadata header is `x-ms-meta-name:value`.  
  
 If a share by the same name is being deleted when `Create Share` is called, the server will return status code 409 (Conflict), with additional error information indicating that the share is being deleted.  
  
 The share size quota can be used to limit the size of files stored on the share.  It does not limit the size of snapshots.  The overhead associated with files that is used in computing the billing size for the storage account is not accounted for in the quota.  
  
 When the sum of the sizes of the files on the share exceeds the quota set on the share, attempts to increase the size of a file will fail, and creating new non-empty files (via REST) will fail. You will still be able to create empty files.  
  
 Changing or setting the quota has no effect on billing. You will still be billed for the size of the files plus the overhead.  
  
## See Also  
 [Operations on Shares (File Service)](../StorageServicesREST/Operations-on-Shares--File-Service-.md)
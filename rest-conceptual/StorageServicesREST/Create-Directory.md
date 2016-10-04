---
title: "Create Directory"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: b105fd20-fd69-4aaa-96a0-fdec7e4315d7
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
# Create Directory
The `Create Directory` operation creates a new directory under the specified share or parent directory. The directory resource includes the properties for that directory. It does not include a list of the files or subdirectories contained by the directory.  
  
## Request  
 The `Create Directory` request may be constructed as follows. HTTPS is recommended.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`PUT`|`https://myaccount.file.core.windows.net/myshare/myparentdirectorypath/mydirectory?restype=directory`|HTTP/1.1|  
  
 Replace the path components shown in the request URI with your own, as follows:  
  
|Path Component|Description|  
|--------------------|-----------------|  
|*myaccount*|The name of your storage account.|  
|*myshare*|The name of your file share.|  
|*myparentdirectorypath*|Optional. The path to the parent directory where *mydirectory* is to be created. If the parent directory path is omitted, the directory will be created within the specified share.<br /><br /> If specified, the parent directory must already exist within the share before *mydirectory* can be created.|  
|*mydirectory*|The name of the directory to create.|  
  
 For details on path naming restrictions, see [Naming and Referencing Shares, Directories, Files, and Metadata](../StorageServicesREST/Naming-and-Referencing-Shares--Directories--Files--and-Metadata.md).  
  
### URI Parameters  
 The following additional parameters may be specified on the request URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`timeout`|Optional. The `timeout` parameter is expressed in seconds. For more information, see [Setting Timeouts for File Service Operations](../StorageServicesREST/Setting-Timeouts-for-File-Service-Operations.md).|  
  
### Request Body  
 None.  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) time for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Required for all authenticated requests. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-meta-name:value`|Optional. Version 2015-02-21 and newer. A name-value pair to associate with the directory as metadata.<br /><br /> Metadata names must adhere to the naming rules for [C# identifiers](http://msdn.microsoft.com/en-us/library/aa664670\(VS.71\).aspx).|  
  
### Sample Request  
  
```  
PUT https://myaccount.file.core.windows.net/myshare/myparentdirectorypath/mydirectory? restype=directory HTTP/1.1  
  
Request Headers:  
x-ms-version: 2014-02-14  
x-ms-date: Mon, 27 Jan 2014 22:50:32 GMT  
x-ms-meta-Category: Images  
Authorization: SharedKey myaccount:Z5043vY9MesKNh0PNtksNc9nbXSSqGHueE00JdjidOQ=  
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
|`ETag`|The ETag contains a value which represents the version of the directory, in quotes.|  
|`Last-Modified`|Returns the date and time the directory was last modified. The date format follows RFC 1123. For more information, see [Representation of Date/Time Values in Headers](http://msdn.microsoft.com/library/windowsazure/dd135714). Any operation that modifies the directory or its properties updates the last modified time. Operations on files do not affect the last modified time of the directory.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](http://msdn.microsoft.com/library/windowsazure/dd573365).|  
|`x-ms-version`|Indicates the version of the Azure File service used to execute the request.|  
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
 If a directory by the same name is being deleted when `Create Directory` is called, the server will return status code 409 (Conflict), with additional error information indicating that the directory is being deleted.  
  
 If a directory or file with the same name already exists, the operation fails with status code 409 (Conflict). If the parent directory does not exist, then the operation fails with status code 412 (Precondition Failed).  
  
 It is not possible to create a directory hierarchy with a single `Create Directory` operation. The directory will only be created if its immediate parent already exists, as specified in the path. If the parent directory does not exist, then the operation fails with status code 412 (Precondition Failed).  
  
## See Also  
 [Operations on Directories](../StorageServicesREST/Operations-on-Directories.md)
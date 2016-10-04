---
title: "Set File Properties"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 815e53d3-ffc5-45aa-a367-3c1bcf5b66eb
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
# Set File Properties
The `Set File Properties` operation sets system properties on the file.  
  
## Request  
 The `Set File Properties` request may be constructed as follows. HTTPS is recommended.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|PUT|`https://myaccount.file.core.windows.net/myshare/mydirectorypath/myfile?comp=properties`|HTTP/1.1|  
  
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
|`x-ms-cache-control`|Optional. Modifies the cache control string for the file.<br /><br /> If this property is not specified on the request, then the property will be cleared for the file. Subsequent calls to [Get File Properties](../StorageServicesREST/Get-File-Properties.md) will not return this property, unless it is explicitly set on the file again.|  
|`x-ms-content-type`|Optional. Sets the file's content type.<br /><br /> If this property is not specified on the request, then the property will be cleared for the file. Subsequent calls to [Get File Properties](../StorageServicesREST/Get-File-Properties.md) will not return this property, unless it is explicitly set on the file again.|  
|`x-ms-content-md5`|Optional. Sets the file's MD5 hash.<br /><br /> If this property is not specified on the request, then the property will be cleared for the file. Subsequent calls to [Get File Properties](../StorageServicesREST/Get-File-Properties.md) will not return this property, unless it is explicitly set on the file again.|  
|`x-ms-content-encoding`|Optional. Sets the file's content encoding.<br /><br /> If this property is not specified on the request, then the property will be cleared for the file. Subsequent calls to [Get File Properties](../StorageServicesREST/Get-File-Properties.md) will not return this property, unless it is explicitly set on the file again.|  
|`x-ms-content-language`|Optional. Sets the file's content language.<br /><br /> If this property is not specified on the request, then the property will be cleared for the file. Subsequent calls to [Get File Properties](../StorageServicesREST/Get-File-Properties.md) will not return this property, unless it is explicitly set on the file again.|  
|`x-ms-content-disposition`|Optional. Sets the file’s `Content-Disposition` header.<br /><br /> If this property is not specified on the request, then the property will be cleared for the file. Subsequent calls to [Get File Properties](../StorageServicesREST/Get-File-Properties.md) will not return this property, unless it is explicitly set on the file again.|  
|`x-ms-content-length: bytes`|Optional. Resizes a file to the specified size. If the specified byte value is less than the current size of the file, then all ranges above the specified byte value are cleared.|  
  
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
|`ETag`|The ETag contains a value which represents the version of the file, in quotes.|  
|`Last-Modified`|Returns the date and time the directory was last modified. The date format follows RFC 1123. For more information, see [Representation of Date-Time Values in Headers](../StorageServicesREST/Representation-of-Date-Time-Values-in-Headers.md). Any operation that modifies the directory or its properties updates the last modified time. Operations on files do not affect the last modified time of the directory.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the File service used to execute the request.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
### Response Body  
 None.  
  
## Authorization  
 Only the account owner may call this operation.  
  
## Remarks  
 The semantics for updating a file's properties are as follows:  
  
-   A file's size is modified only if the request specifies a value for the `x-ms-content-length` header.  
  
-   If a request sets only `x-ms-content-length`, and no other properties, then none of the file’s other properties are modified.  
  
-   If any one or more of the following properties is set in the request, then all of these properties are set together. If a value is not provided for a given property when at least one of the properties listed below is set, then that property will be cleared for the file.  
  
    -   `x-ms-cache-control`  
  
    -   `x-ms-content-type`  
  
    -   `x-ms-content-md5`  
  
    -   `x-ms-content-encoding`  
  
    -   `x-ms-content-language`  
  
> [!NOTE]
>  The file properties listed above are discrete from the file system properties available to SMB clients. SMB clients cannot read, write, or modify these property values.  
  
## See Also  
 [Operations on Files](../StorageServicesREST/Operations-on-Files.md)
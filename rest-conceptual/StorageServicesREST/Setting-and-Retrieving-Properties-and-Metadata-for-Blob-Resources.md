---
title: "Setting and Retrieving Properties and Metadata for Blob Resources"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 6b4bbda5-bc05-492a-8b8e-0ed39925fd9c
caps.latest.revision: 32
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
# Setting and Retrieving Properties and Metadata for Blob Resources
Containers and blobs support custom metadata, represented as HTTP headers. Metadata headers can be set on a request that creates a new container or blob resource, or on a request that explicitly creates a property on an existing resource.  
  
 This topic contains the following subtopics:  
  
 [Metadata Header Format](#Subheading1)  
  
 [Operations on Metadata](#Subheading2)  
  
 [Standard HTTP Properties for Containers and Blobs](#Subheading3)  
  
##  <a name="Subheading1"></a> Metadata Header Format  
 Metadata headers are name/value pairs. The format for the header is:  
  
```  
x-ms-meta-name:string-value  
```  
  
 Beginning with version 2009-09-19, metadata names must adhere to the naming rules for [C# identifiers](http://msdn.microsoft.com/library/aa664670\(VS.71\).aspx).  
  
 Names are case-insensitive. Note that metadata names preserve the case with which they were created, but are case-insensitive when set or read. If two or more metadata headers with the same name are submitted for a resource, the Blob service returns status code 400 (Bad Request).  
  
 The total size of the metadata, including both the name and value together, may not exceed 8 KB in size.  
  
 Metadata name/value pairs are valid HTTP headers, and so they adhere to all restrictions governing HTTP headers.  
  
##  <a name="Subheading2"></a> Operations on Metadata  
 Metadata on a blob or container resource can be retrieved or set directly, without returning or altering the content of the resource.  
  
 Note that metadata values can only be read or written in full; partial updates are not supported. Setting metadata on a resource overwrites any existing metadata values for that resource.  
  
### Retrieving Properties and Metadata  
 The GET and HEAD operations both retrieve metadata headers for the specified container or blob. These operations return headers only; they do not return a response body.  
  
 The URI syntax for retrieving metadata headers on a container is as follows:  
  
```  
GET/HEAD https://myaccount.blob.core.windows.net/mycontainer?restype=container  
```  
  
 The URI syntax for retrieving metadata headers on a blob is as follows:  
  
```  
GET/HEAD https://myaccount.blob.core.windows.net/mycontainer/myblob?comp=metadata  
```  
  
### Setting Metadata Headers  
 The PUT operation sets metadata headers on the specified container or blob, overwriting any existing metadata on the resource. Calling PUT without any headers on the request clears all existing metadata on the resource.  
  
 The URI syntax for setting metadata headers on a container is as follows:  
  
```  
PUT https://myaccount.blob.core.windows.net/mycontainer?comp=metadata?restype=container  
```  
  
 The URI syntax for setting metadata headers on a blob is as follows:  
  
```  
PUT https://myaccount.blob.core.windows.net/mycontainer/myblob?comp=metadata  
```  
  
##  <a name="Subheading3"></a> Standard HTTP Properties for Containers and Blobs  
 Containers and blobs also support certain standard HTTP properties. Properties and metadata are both represented as standard HTTP headers; the difference between them is in the naming of the headers. Metadata headers are named with the header prefix `x-ms-meta-` and a custom name. Property headers use standard HTTP header names, as specified in the Header Field Definitions section 14 of the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?LinkId=1762).  
  
 The standard HTTP headers supported on containers include:  
  
-   `ETag`  
  
-   `Last-Modified`  
  
 The standard HTTP headers supported on blobs include:  
  
-   `ETag`  
  
-   `Last-Modified`  
  
-   `Content-Length`  
  
-   `Content-Type`  
  
-   `Content-MD5`  
  
-   `Content-Encoding`  
  
-   `Content-Language`  
  
-   `Cache-Control`  
  
-   `Origin`  
  
-   `Range`  
  
## See Also  
 [Create Container](../StorageServicesREST/Create-Container.md)   
 [Get Container Properties](../StorageServicesREST/Get-Container-Properties.md)   
 [Set Container Metadata](../StorageServicesREST/Set-Container-Metadata.md)   
 [Put Blob](../StorageServicesREST/Put-Blob.md)   
 [Copy Blob](../StorageServicesREST/Copy-Blob.md)   
 [Get Blob Properties](../StorageServicesREST/Get-Blob-Properties.md)   
 [Get Blob Metadata](../StorageServicesREST/Get-Blob-Metadata.md)   
 [Set Blob Metadata](../StorageServicesREST/Set-Blob-Metadata.md)   
 [Blob Service Concepts](../StorageServicesREST/Blob-Service-Concepts.md)
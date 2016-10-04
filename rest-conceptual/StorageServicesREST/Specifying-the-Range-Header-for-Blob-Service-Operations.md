---
title: "Specifying the Range Header for Blob Service Operations"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 8087cabc-5e40-4def-8790-a97a20448946
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
# Specifying the Range Header for Blob Service Operations
Several Blob service GET operations support the use of the standard HTTP `Range` header. Many HTTP clients, including the .NET client library, limit the size of the `Range` header to a 32-bit integer, and thus its value is limited to a maximum of 4 GB. Since both block blobs and page blobs can be larger than 4 GB in size, the Blob service accepts a custom range header `x-ms-range` for any operation that takes an HTTP `Range` header.  
  
 Some HTTP clients, including the Microsoft Silverlight library, limit access to the `Range` header altogether. The `x-ms-range` header can be used to circumvent these limitations as well.  
  
 If the `x-ms-range` header is specified on a request, then the service uses the range specified by `x-ms-range`; otherwise, the range specified by the `Range` header is used.  
  
> [!NOTE]
>  The Azure Storage Client Library automatically handles setting the appropriate range header on the request when you set the `Range` property of the `PutPageProperties` object.  
  
## Range Header Formats  
 The Blob service accepts two byte ranges for the `Range` and `x-ms-range` headers. The byte range must adhere to either of the following formats for the headers:  
  
-   `bytes=startByte-` for requests using version 2011-08-18 or newer  
  
-   `bytes=startByte-endByte` for requests using all versions (2009-04-14 through the newest version)  
  
### Format 1: bytes=startByte-  
 The first format, `bytes=startByte-`, is available only for requests using version 2011-08-18 or newer, or the storage emulator service in SDK 1.6 or newer. This range will return bytes from the offset `startByte` through the end of the blob. For example, to specify a range encompassing all bytes after the first 256 bytes of a blob, you can pass in either of the following headers:  
  
-   `Range: bytes=255-`  
  
-   `x-ms-range: bytes=255-`  
  
 The `Content-Length` header in the response is equal to the number of bytes from the offset until the end of the blob. Using the example range above for a blob of 1,024 bytes in length, `Content-Length` would be 756.  
  
 If the offset is valid and does not exceed the blob’s total length, the request will return an status code 206 (Partial Content). If the offset is invalid and exceeds the blob’s total length, the request will return status code 416 (Requested Range Not Satisfiable).  
  
### Format 2: bytes=startByte-endByte  
 The second format, `bytes=startByte-endByte`, is available for requests using all versions (2009-04-14 through the newest version), and for all versions of the storage emulator service. This range will return bytes from the offset `startByte` through `endByte`. For example, to specify a range encompassing the first 512 bytes of a blob, you would pass in either of the following headers:  
  
-   `Range: bytes=0-511`  
  
-   `x-ms-range: bytes=0-511`  
  
 The `Content-Length` header in the response is equal to the number of bytes between each offset. Using the example range above for a blob of 1,024 bytes in length, `Content-Length` would be 512.  
  
 If the offset is valid and does not exceed the blob’s total length, the request will return an status code 206 (Partial Content). If the offset is invalid and exceeds the blob’s total length, the request will return status code 416 (Requested Range Not Satisfiable).  
  
## See Also  
 [Blob Service Concepts](../StorageServicesREST/Blob-Service-Concepts.md)   
 [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md)
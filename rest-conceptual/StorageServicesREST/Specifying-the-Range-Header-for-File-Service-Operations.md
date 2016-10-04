---
title: "Specifying the Range Header for File Service Operations"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 824245eb-02aa-4717-980c-e1f6c7d39ba4
caps.latest.revision: 5
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
# Specifying the Range Header for File Service Operations
Some File service GET operations support the use of the standard HTTP `Range` header. Many HTTP clients, including the .NET client library, limit the size of the `Range` header to a 32-bit integer, and thus its value is limited to a maximum of 4 GB. Since files can be larger than 4 GB in size, the File service accepts a custom range header `x-ms-range` for any operation that takes an HTTP `Range` header.  
  
 Some HTTP clients, including the Microsoft Silverlight library, limit access to the `Range` header altogether. The `x-ms-range` header can be used to circumvent these limitations as well.  
  
 If the `x-ms-range` header is specified on a request, then the service uses the range specified by `x-ms-range`; otherwise, the range specified by the `Range` header is used.  
  
## Range Header Formats  
 The File service accepts two byte ranges for the `Range` and `x-ms-range` headers. The byte range must adhere to either of the following formats for the headers:  
  
-   `bytes=startByte-`  
  
-   `bytes=startByte-endByte`  
  
### Format 1: bytes=startByte-  
 This range will return bytes from the offset `startByte` through the end of the file. For example, to specify a range encompassing all bytes after the first 256 bytes of a file, you can pass in either of the following headers:  
  
-   `Range: bytes=255-`  
  
-   `x-ms-range: bytes=255-`  
  
 The `Content-Length` header in the response is equal to the number of bytes from the offset until the end of the file. Using the example range above for a file of 1,024 bytes in length, `Content-Length` would be 756.  
  
 If the offset is valid and does not exceed the file’s total length, the request will return an status code 206 (Partial Content). If the offset is invalid and exceeds the file’s total length, the request will return status code 416 (Requested Range Not Satisfiable).  
  
### Format 2: bytes=startByte-endByte  
 This range will return bytes from the offset `startByte` through `endByte`. For example, to specify a range encompassing the first 512 bytes of a file, you would pass in either of the following headers:  
  
-   `Range: bytes=0-511`  
  
-   `x-ms-range: bytes=0-511`  
  
 The `Content-Length` header in the response is equal to the number of bytes between each offset. Using the example range above for a file of 1,024 bytes in length, `Content-Length` would be 512.  
  
 If the offset is valid and does not exceed the file’s total length, the request will return an status code 206 (Partial Content). If the offset is invalid and exceeds the file’s total length, the request will return status code 416 (Requested Range Not Satisfiable).  
  
## See Also  
 [File Service Concepts](../StorageServicesREST/File-Service-Concepts.md)
---
title: "Versioning Best Practices"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 173a9a62-a225-4184-ab3a-c7faf35a16fd
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
# Versioning Best Practices
We recommend the following versioning best practices for the Azure storage services:  
  
-   Explicitly specify the REST protocol version to use for every authenticated request.  
  
-   Set a default version for the Blob service using the [Set Blob Service Properties](../StorageServicesREST/Set-Blob-Service-Properties.md) operation. The default version specifies the version to use for anonymous requests for which the version header cannot be set.  
  
-   Client software that uses a shared access signature (SAS) URL to access storage resources may experience unexpected behavior when the SAS URL specifies a storage service version that is newer than that used by the client software. We recommend the following to ensure clients work well with SAS tokens:  
  
    -   For version 2014-02-14 and later, SAS token consumers using the REST API can override the REST protocol version to specify the appropriate version using the `api-version` parameter. See [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md) for details.  
  
         For SAS token consumers using the Storage Client Library, the library ensures that the correct REST protocol version is requested.  
  
    -   For version 2013-08-15 and earlier, code that prepares and distributes shared access signature URLs (*i.e.*, SAS providers or generators) should specify versions that are understood by client software (*i.e.*, SAS consumers) that makes storage service requests.  
  
-   Always use the latest storage service version to benefit from optimizations included with each new version. Some examples of such changes include:  
  
    -   Version 2013-08-15 introduced the JSON payload format that reduces network bandwidth usage by up to 70% compared to OData’s AtomPub protocol.  
  
    -   Version 2013-08-15 allows SAS providers and generators to add certain response headers like `cache-control`, `content-disposition`, and `content-type` via SAS query parameters.  
  
    -   Version 2011-08-18 introduced the quoted `ETag` and `Accept-Ranges` response headers required for optimized download and streaming via browsers.  
  
## See Also  
 [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md)
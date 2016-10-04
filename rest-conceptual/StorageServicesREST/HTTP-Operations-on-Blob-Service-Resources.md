---
title: "HTTP Operations on Blob Service Resources"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: f156bcbb-692c-496f-9c31-92a297896278
caps.latest.revision: 34
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
# HTTP Operations on Blob Service Resources
The Blob service exposes the following resource types via the REST API:  
  
-   **Account.** A storage account is a globally uniquely identified entity within the storage system. The account is the parent namespace for the Blob service. All containers are associated with an account.  
  
-   **Containers.** A container is a user-defined set of blobs within an account. A container resource has no associated content, only properties and metadata.  
  
-   **Blobs.** A blob is an entity representing a set of content. A blob resource includes content, properties, and metadata.  
  
 You can address each resource using its resource URI. For information about URI addresses, see [Referring to Containers and Blobs](assetId:///71b719e2-1ade-43fe-adcd-42b7b2ec011f).  
  
 Each resource supports operations based on the HTTP verbs GET, PUT, HEAD, and DELETE. The verb, syntax, and supported HTTP version(s) for each operation appears on the reference page for each operation. For a complete list of operation reference pages, see [Blob Service REST API](../StorageServicesREST/Blob-Service-REST-API.md).  
  
## See Also  
 [Naming and Referencing Containers, Blobs, and Metadata](../StorageServicesREST/Naming-and-Referencing-Containers--Blobs--and-Metadata.md)   
 [Working with the Root Container](../StorageServicesREST/Working-with-the-Root-Container.md)   
 [Operations on Containers](../StorageServicesREST/Operations-on-Containers.md)   
 [Operations on Blobs](../StorageServicesREST/Operations-on-Blobs.md)   
 [Blob Service Concepts](../StorageServicesREST/Blob-Service-Concepts.md)   
 [Blob Service REST API](../StorageServicesREST/Blob-Service-REST-API.md)
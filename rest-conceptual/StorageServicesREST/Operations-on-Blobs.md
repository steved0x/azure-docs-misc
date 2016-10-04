---
title: "Operations on Blobs"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 3e6953ca-5655-4e29-a398-5b119668c00e
caps.latest.revision: 28
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
# Operations on Blobs
Microsoft Azure Storage provides REST operations for working with blobs in the Blob service.  
  
## In This Section  
 This section contains reference information for operations on block blobs, append blobs and page blobs.  
  
### Operations on Block Blobs, Append Blobs and Page Blobs  
 [Put Blob](../StorageServicesREST/Put-Blob.md)  
 Creates a new blob or replaces an existing blob within a container.  
  
 [Get Blob](../StorageServicesREST/Get-Blob.md)  
 Reads or download a blob from the Blob service, including its user-defined metadata and system properties.  
  
 [Get Blob Properties](../StorageServicesREST/Get-Blob-Properties.md)  
 Returns all user-defined metadata, standard HTTP properties, and system properties for the blob.  
  
 [Set Blob Properties](../StorageServicesREST/Set-Blob-Properties.md)  
 Sets values for system properties defined for a blob.  
  
 [Get Blob Metadata](../StorageServicesREST/Get-Blob-Metadata.md)  
 Returns all user-defined metadata for the specified blob.  
  
 [Set Blob Metadata](../StorageServicesREST/Set-Blob-Metadata.md)  
 Sets user-defined metadata for the specified blob as one or more name-value pairs.  
  
 [Lease Blob](../StorageServicesREST/Lease-Blob.md)  
 Establishes and manages a lock on write and delete operations. To delete or write to a locked blob, a client must provide the lease ID.  
  
 [Snapshot Blob](../StorageServicesREST/Snapshot-Blob.md)  
 Creates a snapshot of a blob.  
  
 [Copy Blob](../StorageServicesREST/Copy-Blob.md)  
 Copies a blob to a destination within the storage account.  
  
 [Abort Copy Blob](../StorageServicesREST/Abort-Copy-Blob.md)  
 Aborts a pending `Copy Blob` operation, and leaves a destination blob with zero length and full metadata.  
  
 [Delete Blob](../StorageServicesREST/Delete-Blob.md)  
 Marks the specified blob for deletion.  
  
### Operations on Block Blobs  
 [Put Block](../StorageServicesREST/Put-Block.md)  
 Creates a new block to be committed as part of a block blob.  
  
 [Put Block List](../StorageServicesREST/Put-Block-List.md)  
 Commits a block blob by specifying the set of block IDs that comprise the blob.  
  
 [Get Block List](../StorageServicesREST/Get-Block-List.md)  
 Retrieves the list of blocks that have been uploaded as part of a block blob.  
  
### Operations on Page Blobs  
 [Put Page](../StorageServicesREST/Put-Page.md)  
 Writes a range of pages into a page blob.  
  
 [Get Page Ranges](../StorageServicesREST/Get-Page-Ranges.md)  
 Returns a list of valid page ranges for a page blob or a snapshot of a page blob.  
  
### Operations on Append Blobs  
 [Append Block](../StorageServicesREST/Append-Block.md)  
 Writes a range of pages into a page blob.  
  
## See Also  
 [Blob Service Concepts](../StorageServicesREST/Blob-Service-Concepts.md)
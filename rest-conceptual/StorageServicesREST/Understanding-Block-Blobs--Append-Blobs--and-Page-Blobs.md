---
title: "Understanding Block Blobs, Append Blobs, and Page Blobs"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 2de10e66-46cd-4bbe-98ec-aba34bf22c4d
caps.latest.revision: 38
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
# Understanding Block Blobs, Append Blobs, and Page Blobs
The storage service offers three types of blobs, *block blobs*, *append blobs*, and *page blobs*. You specify the blob type when you create the blob. Once the blob has been created, its type cannot be changed, and it can be updated only by using operations appropriate for that blob type, *i.e.*, writing a block or list of blocks to a block blob, appending blocks to a append blob, and writing pages to a page blob.  
  
 All blobs reflect committed changes immediately. Each version of the blob has a unique tag, called an *ETag*, that you can use with access conditions to assure you only change a specific instance of the blob.  
  
 Any blob can be leased for exclusive write access. When a blob is leased, only calls that include the current lease ID can modify the blob or (for block blobs) its blocks.  
  
 Any blob can be duplicated in a snapshot. For information about snapshots, see [Creating a Snapshot of a Blob](../StorageServicesREST/Creating-a-Snapshot-of-a-Blob.md).  
  
> [!NOTE]
>  Blobs in the Azure storage emulator are limited to 2 GB.  
  
## About Block Blobs  
 Block blobs let you upload large blobs efficiently. Block blobs are comprised of blocks, each of which is identified by a block ID. You create or modify a block blob by writing a set of blocks and committing them by their block IDs. Each block can be a different size, up to a maximum of 4 MB, and a block blob can include up to 50,000 blocks. The maximum size of a block blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks). If you are writing a block blob that is no more than 64 MB in size, you can upload it in its entirety with a single write operation; see [Put Blob](../StorageServicesREST/Put-Blob.md).  
  
 Storage clients default to a 32 MB maximum single block upload, settable using the <xref:Microsoft.WindowsAzure.StorageClient.CloudBlobClient.?qualifyHint=False> SingleBlobUploadThresholdInBytes?qualifyHint=False&autoUpgrade=False property. When a block blob upload is larger than the value in this property, storage clients break the file into blocks. You can set the number of threads used to upload the blocks in parallel using the <xref:Microsoft.WindowsAzure.StorageClient.CloudBlobClient.?qualifyHint=False> ParallelOperationThreadCount?qualifyHint=False&autoUpgrade=False property.  
  
 When you upload a block to a blob in your storage account, it is associated with the specified block blob, but it does not become part of the blob until you commit a list of blocks that includes the new block's ID. New blocks remain in an uncommitted state until they are specifically committed or discarded. Writing a block does not update the last modified time of an existing blob.  
  
 Block blobs include features that help you manage large files over networks. With a block blob, you can upload multiple blocks in parallel to decrease upload time. Each block can include an MD5 hash to verify the transfer, so you can track upload progress and re-send blocks as needed. You can upload blocks in any order, and determine their sequence in the final block list commitment step. You can also upload a new block to replace an existing uncommitted block of the same block ID. You have one week to commit blocks to a blob before they are discarded. All uncommitted blocks are also discarded when a block list commitment operation occurs but does not include them.  
  
 You can modify an existing block blob by inserting, replacing, or deleting existing blocks. After uploading the block or blocks that have changed, you can commit a new version of the blob by committing the new blocks with the existing blocks you want to keep using a single commit operation. To insert the same range of bytes in two different locations of the committed blob, you can commit the same block in two places within the same commit operation. For any commit operation, if any block is not found, the entire commitment operation fails with an error, and the blob is not modified. Any block commitment overwrites the blob’s existing properties and metadata, and discards all uncommitted blocks.  
  
 Block IDs are strings of equal length within a blob. Block client code usually uses base-64 encoding to normalize strings into equal lengths. When using base-64 encoding, the pre-encoded string must be 64 bytes or less. Block ID values can be duplicated in different blobs. A blob can have up to 100,000 uncommitted blocks, but their total size cannot exceed 200,000 MB.  
  
 If you write a block for a blob that does not exist, a new block blob is created, with a length of zero bytes. This blob will appear in blob lists that include uncommitted blobs. If you don’t commit any block to this blob, it and its uncommitted blocks will be discarded one week after the last successful block upload. All uncommitted blocks are also discarded when a new blob of the same name is created using a single step (rather than the two-step block upload-then-commit process).  
  
## About Page Blobs  
 Page blobs are a collection of 512-byte pages optimized for random read and write operations. To create a page blob, you initialize the page blob and specify the maximum size the page blob will grow. To add or update the contents of a page blob, you write a page or pages by specifying an offset and a range that align to 512-byte page boundaries. A write to a page blob can overwrite just one page, some pages, or up to 4 MB of the page blob. Writes to page blobs happen in-place and are immediately committed to the blob. The maximum size for a page blob is 1 TB.  
  
 With the introduction of new Premium Storage, Microsoft Azure now offers two types of durable storage: **Premium Storage** and **Standard Storage**. Premium Storage is specifically designed for Azure Virtual Machine workloads requiring consistent high performance and low latency. Premium Storage is currently available only for storing data on disks used by Azure Virtual Machines. These disks are backed by page blobs in Azure Storage. For detailed information, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](http://go.microsoft.com/fwlink/?LinkId=521898). For information on the scalability targets for Premium Storage, see [Azure Storage Scalability and Performance Targets](assetId:///26df4d89-8289-4b31-aaa0-df971cab9b52).  
  
## About Append Blobs  
 An append blob is comprised of blocks and is optimized for append operations. When you modify an append blob, blocks are added to the end of the blob only, via the [Append Block](../StorageServicesREST/Append-Block.md) operation. Updating or deleting of existing blocks is not supported. Unlike a block blob, an append blob does not expose its block IDs.  
  
 Each block in an append blob can be a different size, up to a maximum of 4 MB, and an append blob can include up to 50,000 blocks. The maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).  
  
## See Also  
 [How to Use the Blob Storage Service](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)   
 [How to Use the Queue Storage Service](http://www.windowsazure.com/develop/net/how-to-guides/queue-service/)
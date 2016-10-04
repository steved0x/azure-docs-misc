---
title: "Creating a Snapshot of a Blob"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 5614e5d3-58cb-42ee-9db6-d90de86196cd
caps.latest.revision: 24
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
# Creating a Snapshot of a Blob
You can create a snapshot of a blob. A snapshot is a read-only version of a blob that's taken at a point in time. Once a snapshot has been created, it can be read, copied, or deleted, but not modified. Snapshots provide a way to back up a blob as it appears at a moment in time.  
  
 A snapshot of a blob has the same name as the base blob from which the snapshot is taken, with a `DateTime` value appended to indicate the time at which the snapshot was taken. For example, if the page blob URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, the snapshot URI will be similar to `http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`. This value may be used to reference the snapshot for further operations. A blob's snapshots share its URI and are distinguished only by this `DateTime` value. In client library code, the blob's <xref:Microsoft.WindowsAzure.StorageClient.BlobAttributes.Snapshot?qualifyHint=False> property returns a `DateTime` value that uniquely identifies the snapshot relative to its base blob. You can use this value to perform further operations on the snapshot.  
  
 A blob may have any number of snapshots. Snapshots persist until they are explicitly deleted A snapshot cannot outlive its source blob. You can enumerate the snapshots associated with your blob to track your current snapshots.  
  
 **Inheriting Properties**  
  
 When you create a snapshot of a blob, system properties are copied to the snapshot with the same values. This list shows copied system properties for the .NET storage client library:  
  
-   <xref:Microsoft.WindowsAzure.StorageClient.BlobProperties.ContentType?qualifyHint=False>  
  
-   <xref:Microsoft.WindowsAzure.StorageClient.BlobProperties.ContentEncoding?qualifyHint=False>  
  
-   <xref:Microsoft.WindowsAzure.StorageClient.BlobProperties.ContentLanguage?qualifyHint=False>  
  
-   <xref:Microsoft.WindowsAzure.StorageClient.BlobProperties.Length?qualifyHint=False>  
  
-   <xref:Microsoft.WindowsAzure.StorageClient.BlobProperties.CacheControl?qualifyHint=False>  
  
-   <xref:Microsoft.WindowsAzure.StorageClient.BlobProperties.ContentMd5?qualifyHint=False>  
  
 A lease associated with the base blob is not copied to the snapshot. Snapshots cannot be leased.  
  
 **Copying Snapshots**  
  
 Copy operations involving blobs and snapshots follow these rules:  
  
-   You can copy a snapshot over its base blob. By promoting a snapshot to the position of the base blob, you can restore an earlier version of a blob. The snapshot remains, but its source is overwritten with a copy that can be both read and written.  
  
-   You can copy a snapshot to a destination blob with a different name. The resulting destination blob is a writeable blob and not a snapshot.  
  
-   When a source blob is copied, any snapshots of the source blob are not copied to the destination. When a destination blob is overwritten with a copy, any snapshots associated with the destination blob stay intact under its name.  
  
-   When you create a snapshot of a block blob, the blob's committed block list is also copied to the snapshot. Any uncommitted blocks are not copied.  
  
 **Specifying an Access Condition**  
  
 You can specify an access condition so that the snapshot is created only if a condition is met. To specify an access condition, use the <xref:Microsoft.WindowsAzure.StorageClient.BlobRequestOptions.AccessCondition?qualifyHint=False> property. If the specified condition is not met, the snapshot is not created, and the Blob service returns status code [HTTPStatusCode.PreconditionFailed](http://msdn.microsoft.com/library/system.net.httpstatuscode.aspx).  
  
 **Deleting Snapshots**  
  
 A blob that has snapshots cannot be deleted unless the snapshots are also deleted. You can delete a snapshot individually, or tell the storage service to delete all snapshots when deleting the source blob. If you attempt to delete a blob that still has snapshots, your call will return an error.  
  
 **Constructing the Absolute URI to a Snapshot**  
  
 This code example constructs the absolute URI of a snapshot from its base blob object.  
  
```c#  
var snapshot = blob.CreateSnapshot();  
var uri = Microsoft.WindowsAzure.StorageClient.Protocol.BlobRequest.Get  
    (snapshot.Uri,   
    0,   
    snapshot.SnapshotTime.Value,   
    null).Address.AbsoluteUri;  
```  
  
## See Also  
 <xref:Microsoft.WindowsAzure.StorageClient.CloudBlob.CreateSnapshot?qualifyHint=False>   
 <xref:Microsoft.WindowsAzure.StorageClient.CloudDrive.Snapshot?qualifyHint=False>   
 <xref:Microsoft.WindowsAzure.StorageClient.CloudBlob.SnapshotTime?qualifyHint=False>   
 [Snapshot Blob](../StorageServicesREST/Snapshot-Blob.md)   
 [Put Block](../StorageServicesREST/Put-Block.md)   
 [Put Block List](../StorageServicesREST/Put-Block-List.md)   
 [Put Page](../StorageServicesREST/Put-Page.md)   
 [Delete Blob](../StorageServicesREST/Delete-Blob.md)   
 [Enumerating Blob Resources](../StorageServicesREST/Enumerating-Blob-Resources.md)   
 [Understanding How Snapshots Accrue Charges](../StorageServicesREST/Understanding-How-Snapshots-Accrue-Charges.md)
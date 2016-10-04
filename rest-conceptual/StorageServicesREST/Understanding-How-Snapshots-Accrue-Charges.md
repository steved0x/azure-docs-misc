---
title: "Understanding How Snapshots Accrue Charges"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 1f59392b-419a-4436-895e-1025a55ae70c
caps.latest.revision: 11
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
# Understanding How Snapshots Accrue Charges
Creating a snapshot, which is a read-only copy of a blob, can result in additional data storage charges to your account. When designing your application, it is important to be aware how these charges may accrue so that you can minimize unnecessary costs.  
  
## Important Billing Considerations  
 The following list includes key points to consider when creating a snapshot.  
  
-   Charges are incurred for unique blocks or pages, whether they are in the blob or in the snapshot. Your account does not incur additional charges for snapshots associated with a blob until you update the blob on which they are based. Once you update the base blob, it diverges from its snapshots, and you will be charged for the unique blocks or pages in each blob or snapshot.  
  
-   When you replace a block within a block blob, that block is subsequently charged as a unique block. This is true even if the block has the same block ID and the same data as it has in the snapshot. Once the block is committed again, it diverges from its counterpart in any snapshot, and you will be charged for its data. The same holds true for a page in a page blob that’s updated with identical data.  
  
-   Replacing a block blob by calling the **UploadFile**, **UploadText**, **UploadStream**, or **UploadByteArray** method replaces all of the blocks in that blob. If you have a snapshot associated with that blob, all of the blocks in the base blob and snapshot will now diverge and you will be charged for all of the blocks in both blobs. This is true even if the data in the base blob and the snapshot remain identical.  
  
-   The Azure Blob service does not have a means to determine whether two blocks contain identical data. Each block that is uploaded and committed is treated as unique, even if it has the same data and the same block ID. Because charges accrue for unique blocks, it is important to consider that updating a blob that has a snapshot will result in additional unique blocks and additional charges.  
  
> [!IMPORTANT]
>  Best practices dictate that you manage snapshots carefully to avoid extra charges. It’s recommended that you manage snapshots in the following manner:  
>   
>  -   Delete and re-create snapshots associated with a blob whenever you update the blob, even if you are updating with identical data, unless your application design requires that you maintain snapshots. By deleting and re-creating the blob’s snapshots, you can ensure that the blob and snapshots do not diverge.  
> -   If you are maintaining snapshots for a blob, avoid calling **UploadFile**, **UploadText**, **UploadStream**, or **UploadByteArray** to update the blob, as those methods replace all of the blocks in the blob. Instead, update the fewest possible number of blocks by using the **PutBlock** and **PutBlockList** methods.  
  
## Snapshot Billing Scenarios  
 The following scenarios demonstrate how charges accrue for a block blob and its snapshots. In Scenario 1, the base blob has not been updated since the snapshot was taken, so charges are incurred only for unique blocks 1, 2, and 3:  
  
 ![WA&#95;SnapshotScenario1](../StorageServicesREST/media/WA_SnapshotScenario1.png "WA_SnapshotScenario1")  
Scenario 1: Only blocks 1, 2, and 3 accrue charges.  
  
 In Scenario 2, the base blob has been updated, but the snapshot has not. Block 3 was updated, and even though it contains the same data and the same ID, it is not the same as block 3 in the snapshot. As a result, the account is charged for four blocks:  
  
 ![WA&#95;SnapshotScenario2](../StorageServicesREST/media/WA_SnapshotScenario2.png "WA_SnapshotScenario2")  
Scenario 2: Blocks 1, 2, and 3 in the base blob accrue charges, along with block 3 in the snapshot.  
  
 In Scenario 3, the base blob has been updated, but the snapshot has not. Block 3 was replaced with block 4 in the base blob, but the snapshot still reflects block 3. As a result, the account is charged for four blocks:  
  
 ![WA&#95;SnapshotScenario3](../StorageServicesREST/media/WA_SnapshotScenario3.png "WA_SnapshotScenario3")  
Scenario 3: Blocks 1, 2, 3, and 4 accrue charges.  
  
 In Scenario 4, the base blob has been completely updated and contains none of its original blocks. As a result, the account is charged for all eight unique blocks. This scenario can occur if you are using an update method such as **UploadFile**, **UploadText**, **UploadFromStream**, or **UploadByteArray**, because these methods replace all of the contents of a blob.  
  
 ![WA&#95;SnapshotScenario4](../StorageServicesREST/media/WA_SnapshotScenario4.png "WA_SnapshotScenario4")  
Scenario 4: Blocks 1, 2, 3, 4, 5, 6, 7, and 8 accrue charges.  
  
## See Also  
 [How to Use the Blob Storage Service](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)   
 [How to Use the Queue Storage Service](http://www.windowsazure.com/develop/net/how-to-guides/queue-service/)   
 [Creating a Snapshot of a Blob](../StorageServicesREST/Creating-a-Snapshot-of-a-Blob.md)
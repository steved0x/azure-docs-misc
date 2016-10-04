---
title: "Cancelling and Deleting Jobs"
ms.custom: na
ms.date: 05/25/2015
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: fd3d66f0-1dbb-4c75-9223-307d5abaeefc
caps.latest.revision: 8
author: tamram
manager: adinah
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
# Cancelling and Deleting Jobs
You can request that a job be cancelled before it is in the `Packaging` state by calling the [Update Job Properties](../StorageImportExportREST/Update-Job-Properties.md) operation and setting the `CancelRequested` element to `true`. The job will be cancelled on a best-effort basis. If drives are in the process of transferring data, data may continue to be transferred even after cancellation has been requested.  
  
 A cancelled job will move to the `Completed` state and be kept for 90 days, at which point it will be deleted.  
  
 To delete a job, call the [Delete Job](../StorageImportExportREST/Delete-Job1.md) operation before the job has shipped (*i.e.*, while the job is in the `Creating` state). You can also delete a job when it is in the `Completed` state. After a job has been deleted, its information and status are no longer accessible via the REST API or the Azure Management Portal.  
  
## See Also  
 [Using the Import/Export Service REST API](../StorageImportExportREST/Using-the-Azure-Import-Export-Service-REST-API.md)
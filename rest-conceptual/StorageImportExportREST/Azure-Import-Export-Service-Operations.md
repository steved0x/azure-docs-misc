---
title: "Azure Import-Export Service Operations"
ms.custom: na
ms.date: 05/25/2015
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 76b1eebf-5275-463a-a63c-af5681da56ba
caps.latest.revision: 7
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
# Azure Import-Export Service Operations
The Windows Azure Import/Export service REST API includes the operations described in the following table:  
  
|Operation|Description|  
|---------------|-----------------|  
|[Get Service Document](../StorageImportExportREST/Get-Service-Document.md)|Retrieves the service document, which describes the resources exposed by the Windows Azure Import/Export service.|  
|[Get Metadata Document](../StorageImportExportREST/Get-Metadata-Document.md)|Retrieves the service metadata document, which describes the complete data model for the resources exposed by the Windows Azure Import/Export service.|  
|[List Locations](../StorageImportExportREST/List-Locations2.md)|Returns a list of locations to which you can ship the disks associated with an import or export job.|  
|[List Storage Accounts](../StorageImportExportREST/List-Storage-Accounts2.md)|Returns a list of storage accounts for which one or more import or export jobs have been created for a subscription.|  
|[Put Job](../StorageImportExportREST/Put-Job.md)|Creates a new job in the Windows Azure Import/Export service.|  
|[Update Job Properties](../StorageImportExportREST/Update-Job-Properties.md)|Updates specific properties of a job. Can be used to update job state to `Shipping` or to cancel a job.|  
|[Get Job](../StorageImportExportREST/Get-Job3.md)|Gets information about an existing job from the Windows Azure Import/Export service.|  
|[List Jobs](../StorageImportExportREST/List-Jobs3.md)|Lists active and completed jobs for a subscription.|  
|[Delete Job](../StorageImportExportREST/Delete-Job1.md)|Deletes an existing job, purging the related data from the system.|  
  
## See Also  
 [Storage Import/Export REST](../StorageImportExportREST/Storage-Import-Export-Service-REST-API-Reference.md)
---
title: "Backing Up Drive Manifests"
ms.custom: na
ms.date: 05/25/2015
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 594abd80-b834-4077-a474-d8a0f4b7928a
caps.latest.revision: 7
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
# Backing Up Drive Manifests
Drive manifests can be automatically backed up to blobs by setting the `BackupDriveManifest` property to `true` in the [Put Job](../StorageImportExportREST/Put-Job.md) or [Update Job Properties](../StorageImportExportREST/Update-Job-Properties.md) operations. By default the drive manifests are not backed up. The drive manifest backups are stored as block blobs in a container within the storage account associated with the job. By default, the container name is `waimportexport`, but you can specify a different name in the `ImportExportStatesPath` property when calling the `Put Job` or `Update Job Properties` operations. The backup manifest blob are named in the following format: `waies/jobname_driveid_timestamp_manifest.xml`.  
  
 You can retrieve the URI of the backup drive manifests for a job by calling the [Get Job](../StorageImportExportREST/Get-Job3.md) operation. The blob URI is returned in the `ManifestUri` property for each drive.  
  
## See Also  
 [Using the Import/Export Service REST API](../StorageImportExportREST/Using-the-Azure-Import-Export-Service-REST-API.md)
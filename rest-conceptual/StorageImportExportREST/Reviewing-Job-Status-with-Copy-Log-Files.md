---
title: "Reviewing Job Status with Copy Log Files"
ms.custom: na
ms.date: 05/25/2015
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: c69d1d69-6403-4eee-9949-0185faeecfa1
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
# Reviewing Job Status with Copy Log Files
When the Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files to the storage account to or from which you are importing or exporting blobs. The log file contains detailed status about each file that was imported or exported. The URL to each copy log file is returned when you query the status of a completed job; see [Get Job](../StorageImportExportREST/Get-Job3.md) for more information.  
  
 The following are example URLs for copy log files for an import job with two drives:  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath /waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 See [Import-Export Service Log File Format](../StorageImportExportREST/Import-Export-Service-Log-File-Format.md) for the format of copy logs and the full list of status codes.  
  
## See Also  
 [Setting Up the Azure Import-Export Tool](../StorageImportExportREST/Setting-Up-the-Azure-Import-Export-Tool.md)   
 [Preparing Hard Drives for an Import Job](../StorageImportExportREST/Preparing-Hard-Drives-for-an-Import-Job.md)   
 [Repairing an Import Job](../StorageImportExportREST/Repairing-an-Import-Job.md)   
 [Repairing an Export Job](../StorageImportExportREST/Repairing-an-Export-Job.md)   
 [Troubleshooting the Azure Import-Export Tool](../StorageImportExportREST/Troubleshooting-the-Azure-Import-Export-Tool.md)
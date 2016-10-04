---
title: "Troubleshooting the Azure Import-Export Tool"
ms.custom: na
ms.date: 05/25/2015
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: b91ca5eb-c557-460a-9afc-0590b38471f9
caps.latest.revision: 11
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
# Troubleshooting the Azure Import-Export Tool
The Microsoft Azure Import/Export tool returns error messages if it runs into issues. This topic lists some common issues that users may run into.  
  
## A copy session fails, what I should do?  
 When a copy session fails, there are two options:  
  
 If the error is retryable, for example if the network share was offline for a short period and now is back online, you can resume the copy session. If the error is not retryable, for example if you specified the wrong source file directory in the command line parameters, you need to abort the copy session. See [Preparing Hard Drives for an Import Job](../StorageImportExportREST/Preparing-Hard-Drives-for-an-Import-Job.md) for more information about resuming and aborting copy sessions.  
  
## I can’t resume or abort a copy session.  
 If the copy session is the first copy session for a drive, then the error message should state: "The first copy session cannot be resumed or aborted." In this case, you can delete the old journal file and rerun the command.  
  
 If a copy session is not the first one for a drive, it can always be resumed or aborted.  
  
## I lost the journal file, can I still create the job?  
 The journal file for a drive contains the complete information of copying data to this drive, and it is needed to add more files to the drive and will be used to create an import job. If the journal file is lost, you will have to redo all the copy sessions for the drive.  
  
## See Also  
 [Setting Up the Azure Import-Export Tool](../StorageImportExportREST/Setting-Up-the-Azure-Import-Export-Tool.md)   
 [Preparing Hard Drives for an Import Job](../StorageImportExportREST/Preparing-Hard-Drives-for-an-Import-Job.md)   
 [Reviewing Job Status with Copy Log Files](../StorageImportExportREST/Reviewing-Job-Status-with-Copy-Log-Files.md)   
 [Repairing an Import Job](../StorageImportExportREST/Repairing-an-Import-Job.md)   
 [Repairing an Export Job](../StorageImportExportREST/Repairing-an-Export-Job.md)
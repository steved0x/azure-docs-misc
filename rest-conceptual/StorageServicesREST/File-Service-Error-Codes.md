---
title: "File Service Error Codes"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 88e9598f-06ea-4864-8758-6eb206923230
caps.latest.revision: 2
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
# File Service Error Codes
The error codes listed in the following table may be returned by an operation against the File service.  
  
|Error code|HTTP status code|User message|  
|----------------|----------------------|------------------|  
|ShareNotFound|Not Found (404)|The specified share does not exist.|  
|ShareAlreadyExists|Conflict (409)|The specified share already exists.|  
|ShareDisabled|Forbidden (403)|The specified share is disabled by the administrator.|  
|ShareBeingDeleted|Conflict (409)|The specified share is being deleted. Try operation later.|  
|DeletePending|Conflict (409)|The specified resource is marked for deletion by an SMB client.|  
|DirectoryNotEmpty|Conflict (409)|The specified directory is not empty.|  
|ParentNotFound|Not Found (404)|The specified parent path does not exist.|  
|SharingViolation|Conflict (409)|The specified resource may be in use by an SMB client.|  
|CannotDeleteFileOrDirectory|Conflict (409)|The file or directory could not be deleted because it is in use by an SMB client.|  
|FileLockConflict|Conflict (409)|A portion of the specified file is locked by an SMB client.|  
|ReadOnlyAttribute|Conflict (409)|The specified resource is read-only and cannot be modified at this time.|  
|ClientCacheFlushDelay|Internal Server Error (500)|The specified resource state could not be flushed from an SMB client in the specified time.|  
|InvalidFileOrDirectoryPathName|Bad Request (400)|File or directory path is too long.|  
|InvalidFileOrDirectoryPathName|Bad Request (400)|File or directory path has too many subdirectories.|  
  
## See Also  
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)
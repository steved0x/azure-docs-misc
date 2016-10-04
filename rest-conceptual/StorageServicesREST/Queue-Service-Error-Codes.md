---
title: "Queue Service Error Codes"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: aaf9617a-85c8-4e7b-aca6-acd95d596faa
caps.latest.revision: 21
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
# Queue Service Error Codes
The error codes listed in the following table may be returned by an operation on the Queue service.  
  
|Error code|HTTP status code|User message|  
|----------------|----------------------|------------------|  
|MessageTooLarge|Bad Request (400)|The message exceeds the maximum allowed size.|  
|InvalidMarker|Bad Request (400)|The specified marker is invalid.|  
|PopReceiptMismatch|Bad Request (400)|The specified pop receipt did not match the pop receipt for a dequeued message.|  
|QueueNotFound|Not Found (404)|The specified queue does not exist.|  
|MessageNotFound|Not Found (404)|The specified message does not exist.|  
|QueueDisabled|Conflict (409)|The specified queue has been disabled by the administrator.|  
|QueueAlreadyExists|Conflict (409)|The specified queue already exists.|  
|QueueBeingDeleted|Conflict (409)|The specified queue is being deleted.|  
|QueueNotEmpty|Conflict (409)|The specified queue is not empty.|  
  
## See Also  
 [Common REST API Error Codes](../StorageServicesREST/Common-REST-API-Error-Codes.md)   
 [Blob Service Error Codes](../StorageServicesREST/Blob-Service-Error-Codes.md)   
 [Table Service Error Codes](../StorageServicesREST/Table-Service-Error-Codes.md)   
 [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md)   
 [HttpStatusCode Enumeration](http://go.microsoft.com/fwlink/?LinkId=152845)   
 [Storage Services REST](../StorageServicesREST/Azure-Storage-Services-REST-API-Reference.md)
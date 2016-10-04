---
title: "Setting Timeouts for Queue Service Operations"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 59e840ea-62da-4e1c-9cc2-8a70e919594e
caps.latest.revision: 18
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
# Setting Timeouts for Queue Service Operations
A call to a Queue service API can include a server timeout interval, specified in the `timeout` parameter of the request URI. If the server timeout interval elapses before the service has finished processing the request, the service returns an error.  
  
 The maximum timeout interval for Queue service operations is 30 seconds. The Queue service automatically reduces any timeouts larger than 30 seconds to the 30-second maximum.  
  
 The following example REST URI sets the timeout interval for the [List Queues](../StorageServicesREST/List-Queues1.md) operation to 20 seconds:  
  
```  
GET https://myaccount.queue.core.windows.net?comp=list&timeout=20  
```  
  
## See Also  
 [Queue Service Concepts](../StorageServicesREST/Queue-Service-Concepts.md)
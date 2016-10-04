---
title: "Setting Timeouts for Table Service Operations"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: e54f330c-9fd7-4723-be6c-32d5e4ecd922
caps.latest.revision: 14
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
# Setting Timeouts for Table Service Operations
A call to a Table service API can include a server timeout interval, specified in the `timeout` parameter of the request URI. If the server timeout interval elapses before the service has finished processing the request, the service returns an error.  
  
 The maximum timeout interval for Table service operations is 30 seconds. The Table service automatically reduces any timeouts larger than 30 seconds to the 30-second maximum.  
  
 The Table service enforces server timeouts as follows:  
  
-   **Query operations:** During the timeout interval, a query may execute for up to a maximum of five seconds. If the query does not complete within the five-second interval, the response includes continuation tokens for retrieving remaining items on a subsequent request. See [Query Timeout and Pagination](../StorageServicesREST/Query-Timeout-and-Pagination.md) for more information.  
  
-   **Insert, update, and delete operations:** The maximum timeout interval is 30 seconds. Thirty seconds is also the default interval for all insert, update, and delete operations.  
  
 If you specify a timeout interval that is greater than 30 seconds, the Table service uses 30 seconds. If you specify a timeout that is less than the service's default timeout, your timeout interval will be used.  
  
## See Also  
 [Table Service Concepts](../StorageServicesREST/Table-Service-Concepts.md)
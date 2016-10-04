---
title: "CAST (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-07-19
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
applies_to: 
  - Azure
ms.assetid: 1cddcf7a-cdc7-4efc-91c3-9f8058b0e8c7
caps.latest.revision: 8
author: jeffstokes72
manager: jhubbard
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
# CAST (Azure Stream Analytics)
  Converts an expression of one data type to another within the supported types in Stream Analytics Query Language. This will fail and cause the job to stop if the conversion cannot be performed.
  
  For example, CAST ('this is a string' AS bigint) will result in a job failure. When this is not a desired outcome use [TRY_CAST &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/TRY_CAST--Azure-Stream-Analytics-.md) instead.
    
  
 **Syntax**  
  
```  
CAST ( expression AS data_type)  
  
```  
  
## Arguments  
 **expression**  
  
 Is any valid expression.  
  
 **data_type**  
  
 Is the target data type supported by Stream Analytics Query Language.  
  
## Return Types  
 Returns expression translated to data_type.  
  
## Examples  
  
```  
  
SELECT TollId, EntryTime, LicensePlate, State, Make   
FROM Input TIMESTAMP BY EntryTime  
WHERE CAST( TollId AS bigint) > 2  
  
```  
  
  
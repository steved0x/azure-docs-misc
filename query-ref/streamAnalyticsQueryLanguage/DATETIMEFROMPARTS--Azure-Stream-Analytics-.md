---
title: "DATETIMEFROMPARTS (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
applies_to: 
  - Azure
ms.assetid: 6e69e0ea-6774-4ad2-981b-a4624a56c52b
caps.latest.revision: 5
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
# DATETIMEFROMPARTS (Azure Stream Analytics)
  Returns a datetime value for the specified date and time.  
  
 **Syntax**  
  
```  
DATETIMEFROMPARTS (year, month, day, hour, minute, seconds, milliseconds)  
  
```  
  
## Arguments  
 **date**  
  
 Is an expression that can be resolved to a datetime. date can be an expression, column expression, or string literal.  
  
## Return Types  
 datetime  
  
## Examples  
  
```  
SELECT EntryTime, DATETIMEFROMPARTS(2014,9,10,12,DATEPART(minute,EntryTime)+10,00,00)   
AS ExitTime  
FROM Input TIMESTAMP BY EntryTime  
WHERE Toll > 5  
  
```  
  
  
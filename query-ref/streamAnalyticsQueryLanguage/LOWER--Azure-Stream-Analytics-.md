---
title: "LOWER (Azure Stream Analytics)"
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
ms.assetid: 378b640d-7cd8-429a-83f8-7738c008411d
caps.latest.revision: 6
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
# LOWER (Azure Stream Analytics)
  Returns a character expression after converting uppercase character data to lowercase.  
  
 **Syntax**  
  
```  
LOWER ( string_expression )  
```  
  
## Arguments  
 **string_expression**  
  
 Is the string expression to be evaluated. string_expression can be a constant or column of type nvarchar(max)  
  
## Return Types  
 nvarchar(max)  
  
## Examples  
  
```  
SELECT TollId, EntryTime, LOWER(LicensePlate) AS LicensePlate_Lower  
FROM Input  
```  
  
## See Also  
 [UPPER &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/UPPER--Azure-Stream-Analytics-.md)  
  
  
---
title: "UPPER (Azure Stream Analytics)"
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
ms.assetid: 36eeda67-4fe9-46ff-b5cb-5a53244f3ed3
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
# UPPER (Azure Stream Analytics)
  Returns a character expression with lowercase character data converted to uppercase.  
  
 **Syntax**  
  
```  
UPPER ( string_expression )  
```  
  
## Arguments  
 **string_expression**  
  
 Is the string expression to be evaluated. string_expression can be a constant or column of type nvarchar(max)  
  
## Return Types  
 nvarchar(max)  
  
## Examples  
  
```  
SELECT TollId, EntryTime, UPPER(LicensePlate) AS LicensePlate_Upper  
FROM Input  
```  
  
## See Also  
 [LOWER &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/LOWER--Azure-Stream-Analytics-.md)  
  
  
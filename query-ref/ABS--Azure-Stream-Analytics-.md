---
title: "ABS (Azure Stream Analytics)"
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
ms.assetid: 88f0e7d4-dc2e-4c0b-a9b5-6942a85f93a9
caps.latest.revision: 9
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
# ABS (Azure Stream Analytics)
  A mathematical function that returns the absolute (positive) value of the specified numeric expression.  
  
 **Syntax**  
  
```  
ABS (expression )  
```  
  
## Argument  
 **expression**  
  
 Is an expression of the exact numeric or approximate numeric data type category. ABS can be used with bigint or float columns.  
  
## Return Type  
 Returns the same type as expression.  
  
## Example  
  
```  
SELECT ABS(input.x) AS "The ABS of the variable x"  
FROM input  
```  
  
  
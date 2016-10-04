---
title: "CEILING (Azure Stream Analytics)"
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
ms.assetid: 86b82a0b-cb22-40fa-a5b3-3731e2dde085
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
# CEILING (Azure Stream Analytics)
  A mathematical function that returns the smallest integer greater than or equal to the specified numeric expression.  
  
 **Syntax**  
  
```  
CEILING (expression)  
```  
  
## Arguement  
 **expression**  
  
 An expression of the exact numeric or approximate numeric data type category.  
  
### Return Types  
 Returns the same type as submitted in the expression.  
  
### Example  
  
```  
SELECT CEILING(input.x) AS "The CEILING of the variable x"  
FROM input  
```  
  
  
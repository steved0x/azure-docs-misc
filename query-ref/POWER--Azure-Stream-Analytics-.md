---
title: "POWER (Azure Stream Analytics)"
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
ms.assetid: 89a126bc-f801-4697-b1dd-93235d1f54a0
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
# POWER (Azure Stream Analytics)
  A mathematical function that returns the value of the specified expression to the specified power.  
  
 **Syntax**  
  
```  
POWER (float_expression, y)  
```  
  
## Arguments  
 **float_expression**  
  
 Is an expression of type **float** or of a type that can be implicitly converted to a **float**.  
  
 **y**  
  
 The power to which to raise **float_expression**. **y** can be an expression of the exact numeric or approximate numeric data type category.  
  
## Return Type  
 Returns the same type as submitted in **float_expression**. For example, if a bigint was submitted as **float_expressions**, the result returned is bigint.  
  
## Example  
  
```  
SELECT POWER(input.x, 3) AS "The 3rd POWER of the variable x"  
FROM input  
```  
  
  
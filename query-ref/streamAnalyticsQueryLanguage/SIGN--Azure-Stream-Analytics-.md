---
title: "SIGN (Azure Stream Analytics)"
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
ms.assetid: dbac5267-6bc2-42c9-98f8-5b05485b54b7
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
# SIGN (Azure Stream Analytics)
  A mathematical function that returns the positive (+1), zero (0), or negative (-1) sign of the specified expression.  
  
 **Syntax**  
  
```  
SIGN (expression)  
```  
  
## Arguement  
 **expression**  
  
 Is an **expression** of the exact numeric or approximate numeric data type category.  
  
## Return Type  
 Returns the same type as submitted in **expression**.  
  
## Example  
  
```  
SELECT SIGN(input.x) AS "The SIGN of the variable x"  
FROM input  
```  
  
  
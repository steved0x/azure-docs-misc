---
title: "GetArrayLength (Azure Stream Analytics)"
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
ms.assetid: e5efa2e4-57fa-49c6-9620-36eef71e74fb
caps.latest.revision: 7
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
# GetArrayLength (Azure Stream Analytics)
  Returns the length of the specified array.  
  
 **Syntax**  
  
```  
GetArrayLength ( array_expression )  
```  
  
## Arguments  
 **array_expression**  
  
 Is the array expression to be evaluated as a source array. array_expression can be a column of type Array or result of another function call.  
  
## Return Types  
 bigint  
  
## Examples  
  
```  
SELECT   
    GetArrayLength(arrayField) AS arrayLength  
FROM input  
  
```  
  
  
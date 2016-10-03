---
title: "PATINDEX (Azure Stream Analytics)"
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
ms.assetid: 42e4e849-2fbd-4374-bd8c-d40130ae81a3
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
# PATINDEX (Azure Stream Analytics)
  Returns the starting position of the first occurrence of a pattern in a specified expression, or 0 if the pattern is not found, on all valid nvarchar(max) data types.  
  
 **Syntax**  
  
```  
PATINDEX ( '%pattern%' , expression )  
```  
  
## Arguments  
 **pattern**  
  
 A character expression that contains the sequence to be found. Wildcard characters can be used; however, the % character must come before and follow pattern (except when searching for first or last characters). pattern is an expression of the character string data type category. pattern is limited to 8000 characters.  
  
 **expression**  
  
 An expression, typically a column that is searched for the specified pattern. Where the expression is of the nvarchar(max) data type.  
  
## Return Types  
 bigint  
  
## Examples  
  
```  
SELECT TollId, EntryTime, LicensePlate, PATINDEX ( ‘%100%’,LicensePlate ),  
FROM Input TIMESTAMP BY EntryTime  
  
```  
  
  
---
title: "LEN (Azure Stream Analytics)"
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
ms.assetid: 82f25a01-f71c-470a-9b01-93fc374fda90
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
# LEN (Azure Stream Analytics)
  Returns the number of characters of the specified string expression, excluding trailing blanks.  
  
 **Syntax**  
  
```  
LEN ( string_expression )  
  
```  
  
## Arguments  
 **string_expression**  
  
 Is the string expression to be evaluated. string_expression can be a constant or column of type nvarchar(max)  
  
## Return Types  
 bigint  
  
## Examples  
  
```  
SELECT TollId, EntryTime, LicensePlate, LEN (LicensePlate) AS Len_License  
FROM Input TIMESTAMP BY EntryTime  
WHERE Toll > 5  
```  
  
  
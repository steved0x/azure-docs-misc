---
title: "CONCAT (Azure Stream Analytics)"
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
ms.assetid: 57e62210-6923-4306-918c-6e0e8834afb0
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
# CONCAT (Azure Stream Analytics)
  Returns a string that is the result of concatenating two or more string values.  
  
 **Syntax**  
  
```  
CONCAT ( string_value1, string_value2 [, string_valueN ] )  
```  
  
## Arguments  
 **string_value**  
  
 A string value to concatenate to the other values.  
  
## Return Types  
 nvarchar(max)  
  
## Examples  
  
```  
SELECT TollId, EntryTime, CONCAT ( 'Make:', Make, ' And Model:', Model) AS MakeModel, LicensePlate  
FROM Input TIMESTAMP BY EntryTime  
WHERE Toll > 5  
  
```  
  
  
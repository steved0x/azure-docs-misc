---
title: "COUNT (Azure Stream Analytics)"
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
ms.assetid: 494f899f-2ea7-4990-9a65-3881d9995b33
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
# COUNT (Azure Stream Analytics)
  Returns the number of items in a group. COUNT always returns a bigint data type value.  
  
 **Syntax**  
  
```  
COUNT ( { [expression ] | * } )  
  
```  
  
## Arguments  
 **expression**  
  
 Is an expression of any type or a column name. Aggregate functions and sub queries are not permitted.  
  
 **\***  
  
 Specifies that all rows should be counted to return the total number of rows in a table. COUNT(*) takes no parameters. COUNT(\*) does not require an expression parameter because, by definition, it does not use information about any particular column. COUNT(\*) returns the number of rows in a specified table without getting rid of duplicates. It counts each row separately. This includes rows that contain null values.  
  
## Return Types  
 bigint  
  
## Examples  
  
```  
SELECT System.TimeStamp AS OutTime, TollId, COUNT(*)   
FROM Input TIMESTAMP BY EntryTime  
GROUP BY TollId, TumblingWindow(minute,3)  
  
```  
  
  
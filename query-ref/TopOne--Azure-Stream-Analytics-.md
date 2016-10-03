---
title: "TopOne (Azure Stream Analytics)"
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
ms.assetid: 9728630c-1c59-4349-a562-fdd98433da9d
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
# TopOne (Azure Stream Analytics)
  Returns the top-rank record, where rank defines the ranking position of the event in the window according to the specified ordering. Ordering/ranking is based on event columns and can be specified in ORDER BY clause.  
  
 **Syntax**  
  
```  
TopOne() OVER (ORDER BY (<column name> [ASC |DESC])+)  
```  
  
## Arguments  
 **column_name**  
  
 Specifies the name of the column in the input event by which ordering will be done. Note that only ordering by bigint, float and datetime types are allowed.  
  
## Return Types  
 Returns a record.  
  
## Examples  
  
```  
SELECT   
    TopOne() OVER (ORDER BY value DESC) as topEvent  
FROM input  
GROUP BY TumblingWindow(second, 10)  
  
```  
  
  
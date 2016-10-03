---
title: "GROUP BY (Azure Stream Analytics)"
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
ms.assetid: 6ae879ff-435d-44e3-bbc7-09cbd399a502
caps.latest.revision: 11
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
# GROUP BY (Azure Stream Analytics)
  Groups a selected set of rows into a set of summary rows by the values of one or more columns or expressions. One row is returned for each group. Aggregate functions in the SELECT clause’s <select\> list provide information about each group instead of individual rows.  
  
 **Syntax**  
  
```  
GROUP BY <group by spec>  
  
<group by spec> ::=  
    <group by item> [ ,...n ]  
    | <window_type> | System.Timestamp  
  
<group by item> ::=  
    <column_expression>  
  
```  
  
 Either <window_type> or System.Timestamp is required, <group by item\> is optional.  <window_type> and a sequence of <group by items\> can appear in any order.  
  
## Arguments  
 **<window_type>**  
  
 Specifies any Azure Stream Analytics supported Windowing. See [Windowing &#40;Azure Stream Analytics&#41;](../query-ref/Windowing--Azure-Stream-Analytics-.md).  
  
 **< column_expression >**  
  
 Is the expression or the name of the column on which the grouping operation is performed.  
  
## Example  
  
```  
SELECT TollId, System.Timestamp AS WinEndTime, COUNT(*)   
FROM TollTagEntry TIMESTAMP BY EntryTime  
GROUP BY TumblingWindow( minute , 3 ) , TollId  
```  
  
## See Also  
 [System.Timestamp](../query-ref/System.Timestamp---Stream-Analytics-.md)   
 [Windowing](../query-ref/Windowing--Azure-Stream-Analytics-.md)  
  
  
---
title: "Aggregate Functions (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-09-12
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
applies_to: 
  - Azure
ms.assetid: 1fa11c79-3f97-4050-8d2c-b4cf61cdaf59
caps.latest.revision: 23
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
# Aggregate Functions (Azure Stream Analytics)
  Aggregate functions perform a calculation on a set of values and return a single value. Except for the COUNT function, aggregate functions ignore null values. Aggregate functions are frequently used with the GROUP BY clause of the SELECT statement.  
  
 All aggregate functions are deterministic. This means aggregate functions return the same value any time that they are called by using a specific set of input values.  
  
 Aggregate functions can be used as expressions only in the following:  
  
-   The select list of a SELECT statement (either a subquery or an outer query).  
  
-   A HAVING clause.  
  
 Stream Analytics Query Language provides the following aggregate functions:  
  
||||  
|-|-|-|  
|[AVG &#40;Azure Stream Analytics&#41;](../query-ref/AVG--Azure-Stream-Analytics-.md)|[COUNT &#40;Azure Stream Analytics&#41;](../query-ref/COUNT--Azure-Stream-Analytics-.md)|[Collect &#40;Azure Stream Analytics&#41;](../query-ref/Collect--Azure-Stream-Analytics-.md)|
|[CollectTOP &#40;Azure Stream Analytics&#41;](../query-ref/CollectTOP--Azure-Stream-Analytics-.md)|[MAX &#40;Azure Stream Analytics&#41;](../query-ref/MAX--Azure-Stream-Analytics-.md)|[MIN &#40;Azure Stream Analytics&#41;](../query-ref/MIN--Azure-Stream-Analytics-.md)|
|[Percentile_Cont &#40;Azure Stream Analytics&#41;](../query-ref/Percentile_Cont--Azure-Stream-Analytics-.md)  | [Percentile_Disc &#40;Azure Stream Analytics&#41;](../query-ref/Percentile_Disc--Azure-Stream-Analytics-.md) |[STDEV &#40;Azure Stream Analytics&#41;](../query-ref/STDEV--Azure-Stream-Analytics-.md)|
|[STDEVP &#40;Azure Stream Analytics&#41;](../query-ref/STDEVP--Azure-Stream-Analytics-.md)|[SUM &#40;Azure Stream Analytics&#41;](../query-ref/SUM--Azure-Stream-Analytics-.md)| [TopOne &#40;Azure Stream Analytics&#41;](../query-ref/TopOne--Azure-Stream-Analytics-.md)|
|[VAR &#40;Azure Stream Analytics&#41;](../query-ref/VAR--Azure-Stream-Analytics-.md)|[VARP &#40;Azure Stream Analytics&#41;](../query-ref/VARP--Azure-Stream-Analytics-.md)|
  
## See Also  
 [Built-In Functions](../query-ref/Built-in-Functions--Azure-Stream-Analytics-.md)   
 [Analytic Functions](../query-ref/Analytic-Functions--Azure-Stream-Analytics-.md)   
 [Array Functions](../query-ref/Array-Functions--Stream-Analytics-.md)   
 [Conversion Functions](../query-ref/Conversion-Functions--Azure-Stream-Analytics-.md)   
 [Date and Time Functions](../query-ref/Date-and-Time-Functions--Azure-Stream-Analytics-.md)   
 [Mathematical Functions](../query-ref/Mathematical-Functions--Azure-Stream-Analytics-.md)   
 [Record Functions](../query-ref/Record-Functions--Azure-Stream-Analytics-.md)   
 [String Functions](../query-ref/String-Functions--Azure-Stream-Analytics-.md)  
  
  
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
|[AVG &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/AVG--Azure-Stream-Analytics-.md)|[COUNT &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/COUNT--Azure-Stream-Analytics-.md)|[Collect &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/Collect--Azure-Stream-Analytics-.md)|
|[CollectTOP &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/CollectTOP--Azure-Stream-Analytics-.md)|[MAX &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/MAX--Azure-Stream-Analytics-.md)|[MIN &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/MIN--Azure-Stream-Analytics-.md)|
|[Percentile_Cont &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/Percentile_Cont--Azure-Stream-Analytics-.md)  | [Percentile_Disc &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/Percentile_Disc--Azure-Stream-Analytics-.md) |[STDEV &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/STDEV--Azure-Stream-Analytics-.md)|
|[STDEVP &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/STDEVP--Azure-Stream-Analytics-.md)|[SUM &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/SUM--Azure-Stream-Analytics-.md)| [TopOne &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/TopOne--Azure-Stream-Analytics-.md)|
|[VAR &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/VAR--Azure-Stream-Analytics-.md)|[VARP &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/VARP--Azure-Stream-Analytics-.md)|
  
## See Also  
 [Built-In Functions](../streamAnalyticsQueryLanguage/Built-in-Functions--Azure-Stream-Analytics-.md)   
 [Analytic Functions](../streamAnalyticsQueryLanguage/Analytic-Functions--Azure-Stream-Analytics-.md)   
 [Array Functions](../streamAnalyticsQueryLanguage/Array-Functions--Stream-Analytics-.md)   
 [Conversion Functions](../streamAnalyticsQueryLanguage/Conversion-Functions--Azure-Stream-Analytics-.md)   
 [Date and Time Functions](../streamAnalyticsQueryLanguage/Date-and-Time-Functions--Azure-Stream-Analytics-.md)   
 [Mathematical Functions](../streamAnalyticsQueryLanguage/Mathematical-Functions--Azure-Stream-Analytics-.md)   
 [Record Functions](../streamAnalyticsQueryLanguage/Record-Functions--Azure-Stream-Analytics-.md)   
 [String Functions](../streamAnalyticsQueryLanguage/String-Functions--Azure-Stream-Analytics-.md)  
  
  
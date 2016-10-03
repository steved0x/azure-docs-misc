---
title: "Time Management (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-05-18
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
applies_to: 
  - Azure
ms.assetid: 1cc875d1-0f20-46b6-8001-dad1eaa075e5
caps.latest.revision: 15
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
# Time Management (Azure Stream Analytics)
  Azure Stream Analytics query language extends SQL syntax to enable complex computations over streams of events. Stream Analytics provides language constructs to deal with the temporal aspects of the data. For example, it is possible to assign custom timestamps to the stream events, specify time window for aggregations, specify allowed time difference between two streams of data for JOIN operation, etc.  
  
|Item|Summary|  
|----------|-------------|  
|[System.Timestamp](../query-ref/System.Timestamp---Stream-Analytics-.md)|System.Timestamp is a system property that can be used to retrieve the event’s timestamp.|  
|[TIMESTAMP BY](../query-ref/TIMESTAMP-BY--Azure-Stream-Analytics-.md)|The TIMESTAMP BY clause allows specifying custom timestamp values.|  
|[Time Skew Policies](../query-ref/Time-Skew-Policies--Azure-Stream-Analytics-.md)|Policies for Out of Order and Late Arrival Events.|  
|[Aggregate functions](../query-ref/Aggregate-Functions--Azure-Stream-Analytics-.md) over [time window](../query-ref/Windowing--Azure-Stream-Analytics-.md)|Aggregate functions are used to perform a calculation on a set of values from a time window and return a single value.|  
|[DATEDIFF in JOIN predicate](../query-ref/JOIN--Azure-Stream-Analytics-.md)|Specify time boundaries for JOIN operations|  
|[Date and Time functions](../query-ref/Date-and-Time-Functions--Azure-Stream-Analytics-.md)|Stream Analytics provides a variety of date and time functions for use.|  
  
## See Also  
 [Built-in Functions &#40;Azure Stream Analytics&#41;](../query-ref/Built-in-Functions--Azure-Stream-Analytics-.md)   
 [Data Types &#40;Azure Stream Analytics&#41;](../query-ref/Data-Types--Azure-Stream-Analytics-.md)   
 [Event Delivery Guarantees&#40;Azure Stream Analytics&#41;](../query-ref/Event-Delivery-Guarantees--Azure-Stream-Analytics-.md)  
  
  
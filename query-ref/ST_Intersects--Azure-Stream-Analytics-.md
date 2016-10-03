---
title: "ST_Intersects (Azure Stream Analytics)"
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
ms.assetid: 249dbc76-3106-4232-a5ca-aa9d8350d97a
caps.latest.revision: 8
author: jeffstokes72
manager: jhubbard
robots: noindex,nofollow
---
# ST_Intersects (Azure Stream Analytics)
  Returns 1 if a geography intersects with another. If geographies do not intersect it will return 0.  
  
 **Syntax**  
  
```  
ST_INTERSECTS (lineStringA, lineStringB)  
```  
  
## Argument  
 **LineStringA**  
  
 The LineString that could intersect with LineStringB.  
  
 **LineStringB**  
  
 The LineString that could intersect with LineStringA.  
  
## Return Type  
 Returns 1 if a LineString intersects with another LineString, if not it will return 0.  
  
## Example  
  
```  
SELECT  
     ST_INTERSECTS(input.pavedRoad, input.dirtRoad)  
FROM input  
  
```  
  
### Input Example  
  
|datacenterArea|stormArea|  
|--------------------|---------------|  
|{“type”:”LineString”, “coordinates”: [ [-10.0, 0.0], [0.0, 0.0], [10.0, 0.0] ]}|{“type”:”LineString”, “coordinates”: [ [0.0, 10.0], [0.0, 0.0], [0.0, -10.0] ]}|  
|{“type”:”LineString”, “coordinates”: [ [-10.0, 0.0], [0.0, 0.0], [10.0, 0.0] ]}|{“type”:”LineString”, “coordinates”: [ [-10.0, 10.0], [0.0, 10.0], [10.0, 10.0] ]}|  
  
### Output Example  
 1  
  
 0  
  
## See Also  
 [Geospatial Functions &#40;Azure Stream Analytics&#41;](../query-ref/Geospatial-Functions--Azure-Stream-Analytics-.md)   
 [ST_Distance &#40;Azure Stream Analytics&#41;](../query-ref/ST_Distance--Azure-Stream-Analytics-.md)   
 [ST_Overlaps &#40;Azure Stream Analytics&#41;](../query-ref/ST_Overlaps--Azure-Stream-Analytics-.md)   
 [ST_Within &#40;Azure Stream Analytics&#41;](../query-ref/ST_Within--Azure-Stream-Analytics-.md)  
  
  
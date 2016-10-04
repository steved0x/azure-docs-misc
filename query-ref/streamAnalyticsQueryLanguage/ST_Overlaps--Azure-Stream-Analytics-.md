---
title: "ST_Overlaps (Azure Stream Analytics)"
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
ms.assetid: e00392b8-f899-43e0-bac1-b900902a0cab
caps.latest.revision: 9
author: jeffstokes72
manager: jhubbard
robots: noindex,nofollow
---
# ST_Overlaps (Azure Stream Analytics)
  Returns 1 if a geography overlaps with another. If geographies do not overlap or one is within another, it will return 0.  
  
 **Syntax**  
  
```  
ST_OVERLAPS (polygonA, polygonB)  
```  
  
## Argument  
 **PolygonA**  
  
 The polygon that could overlap with polygonB.  
  
 **PolygonB**  
  
 The polygon that could overlap with polygonA.  
  
## Return Type  
 Returns 1 if a polygon overlaps with another polygon, if not it will return 0.  
  
## Example  
  
```  
SELECT  
     ST_OVERLAPS(input.datacenterArea, input.stormArea)  
FROM input  
  
```  
  
### Input Example  
  
|datacenterArea|stormArea|  
|--------------------|---------------|  
|{“type”:”Polygon”, “coordinates”: [ [0.0, 0.0], [10.0, 0.0], [10.0, 10.0], [0.0, 10.0], [0.0, 0.0] ]}|{“type”:”Polygon”, “coordinates”: [ [30.0, 30.0], [40.0, 30.0], [40.0, 40.0], [30.0, 40.0], [30.0, 30.0] ]}|  
|{“type”:”Polygon”, “coordinates”: [ [0.0, 0.0], [20.0, 0.0], [20.0, 20.0], [0.0, 20.0], [0.0, 0.0] ]}|{“type”:”Polygon”, “coordinates”: [ [10.0, 10.0], [40.0, 10.0], [40.0, 40.0], [40.0, 20.0], [40.0, 40.0] ]}|  
  
### Output Example  
 0  
  
 1  
  
## See Also  
 [Geospatial Functions &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/Geospatial-Functions--Azure-Stream-Analytics-.md)   
 [ST_Distance &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/ST_Distance--Azure-Stream-Analytics-.md)   
 [ST_Intersects &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/ST_Intersects--Azure-Stream-Analytics-.md)   
 [ST_Within &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/ST_Within--Azure-Stream-Analytics-.md)  
  
  
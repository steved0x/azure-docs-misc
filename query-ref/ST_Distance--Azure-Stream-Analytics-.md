---
title: "ST_Distance (Azure Stream Analytics)"
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
ms.assetid: e7a73195-d043-4645-928a-48860ac9af04
caps.latest.revision: 6
author: jeffstokes72
manager: jhubbard
robots: noindex,nofollow
---
# ST_Distance (Azure Stream Analytics)
  Returns the distance between two points in meters. If used with Polygons will return 0.  
  
 **Syntax**  
  
```  
ST_DISTANCE ( pointA, pointB )  
```  
  
## Argument  
 **PointA**  
  
 The point to measure distance from.  
  
 **PointB**  
  
 The point to measure distance to.  
  
## Return Type  
 Returns the distance between two points in meters.  
  
## Example  
  
```  
SELECT  
     ST_DISTANCE(input.car1Position, input.car2Position)  
FROM input  
  
```  
  
### Input Example  
  
|carPosition|warehouse|  
|-----------------|---------------|  
|{“type”:”Point”, “coordinates”: [-5.0, -5.0]}|{“type”:”Point”, “coordinates”: [0.0, 0.0]}|  
  
### Output Example  
 784028.74077501823  
  
## See Also  
 [Geospatial Functions &#40;Azure Stream Analytics&#41;](../query-ref/Geospatial-Functions--Azure-Stream-Analytics-.md)   
 [ST_Intersects &#40;Azure Stream Analytics&#41;](../query-ref/ST_Intersects--Azure-Stream-Analytics-.md)   
 [ST_Overlaps &#40;Azure Stream Analytics&#41;](../query-ref/ST_Overlaps--Azure-Stream-Analytics-.md)   
 [ST_Within &#40;Azure Stream Analytics&#41;](../query-ref/ST_Within--Azure-Stream-Analytics-.md)  
  
  
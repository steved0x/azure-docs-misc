---
title: "ST_Within (Azure Stream Analytics)"
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
ms.assetid: d842c8c8-63cd-49aa-9ab4-2a92c338e6db
caps.latest.revision: 9
author: jeffstokes72
manager: jhubbard
robots: noindex,nofollow
---
# ST_Within (Azure Stream Analytics)
  Returns 1 if a geography is within another, if not it will return 0.  
  
 **Syntax**  
  
```  
ST_WITHIN (geography, polygon)  
```  
  
## Argument  
 **Geography**  
  
 The geography that could be inside the polygon. Can be either a point or a polygon.  
  
 **Polygon**  
  
 The polygon that could contain the geography.  
  
## Return Type  
 Returns 1 if either a point or polygon is within another polygon, if not it will return 0.  
  
## Example  
  
```  
SELECT  
     ST_WITHIN(input.deliveryDestination, input.warehouse)  
FROM input  
  
```  
  
### Input Example  
  
|deliveryDestination|warehouse|  
|-------------------------|---------------|  
|{“type”:”Point”, “coordinates”: [76.6, 10.1]}|{“type”:”Polygon”, “coordinates”: [ [0.0, 0.0], [10.0, 0.0], [10.0, 10.0], [0.0, 10.0], [0.0, 0.0] ]}|  
|{“type”:”Point”, “coordinates”: [15.0, 15.0]}|{“type”:”Polygon”, “coordinates”: [ [10.0, 10.0], [20.0, 10.0], [20.0, 20.0], [10.0, 20.0], [10.0, 10.0] ]}|  
  
### Output Example  
 0  
  
 1  
  
## See Also  
 [Geospatial Functions &#40;Azure Stream Analytics&#41;](../query-ref/Geospatial-Functions--Azure-Stream-Analytics-.md)   
 [ST_Distance &#40;Azure Stream Analytics&#41;](../query-ref/ST_Distance--Azure-Stream-Analytics-.md)   
 [ST_Intersects &#40;Azure Stream Analytics&#41;](../query-ref/ST_Intersects--Azure-Stream-Analytics-.md)   
 [ST_Overlaps &#40;Azure Stream Analytics&#41;](../query-ref/ST_Overlaps--Azure-Stream-Analytics-.md)  
  
  
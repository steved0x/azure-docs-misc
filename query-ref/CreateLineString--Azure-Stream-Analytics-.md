---
title: "CreateLineString (Azure Stream Analytics)"
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
ms.assetid: 72f28320-0e5b-4292-af82-12f88889ebec
caps.latest.revision: 8
author: jeffstokes72
manager: jhubbard
robots: noindex,nofollow
---
# CreateLineString (Azure Stream Analytics)
  Returns a GeoJSON LineString record. The result of a CreateLineString can be used as input to other Geospatial functions.  
  
 Be away that when declaring LineStrings:  
  
-   A LineStrings must have at least 2 points.  
  
-   The structure cannot overlap itself over an interval of two or more consecutive points.  
  
 **Syntax**  
  
```  
CreateLineString (points)  
```  
  
## Argument  
 **Points**  
  
 A list of GeoJSON record points.  
  
## Return Type  
 Returns a GeoJSON LineString record with LineString as type and an arrays of points as coordinates.  
  
## Example  
  
```  
SELECT  
     CreateLineString(CreatePoint(input.latitude, input.longitude), CreatePoint(10.0, 10.0), CreatePoint(10.5, 10.5))  
FROM input  
  
```  
  
### Input Example  
  
|latitude|longitude|  
|--------------|---------------|  
|3.0|-10.2|  
|-87.33|20.2321|  
  
### Output Example  
 {“type” : “LineString”, “coordinates” : [ [3.0, -10.2], [10.0, 10.0], [10.5, 10.5] ]}  
  
 {“type” : “LineString”, “coordinates” : [ [-87.33, 20.2321], [10.0, 10.0], [10.5, 10.5] ]}  
  
## See Also  
 [Geospatial Functions &#40;Azure Stream Analytics&#41;](../query-ref/Geospatial-Functions--Azure-Stream-Analytics-.md)   
 [CreatePoint &#40;Azure Stream Analytics&#41;](../query-ref/CreatePoint--Azure-Stream-Analytics-.md)   
 [CreatePolygon &#40;Azure Stream Analytics&#41;](../query-ref/CreatePolygon--Azure-Stream-Analytics-.md)  
  
  
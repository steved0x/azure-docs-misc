---
title: "CreatePolygon (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
apitype: NA
applies_to: 
  - Azure
ms.assetid: 219c61b2-d0f1-4e0e-831d-aa2f04e18c40
caps.latest.revision: 8
author: jeffstokes72
manager: jhubbard
robots: noindex,nofollow
---
# CreatePolygon (Azure Stream Analytics)
  Returns a GeoJSON Polygon record. The result of a CreatePolygon can be used as input to other Geospatial functions. The order of points must follow right-hand ring orientation, an easy way to check if the polygon orientation is correct is to imagine yourself walking from one point to the other in order of declaration, the inside of the polygon needs to be on your left side all the time.  
  
 Be aware that when declaring polygons:  
  
-   A polygon with left-hand ring orientation will generate a geography that encompass the entire globe minus the polygon you declared.  
  
-   Polygons cannot have holes.  
  
-   Polygons cannot have less than 3 points.  
  
-   First and last points declared must be equal to close the loop  
  
 **Syntax**  
  
```  
CreatePolygon (points)  
```  
  
## Argument  
 **Points**  
  
 A list of GeoJSON record points.  
  
## Return Type  
 Returns a GeoJSON polygon record with Polygon as type and an array of points as coordinates.  
  
## Example  
  
```  
 SELECT  
     CreatePolygon(CreatePoint(input.latitude, input.longitude), CreatePoint(10.0, 10.0), CreatePoint(10.5, 10.5), CreatePoint(input.latitude, input.longitude))  
FROM input  
  
```  
  
### Input Example  
  
|latitude|longitude|  
|--------------|---------------|  
|3.0|-10.2|  
|-87.33|20.2321|  
  
### Output Example  
 {“type” : “Polygon”, “coordinates” : [ [3.0, -10.2], [10.0, 10.0], [10.5, 10.5], [3.0, -10.2] ]}  
  
 {“type” : “Polygon”, “coordinates” : [ [-87.33, 20.2321], [10.0, 10.0], [10.5, 10.5], [-87.33, 20.2321] ]}  
  
## See Also  
 [Geospatial Functions &#40;Azure Stream Analytics&#41;](../query-ref/Geospatial-Functions--Azure-Stream-Analytics-.md)   
 [CreateLineString &#40;Azure Stream Analytics&#41;](../query-ref/CreateLineString--Azure-Stream-Analytics-.md)   
 [CreatePoint &#40;Azure Stream Analytics&#41;](../query-ref/CreatePoint--Azure-Stream-Analytics-.md)  
  
  
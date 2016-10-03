---
title: "CreatePoint (Azure Stream Analytics)"
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
ms.assetid: d5ad918a-df88-4b40-8a72-d9068896591c
caps.latest.revision: 6
author: jeffstokes72
manager: jhubbard
robots: noindex,nofollow
---
# CreatePoint (Azure Stream Analytics)
  Returns a GeoJSON Point record. The result of a CreatePoint can be used as input to other Geospatial functions.  
  
 **Syntax**  
  
```  
CreatePoint (latitude, longitude)  
```  
  
## Argument  
 **Latitude**  
  
 Is the latitude of a geographic point, value must be float.  
  
 **Longitude**  
  
 Is the longitude of a geographic point, value must be float.  
  
## Return Type  
 Returns a GeoJSON point record with Point as type and an array with latitude and longitude as coordinates.  
  
## Example  
  
```  
 SELECT  
     CreatePoint(input.latitude, input.longitude)  
FROM input  
  
```  
  
### Input Example  
  
|latitude|longitude|  
|--------------|---------------|  
|3.0|-10.2|  
|-87.33|20.2321|  
  
### Output Example  
 {“type” : ”Point”, “coordinates” : [3.0, -10.2]}  
  
 {“type” : ”Point”, “coordinates” : [-87.33, 20.2321]}  
  
## See Also  
 [Geospatial Functions &#40;Azure Stream Analytics&#41;](../query-ref/Geospatial-Functions--Azure-Stream-Analytics-.md)   
 [CreateLineString &#40;Azure Stream Analytics&#41;](../query-ref/CreateLineString--Azure-Stream-Analytics-.md)   
 [CreatePolygon &#40;Azure Stream Analytics&#41;](../query-ref/CreatePolygon--Azure-Stream-Analytics-.md)  
  
  
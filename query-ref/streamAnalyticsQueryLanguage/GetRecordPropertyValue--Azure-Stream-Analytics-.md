---
title: "GetRecordPropertyValue (Azure Stream Analytics)"
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
ms.assetid: 0d49d7a6-680d-4e78-af4e-26301e5deb8b
caps.latest.revision: 8
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
# GetRecordPropertyValue (Azure Stream Analytics)
  Returns the record value associated with the specified property.  
  
 **Syntax**  
  
```  
GetRecordPropertyValue ( record_expression, string_expression )  
```  
  
## Arguments  
 **record_expression**  
  
 Is the record expression to be evaluated as a source record. record_expression can be a column of type Record or result of another function call.  
  
 **string_expression**  
  
 Is the string expression to be evaluated as a record property name.  
  
## Return Types  
 Return type is determined by the record property type and can be any of the [supported types](https://msdn.microsoft.com/en-us/library/azure/dn835065.aspx).  
  
## Examples  
 In this code example, “thresholds” is a reference data name defined on the inputs tab.  
  
```  
SELECT   
    input.DeviceID,  
    thresholds.SensorName  
FROM input  
JOIN thresholds   
ON  
    input.DeviceId = thresholds.DeviceId  
WHERE  
    GetRecordPropertyValue(input.SensorReading, thresholds.SensorName) > thresholds.Value  
```  
  
 Note that you can use dot notation to access record property fields.  
  
```  
SELECT   
    recordColumn.NestedFieldName1.NestedFieldName2  
FROM input  
  
```  
  
  
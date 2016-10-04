---
title: "GetRecordProperties (Azure Stream Analytics)"
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
ms.assetid: 7720ce57-0ef0-406d-84ba-352af8d2dadf
caps.latest.revision: 7
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
# GetRecordProperties (Azure Stream Analytics)
  Returns a dataset with record property names and values. The result of the GetRecordProperties function must be used with the [CROSS APPLY](https://msdn.microsoft.com/en-us/library/azure/dn706229.aspx) operator.  
  
 **Syntax**  
  
```  
GetRecordProperties ( column_reference )  
```  
  
## Arguments  
 **Column_reference**  
  
 Is the column reference expression to be evaluated. Column must be of type Record  
  
## Return Types  
 Returns a dataset with PropertyName and PropertyValue columns.  
  
## Examples  
  
```  
SELECT   
    recordProperty.PropertyName,  
    recordProperty.PropertyValue  
FROM input as event  
CROSS APPLY GetRecordProperties(event.recordField) AS recordProperty  
```  
  
  
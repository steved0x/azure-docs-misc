---
title: "Formatting DateTime Property Values"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 0ff7afef-5b85-44ee-a6eb-17d4dd071f5a
caps.latest.revision: 13
author: tamram
manager: carolz
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
# Formatting DateTime Property Values
`DateTime` property values must be represented as combined Coordinated Universal Time (UTC) values. The `Timestamp` property, which is an opaque property maintained by the Table service, is also represented in this format. UTC formats are described by [ISO 8601](http://go.microsoft.com/fwlink/?LinkId=156016).  
  
 An example of the combined UTC format is as follows. The date is specified first, followed by the literal string "T", which designates the beginning of the time element. The literal string "Z" at the end of the string designates that the time is expressed in UTC:  
  
```  
2009-03-18T04:25:03Z  
```  
  
 The following code example shows one way to construct the combined UTC format from the current UTC date:  
  
```  
string roundtripDateTime = XmlConvert.ToString(DateTime.UtcNow, XmlDateTimeSerializationMode.RoundtripKind);  
```  
  
## See Also  
 [Understanding the Table Service Data Model](../StorageServicesREST/Understanding-the-Table-Service-Data-Model.md)
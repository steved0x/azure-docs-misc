---
title: "Representation of Date-Time Values in Headers"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: d4f67d84-a51c-4ff7-8bd0-0ae206c9e3c9
caps.latest.revision: 22
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
# Representation of Date-Time Values in Headers
Azure storage services follow RFC 1123 for representation of date/time values. This is the preferred format for HTTP/1.1 operations, as described in section 3.3 of the [HTTP/1.1 Protocol Parameters](http://go.microsoft.com/fwlink/?linkid=133333) specification. An example of this format is:  
  
```  
Sun, 06 Nov 1994 08:49:37 GMT  
```  
  
 The following format is also supported, as described in the HTTP/1.1 protocol specification:  
  
```  
Sunday, 06-Nov-94 08:49:37 GMT  
```  
  
 Both are represented in the Coordinated Universal Time (UTC), also known as Greenwich Mean Time.  
  
## See Also  
 [Storage Services REST](../StorageServicesREST/Azure-Storage-Services-REST-API-Reference.md)
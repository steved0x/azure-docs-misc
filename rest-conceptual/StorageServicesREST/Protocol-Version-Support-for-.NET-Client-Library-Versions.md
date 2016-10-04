---
title: "Protocol Version Support for .NET Client Library Versions"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 7dddaa24-5794-417f-a56a-9ab65ec25253
caps.latest.revision: 11
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
# Protocol Version Support for .NET Client Library Versions
The following table shows which storage services REST protocol versions are supported for each version of the .NET Storage Client Library.  
  
|Storage Client Library Version|Underlying REST Protocol Version|  
|------------------------------------|--------------------------------------|  
|1.7|2011-08-18|  
|2.x|2012-02-12|  
|3.x|2013-08-15|  
|4.x|2014-02-14|  
|5.x|2015-02-21|  
|6.x|2015-04-05|  
|7.0|2015-07-08|  
|7.1|2015-12-11|  
  
 For .NET storage client library documentation, see [Storage Client Library .NET](../Topic/Azure%20Storage%20Client%20Library%20for%20.NET.md).  
  
 For a complete list of storage client library versions, see the [Windows Azure Storage NuGet page](https://www.nuget.org/packages/WindowsAzure.Storage/).  
  
> [!NOTE]
>  It is not possible to modify the REST protocol version used by a given client library version. A new major version of the client library usually takes advantage of new features and changes available in a new protocol version of the Azure storage services. Each client library version issues requests only against the protocol version on which it is based.  
  
## See Also  
 [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md)
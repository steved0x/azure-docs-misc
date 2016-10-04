---
title: "Naming Queues and Metadata"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 1675a927-7eff-4385-a6a0-72f22d53c5e1
caps.latest.revision: 24
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
# Naming Queues and Metadata
This topic describes rules for naming queues and queue metadata.  
  
 **Queue Names**  
  
 Every queue within an account must have a unique name. The queue name must be a valid DNS name, and cannot be changed once created. Queue names must confirm to the following rules:  
  
1.  A queue name must start with a letter or number, and can only contain letters, numbers, and the dash (-) character.  
  
2.  The first and last letters in the queue name must be alphanumeric. The dash (-) character cannot be the first or last character. Consecutive dash characters are not permitted in the queue name.  
  
3.  All letters in a queue name must be lowercase.  
  
4.  A queue name must be from 3 through 63 characters long.  
  
 **Metadata Names**  
  
 Metadata for a queue resource is stored as name-value pairs. Beginning with REST API version 2009-09-19, metadata names must adhere to the naming rules for [C# identifiers](http://msdn.microsoft.com/library/aa664670%28VS.71%29.aspx). Existing metadata names that do not adhere to these naming rules can be used with earlier versions of the Queue service, but not with REST API version 2009-09-19 or later.  
  
 Note that metadata names preserve the case with which they were created, but are case-insensitive when set or read. If two or more metadata headers with the same name are submitted for a resource, the Queue service returns status code 400 (Bad Request).  
  
## See Also  
 <xref:Microsoft.WindowsAzure.StorageClient.CloudQueue.Metadata?qualifyHint=True>   
 [Queue Service Concepts](../StorageServicesREST/Queue-Service-Concepts.md)   
 [Addressing Queue Service Resources](../StorageServicesREST/Addressing-Queue-Service-Resources.md)
---
title: "Media Services Management Error Codes"
ms.custom: ""
ms.date: "2016-03-08"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fb7d4575-9ceb-46f9-84da-34ce4df84894
caps.latest.revision: 9
author: "Juliako"
ms.author: "juliako"
manager: "erikre"
translation.priority.mt: 
  - "de-de"
  - "es-es"
  - "fr-fr"
  - "it-it"
  - "ja-jp"
  - "ko-kr"
  - "pt-br"
  - "ru-ru"
  - "zh-cn"
  - "zh-tw"
---
# Media Services Management Error Codes
> [!NOTE]
>  It is now recommended to use  the Azure Resource Manager (ARM) REST API endpoints, as described in [Media Services Management API Reference](../Topic/Media%20Services%20Management%20API%20Reference.md).  
  
 The Media Service Management REST API may return the following error codes. . For more information about status error codes, see [Service Management Status and Error Codes](http://msdn.microsoft.com/en-us/10f8d244-4649-4063-b6c9-7a20765513fa).  
  
## 400 Bad Request  
 Request contains wrong information and is rejected because of one of the following reasons:  
  
-   The specified subscription ID is null or white-space.  
  
-   The specified account name is not valid – A valid account name must be 3-24 lowercase alphanumeric chars.  
  
-   Missing value for a required property (for example, account key).  
  
-   Bad value for requested reserved units.  
  
## 403 Forbidden  
 Request cannot be allowed due to invalid certificate.  
  
## 404 Not Found  
 Request tries to access a resource that does not exist. Reason can be:  
  
-   The specified account name does not exist.  
  
-   The specified account storage account does not exist.  
  
-   The specified media service type does not exist.  
  
## 409 Conflict  
  
-   An account with the specified account name already exists in this subscription.  
  
-   Unable to create a DNS name for specified account.  
  
## 500 Internal Server Error  
 The server encounters an error that stops request processing. The reason could be any unexpected error.  
  
## Sample Error Response  
  
```  
HTTP/1.1 404 The specified account was not found.   
Cache-Control: private   
Content-Length: 68   
Content-Type: application/json; charset=utf-8   
Server: Microsoft-IIS/7.5   
X-AspNet-Version: 4.0.30319   
X-Powered-By: ASP.NET   
Date: Sun, 30 Dec 2012 03:42:28 GMT   
{"Code":"NotFound","Message":"The specified account was not found."}  
  
```
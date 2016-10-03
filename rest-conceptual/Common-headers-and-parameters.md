---
title: "Common headers and parameters"
ms.custom: na
ms.date: 2016-07-21
ms.prod: azure
ms.reviewer: na
ms.service: data-catalog
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: c197d40e-a462-4879-b24a-32731edf5790
caps.latest.revision: 14
author: spelluru
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
# Common headers and parameters
## Common request headers  
  
|**Header**|**Description**  
|---|---  
|Content-Type|Required. Set to "application/json; charset=utf-8".  
|Authorization|Required. Contains authentication token in the format "Bearer {OAuth authorization token}". (Refer to the Azure Active Directory implementation of OAuth 2.0 on how to obtain authorization token).  
|x-ms-client-request-id|Optional.  Provides a client-generated identity of the request in the form of a GUID. Using this header is highly recommended for correlating client-side activities with requests received by the server.  
  
## Common request parameters  
  
|**Parameter**|**Description**  
|---|---  
|api-version|Required. Clients must specify the api-version parameter for every call; if this parameter is not present the service will return status code 400 (BadRequest) and a message stating that api-version is required.  Supported api version: 2016-03-30  
  
## Common response headers  
  
|**Response Header**|**Description**  
|---|---  
|x-ms-request-id|This header uniquely identifies the request that was made and can be used for troubleshooting the request.  
|Location|Contains absolute url which points to the created asset or annotation.  
|Content-Type|application/json; charset=utf-8.  
  
## Error response  
    {  
      "error": {  
        "code": "BadArgument",  
        "message": "'{this type}' is not a valid argument for 'type'."  
      }  
    }  

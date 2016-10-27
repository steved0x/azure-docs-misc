---
title: "Regenerate Media Services Secondary Account Key"
ms.custom: ""
ms.date: "2016-03-08"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b7160757-7e8a-4101-adec-b1341fb6e4d4
caps.latest.revision: 8
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
# Regenerate Media Services Secondary Account Key
> [!NOTE]
>  It is now recommended to use  the Azure Resource Manager (ARM) REST API endpoints, as described in [Media Services Management API Reference](../Topic/Media%20Services%20Management%20API%20Reference.md).  
  
 The `POST` request method described in this topic request to regenerate the specified Media Services account secondary identity key.  
  
 The request may be specified as follows. Replace `<subscription-id>` with your subscription ID, `<accountName>` with your account name:  
  
|||  
|-|-|  
|Method|Request URI|  
|POST|https://endpoint/\<subscriptionId>/services/mediaservices/Accounts/\<accountName>/AccountKeys/Secondary/Regenerate|  
  
 A successful operation returns status code 204 (NoContent). For information about error codes, see [Media Services Management Error Codes](../MediaServicesOperations_RESTAPI/media-services-management-error-codes.md).  
  
## Example  
 See the `RegenerateSecondaryAccountKey` method defined in [How to: Use Media Services Management REST API](../MediaServicesOperations_RESTAPI/how-to--use-media-services-management-rest-api.md).  
  
## See Also  
 [Media Services Operations REST](../MediaServicesOperations_RESTAPI/media-services-operations-rest.md)   
 [Media Services Management Error Codes](../MediaServicesOperations_RESTAPI/media-services-management-error-codes.md)
---
title: "Delete Media Services Account"
ms.custom: ""
ms.date: "2016-03-08"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2dea6c04-a017-48f1-9729-c34706ed8b47
caps.latest.revision: 7
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
# Delete Media Services Account
> [!NOTE]
>  It is now recommended to use  the Azure Resource Manager (ARM) REST API endpoints, as described [Media Services Management API Reference](../Topic/Media%20Services%20Management%20API%20Reference.md).  
  
 The `DELETE` request method described in this topic deletes the specified Media Services account in the specified subscription.  
  
 The request may be specified as follows (replace `<subscription-id>` with your subscription ID, and `<accountName>` with your account name):  
  
|||  
|-|-|  
|Method|Request URI|  
|DELETE|https://endpoint/\<subscriptionId>/services/mediaservices/Accounts/\<accountName>|  
  
 A successful operation returns status code 200 (OK). For information about error codes, see [Media Services Management Error Codes](../MediaServicesOperations_RESTAPI/media-services-management-error-codes.md).  
  
## Example  
 See the `DeleteAccount` method defined in [How to: Use Media Services Management REST API](../MediaServicesOperations_RESTAPI/how-to--use-media-services-management-rest-api.md).  
  
## See Also  
 [Media Services Operations REST](../MediaServicesOperations_RESTAPI/media-services-operations-rest.md)   
 [Media Services Management Error Codes](../MediaServicesOperations_RESTAPI/media-services-management-error-codes.md)
---
title: "Update Storage Account Key (Media Services)"
ms.custom: ""
ms.date: "2016-03-08"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ce787c7a-f3b5-41dc-88de-8d4c5cc5c1cd
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
# Update Storage Account Key (Media Services)
> [!NOTE]
>  It is now recommended to use  the Azure Resource Manager (ARM) REST API endpoints, as described in [Media Services Management API Reference](../Topic/Media%20Services%20Management%20API%20Reference.md).  
  
 The `PUT` request method described in this topic synchronizes Media Services storage account records with the storage account key. The new key is returned in the request body.  
  
 For example, if you regenerate the storage account key using portal, you can call this method to get the updated key value.  
  
 The request may be specified as follows. Replace `<subscription-id>` with your subscription ID, `<accountName>` with your account name, and `<storageAccount>` with the Storage Account name that is associated with the specified Media Services account:  
  
|||  
|-|-|  
|Method|Request URI|  
|PUT|https://endpoint/\<subscriptionId>/services/mediaservices/Accounts/\<accountName>/StorageAccounts/\<storageAccountName>/Key|  
  
 A successful operation returns status code 204 (NoContent). For information about error codes, see [Media Services Management Error Codes](../MediaServicesOperations_RESTAPI/media-services-management-error-codes.md).  
  
## Example  
 See the `SynchronizeStorageAccountKey` method in [How to: Use Media Services Management REST API](../MediaServicesOperations_RESTAPI/how-to--use-media-services-management-rest-api.md).  
  
## See Also  
 [Media Services Operations REST](../MediaServicesOperations_RESTAPI/media-services-operations-rest.md)   
 [Media Services Management Error Codes](../MediaServicesOperations_RESTAPI/media-services-management-error-codes.md)
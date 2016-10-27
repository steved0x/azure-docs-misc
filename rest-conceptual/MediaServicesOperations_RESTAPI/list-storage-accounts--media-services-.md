---
title: "List Storage Accounts (Media Services)"
ms.custom: ""
ms.date: "2016-03-08"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b2490a03-0293-490c-9539-c90b03348f94
caps.latest.revision: 10
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
# List Storage Accounts (Media Services)
> [!NOTE]
>  It is now recommended to use  the Azure Resource Manager (ARM) REST API endpoints, as described in [Media Services Management API Reference](../Topic/Media%20Services%20Management%20API%20Reference.md).  
  
 The `GET` request method described in this topic returns a list of `StorageAccountDetails` for the Storage Account associated with the specified Media Services account. The data contract for `StorageAccountDetails` is defined later in this topic.  
  
 The request may be specified as follows (replace `<subscription-id>` with your subscription ID, and `<accountName>` with your account name.):  
  
|||  
|-|-|  
|Method|Request URI|  
|GET|https://endpoint/\<subscriptionId>/services/mediaservices/Accounts/\<accountName>/StorageAccounts|  
  
 A successful operation returns status code 200 (OK). For information about error codes, see [Media Services Management Error Codes](../MediaServicesOperations_RESTAPI/media-services-management-error-codes.md).  
  
 When attaching multiple storage accounts to your Media Services account, the following considerations apply:  
  
-   All storage accounts attached to a Media Services account must be in the same data center as the Media Services account.  
  
-   Currently, once a storage account is attached to the specified Media Services account, it cannot be detached.  
  
-   Primary storage account is the one indicated during Media Services account creation time. Currently, you cannot change the default storage account.  
  
## Data Contract  
 The data contract for `StorageAccountDetails` is defined as follows:  
  
```  
[DataContract]   
public class StorageAccountDetails   
{   
    public StorageAccountDetails();   
  
    [DataMember]   
    public string BlobStorageEndPoint { get; set; }   
  
    [DataMember]   
    public string StorageAccountName { get; set; }   
  
    [DataMember]   
    public bool IsDefault { get; set; }   
}  
  
```  
  
 For more information about request and response formats, see [Media Services Operations REST](../MediaServicesOperations_RESTAPI/media-services-operations-rest.md)  
  
## Example  
 See the `ListStorageAccountDetails` method in [How to: Use Media Services Management REST API](../MediaServicesOperations_RESTAPI/how-to--use-media-services-management-rest-api.md).  
  
## See Also  
 [Media Services Operations REST](../MediaServicesOperations_RESTAPI/media-services-operations-rest.md)   
 [Media Services Management Error Codes](../MediaServicesOperations_RESTAPI/media-services-management-error-codes.md)
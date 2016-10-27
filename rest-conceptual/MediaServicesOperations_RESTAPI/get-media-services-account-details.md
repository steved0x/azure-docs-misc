---
title: "Get Media Services Account Details"
ms.custom: ""
ms.date: "2016-03-08"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7fb7e81c-8abc-47f2-bbec-4939eac10fcc
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
# Get Media Services Account Details
> [!NOTE]
>  It is now recommended to use  the Azure Resource Manager (ARM) REST API endpoints, as described in [Media Services Management API Reference](../Topic/Media%20Services%20Management%20API%20Reference.md).  
  
 The `GET` request method described in this topic returns an `AccountDetails` object for the specified Media Services account. The data contract for `AccountDetails` is defined later in this topic.  
  
 The request may be specified as follows (replace `<subscription-id>` with your subscription ID, and `<accountName>` with your account name):  
  
|||  
|-|-|  
|Method|Request URI|  
|GET|https://endpoint/\<subscriptionId>/services/mediaservices/Accounts/\<accountName>|  
  
 A successful operation returns status code 200 (OK). For information about error codes, see [Media Services Management Error Codes](../MediaServicesOperations_RESTAPI/media-services-management-error-codes.md).  
  
## Data Contract  
 The data contract for `AccountDetails` is defined as follows:  
  
```  
[DataContract]   
public class AccountDetails   
{   
    public AccountDetails();   
  
    [DataMember]   
    public string AccountKey { get; set; }   
  
    [DataMember]   
    public AccountKeys AccountKeys { get; set; }   
  
    [DataMember]   
    public string AccountName { get; set; }   
  
    [DataMember]   
    public string AccountRegion { get; set; }   
  
    [DataMember]   
    public string StorageAccountName { get; set; } }  
  
```  
  
 For more information about request and response formats, see [Media Services Operations REST](../MediaServicesOperations_RESTAPI/media-services-operations-rest.md)  
  
## Example  
 See the `GetAccountDetails` method defined in [How to: Use Media Services Management REST API](../MediaServicesOperations_RESTAPI/how-to--use-media-services-management-rest-api.md).  
  
## See Also  
 [Media Services Operations REST](../MediaServicesOperations_RESTAPI/media-services-operations-rest.md)   
 [Media Services Management Error Codes](../MediaServicesOperations_RESTAPI/media-services-management-error-codes.md)
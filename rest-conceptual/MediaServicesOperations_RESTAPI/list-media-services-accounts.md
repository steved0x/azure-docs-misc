---
title: "List Media Services Accounts"
ms.custom: ""
ms.date: "2016-03-08"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a6cd024d-1802-4a5a-a1a7-ff03647aaf61
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
# List Media Services Accounts
> [!NOTE]
>  It is now recommended to use  the Azure Resource Manager (ARM) REST API endpoints, as described in [Media Services Management API Reference](../Topic/Media%20Services%20Management%20API%20Reference.md).  
  
 The `GET` request method described in this topic returns a collection of `AzureMediaServicesResource`s in the specified subscription. The data contract for `AzureMediaServicesResource` is defined later in this topic.  
  
 The request may be specified as follows (replace `<subscription-id>` with your subscription ID):  
  
|||  
|-|-|  
|Method|Request URI|  
|GET|https://endpoint/\<subscriptionId>/services/mediaservices/Accounts|  
  
 A successful operation returns status code 200 (OK). For information about error codes, see [Media Services Management Error Codes](../MediaServicesOperations_RESTAPI/media-services-management-error-codes.md).  
  
## Data Contract  
 The data contract for `AzureMediaServicesResource` is defined as follows:  
  
```  
[CollectionDataContract(Name = "ServiceResources", ItemName = "ServiceResource", Namespace = "http://schemas.microsoft.com/windowsazure")]   
public class AzureMediaServicesResourceCollection : Collection<AzureMediaServicesResource>   
{   
    public AzureMediaServicesResourceCollection();   
    public AzureMediaServicesResourceCollection(IEnumerable<AzureMediaServicesResource> resources);  
}  
  
[DataContract(Namespace = "http://schemas.microsoft.com/windowsazure", Name = "ServiceResource")]   
public class AzureMediaServicesResource   
{   
    public AzureMediaServicesResource();   
  
    [DataMember(EmitDefaultValue = false, Order = 5)]   
    public Guid AccountId { get; set; }   
  
    [DataMember(EmitDefaultValue = false, Order = 0)]   
    public string Name { get; set; }   
  
    [DataMember(EmitDefaultValue = false, Order = 4)]   
    public Uri ParentLink { get; set; }  
  
    [DataMember(EmitDefaultValue = false, Order = 3)]   
    public Uri SelfLink { get; set; }   
  
    [DataMember(EmitDefaultValue = false, Order = 2)]   
    public string State { get; set; }  
  
    [DataMember(EmitDefaultValue = false, Order = 1)]   
    public string Type { get; set; }   
}  
  
```  
  
 For more information about request and response formats, see [Media Services Operations REST](../MediaServicesOperations_RESTAPI/media-services-operations-rest.md)  
  
## Example  
 See the `ListSubscriptionAccounts` method defined in [How to: Use Media Services Management REST API](../MediaServicesOperations_RESTAPI/how-to--use-media-services-management-rest-api.md).  
  
## See Also  
 [Media Services Operations REST](../MediaServicesOperations_RESTAPI/media-services-operations-rest.md)   
 [Media Services Management Error Codes](../MediaServicesOperations_RESTAPI/media-services-management-error-codes.md)
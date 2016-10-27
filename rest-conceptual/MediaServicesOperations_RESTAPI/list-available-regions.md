---
title: "List Available Regions"
ms.custom: ""
ms.date: "2016-03-08"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c9a9b2f1-8972-4764-9d83-eeed65a86ef2
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
# List Available Regions
> [!NOTE]
>  It is now recommended to use  the Azure Resource Manager (ARM) REST API endpoints, as described in [Media Services Management API Reference](../Topic/Media%20Services%20Management%20API%20Reference.md).  
  
 The `GET` request method described in this topic returns `SupportedRegion`s in the specified subscription. The data contract for `SupportedRegion` is defined later in this topic.  
  
 The request may be specified as follows (replace `<subscription-id>` with your subscription ID):  
  
|||  
|-|-|  
|Method|Request URI|  
|GET|https://endpoint/\<subscriptionId>/services/mediaservices/SupportedRegions|  
  
 A successful operation returns status code 200 (OK). For information about error codes, see [Media Services Management Error Codes](../MediaServicesOperations_RESTAPI/media-services-management-error-codes.md).  
  
## Data Contract  
 The data contract for `SupportedRegion` is defined as follows:  
  
```  
[DataContract]   
public class SupportedRegion   
{   
    public SupportedRegion();   
    [DataMember]   
    public string RegionName { get; set; }   
}  
  
```  
  
 For more information about request and response formats, see [Media Services Operations REST](../MediaServicesOperations_RESTAPI/media-services-operations-rest.md)  
  
## Example  
 See the `ListAvailableRegions` method defined in [How to: Use Media Services Management REST API](../MediaServicesOperations_RESTAPI/how-to--use-media-services-management-rest-api.md).  
  
## See Also  
 [Media Services Operations REST](../MediaServicesOperations_RESTAPI/media-services-operations-rest.md)   
 [Media Services Management Error Codes](../MediaServicesOperations_RESTAPI/media-services-management-error-codes.md)
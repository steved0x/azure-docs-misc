---
title: "Create Media Services Account"
ms.custom: ""
ms.date: "2016-03-08"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0e146990-ecda-450e-9478-6f799fcc950b
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
# Create Media Services Account
> [!NOTE]
>  It is now recommended to use  the Azure Resource Manager (ARM) REST API endpoints, as described in [Media Services Management API Reference](../Topic/Media%20Services%20Management%20API%20Reference.md).  
  
 The `POST` request method described in this topic creates a Media Services account in the specified subscription. Both request and response follow the data contract described later in this section.  
  
 The request may be specified as follows (replace `<subscription-id>` with your subscription ID):  
  
|||  
|-|-|  
|Method|Request URI|  
|POST|https://endpoint/\<subscriptionId>/services/mediaservices/Accounts|  
  
 A successful operation returns status code 201 (Created). For information about error codes, see [Media Services Management Error Codes](../MediaServicesOperations_RESTAPI/media-services-management-error-codes.md).  
  
## Data Contract  
 The data contract for `AccountCreationRequest` is defined as follows:  
  
```  
[DataContract]   
public class AccountCreationRequest   
{   
    public AccountCreationRequest();   
  
    [DataMember]   
    public string AccountName { get; set; }   
  
    [DataMember]   
    public string BlobStorageEndpointUri { get; set; }   
  
    [DataMember]   
    public string Region { get; set; }   
  
    [DataMember]   
    public string StorageAccountKey { get; set; }   
  
    [DataMember]   
    public string StorageAccountName { get; set; }   
}  
  
```  
  
 The data contract for `AccountCreationResult` is defined as follows:  
  
```  
[DataContract]   
public sealed class AccountCreationResult   
{   
    public Guid AccountId { get; }   
    public string AccountName { get; }   
    public string Reason { get; }   
  
    [DataMember]   
    public HttpStatusCode StatusCode { get; set; }   
    public string Subscription { get; }   
  
    public static AccountCreationResult Failed(string reason, HttpStatusCode result = HttpStatusCode.BadRequest);   
    public static AccountCreationResult Success(Guid accountId, string accountName, string subscription); }  
  
```  
  
 For more information about request and response formats, see [Media Services Operations REST](../MediaServicesOperations_RESTAPI/media-services-operations-rest.md)  
  
## Example  
 See the `CreateMediaServiceAccountUsingXmlContentType` method defined in [How to: Use Media Services Management REST API](../MediaServicesOperations_RESTAPI/how-to--use-media-services-management-rest-api.md).  
  
## See Also  
 [Media Services Operations REST](../MediaServicesOperations_RESTAPI/media-services-operations-rest.md)   
 [Media Services Management Error Codes](../MediaServicesOperations_RESTAPI/media-services-management-error-codes.md)
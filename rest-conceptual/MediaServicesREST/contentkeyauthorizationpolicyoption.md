---
title: "ContentKeyAuthorizationPolicyOption"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2a0a0efb-5127-48e2-84ea-9a31451d7284
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
# ContentKeyAuthorizationPolicyOption
Media Services supports multiple ways of authenticating users who make key requests. The content key authorization policy must be configured by you and met by the client (player) in order for the key to be delivered to the client. The content key authorization policy could have one or more authorization restrictions: open, token restriction, or IP restriction. You use `ContentKeyAuthorizationPolicyOption` to specify the authorization options. You then add the created options to `ContentKeyAuthorizationPolicy`.  
  
 Note that the Key Delivery service caches `ContentKeyAuthorizationPolicy` and its related objects (policy options and restrictions) for 15 minutes.  If you create a `ContentKeyAuthorizationPolicy` and specify to use a “Token” restriction, then test it, and then update the policy to “Open” restriction, it will take roughly 15 minutes before the policy switches to the “Open” version of the policy.  
  
 This topic describes `ContentKeyAuthorizationPolicyOption` and shows how to use this entity. For a more complete example, that shows how to associate `ContentKeyAuthorizationPolicyOption` with `ContentKeyAuthorizationPolicy`, see [ContentKeyAuthorizationPolicy](../MediaServicesREST/contentkeyauthorizationpolicy.md).  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://msdn.microsoft.com/en-us/42ae6204-93bc-4797-bf40-1c68512cfb73).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
##  <a name="mediaprocessor_entity_properties"></a> ContentKeyAuthorizationPolicyOption Entity Properties  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`Id`<br /><br /> Read-only. Set by Media Services.|Edm.String|Unique identifier.|  
|`Name`|Edm.String|Friendly name of the authorization policy.|  
|`KeyDeliveryType`<br /><br /> Required.|Edm. Int32|Delivery method of the content key to the client.<br /><br /> KeyDeliveryType could be one of the following: None = 0, PlayReadyLicense = 1, BaselineHttp = 2).|  
|`KeyDeliveryConfiguration`|Edm.String|Xml data, specific to the key delivery type that defines how the key is delivered to the client.|  
|`Restrictions`<br /><br /> Required.|A collection of [ContentKeyAuthorizationPolicyRestriction ComplexType Properties](#restrions)s.|Requirements defined in each restriction must be met in order to deliver the key using the key delivery data.|  
  
##  <a name="restrions"></a> ContentKeyAuthorizationPolicyRestriction ComplexType Properties  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`Name`|Edm.String|Friendly name of the restriction.|  
|`KeyRestrictionType`<br /><br /> Required.|Edm. Int32|Type of the restriction.<br /><br /> KeyRestrictionType could be one of the following: Open = 0, TokenRestricted = 1, IPRestricted = 2.|  
|`Requirements`|Edm. String|Restriction requirements.|  
  
## Create ContentKeyAuthorizationPolicyOption  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 The following example creates a ContentKeyAuthorizationPolicyOption with the following values set: an `Open` authorization restriction (`"KeyRestrictionType":0`) and BaselineHttp (MPEG baseline HTTP key protocol) key delivery method (`"KeyDeliveryType":2`). You can try out the example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab.  
  
 Make sure to use valid redirected host URI and authorization bearer token values. For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
POST https://testrest.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1  
  
Content-Type: application/json  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json  
Accept-Charset: UTF-8  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
x-ms-version: 2.11  
```  
  
 Request body:  
  
```  
  
{    
   "Name":"policy",  
   "KeyDeliveryType":2,  
   "KeyDeliveryConfiguration":"",  
   "Restrictions":[    
      {    
         "Name":"HLS Open Authorization Policy",  
         "KeyRestrictionType":0,  
         "Requirements":null  
      }  
   ]  
}  
```  
  
 If successful, a **HTTP/1.1 201 Created** status code is returned along with a representation of the created entity in the response body.  
  
 The following example creates a ContentKeyAuthorizationPolicyOption with the following values set: a `Token` authorization restriction (`"KeyRestrictionType":1`) and BaselineHttp (MPEG baseline HTTP key protocol) key delivery method (`"KeyDeliveryType":2`).  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
POST https:/testrest.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1  
  
Content-Type: application/json  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json  
Accept-Charset: UTF-8  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
x-ms-version: 2.11  
  
```  
  
 Request body:  
  
```  
{    
   "Name":"Token option for HLS",  
   "KeyDeliveryType":2,  
   "KeyDeliveryConfiguration":null,  
   "Restrictions":[    
      {    
         "Name":"Token Authorization Policy",  
         "KeyRestrictionType":1,  
         "Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>dliLr1QQJrATxNuoss2Btvk1KxcDJDHvTgu7fII5LEMGAt1p6J1YAD7I0EVd6D69nEkNUlkSDXfgaJ3cswrf8g==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>tqdCrSPGDZYJ4l3YyWR1NH7OdTvucBm7bU/ZQKPszV/hR54saMgyJK9bA9bay996NtNpcA0OruHETvy885g46A==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>JWT</TokenType></TokenRestrictionTemplate>"  
      }  
   ]  
}  
  
```
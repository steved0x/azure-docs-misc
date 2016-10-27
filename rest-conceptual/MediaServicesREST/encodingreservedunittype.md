---
title: "EncodingReservedUnitType"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 15c36cc3-1cbd-4927-9780-935241768161
caps.latest.revision: 13
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
# EncodingReservedUnitType
A Media Services account is associated with a `Reserved Unit Type` which determines the speed with which your encoding jobs are processed. You can pick between the following reserved unit types: `S1`, `S2`, or `S3`.  
  
 In addition to specifying the reserved unit type, you can specify to provision your account with encoding reserved units. The number of provisioned encoding reserved units determines the number of media tasks that can be processed concurrently in a given account. For example, if your account has 5 reserved units, then 5 media tasks will be running concurrently as long as there are tasks to be processed. The remaining tasks will wait in the queue and will get picked up for processing sequentially as soon as a running task finishes. If an account does not have any reserved units provisioned, then tasks will be picked up sequentially. In this case, the wait time between one task finishing and the next one starting will depend on the availability of resources in the system.  
  
 To update the reserved unit type or the number of reserved units, use the REST API described in this topic. For more information, see the [Scaling media processing](https://azure.microsoft.com/documentation/articles/media-services-scale-media-processing-overview/).  
  
 By default, every Media Services account can scale to up to 25 encoding units. To request a higher limit, see [How to request a higher limit for updatable quotas](http://msdn.microsoft.com/en-us/82f7e538-6bdf-4883-aa50-24574cc4996e).  
  
 The highest number of units specified for the 24-hour period is used in calculating the cost.  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://msdn.microsoft.com/en-us/42ae6204-93bc-4797-bf40-1c68512cfb73).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
 This topic gives an overview of the `EncodingReservedUnitType` entity and also demonstrates how to execute various operations with the Media Services REST API.  
  
-   [Get EncodingReservedUnitType](#get_EncodingReservedUnitType)  
  
-   [Update EncodingReservedUnitType](#update_EncodingReservedUnitType)  
  
## EncodingReservedUnitType Entity  
 The `EncodingReservedUnitType` entity contains the following properties.  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`AccountId`<br /><br /> Required. Read-Only|Edm.GUID|Media Services account Id.|  
|`ReservedUnitType`<br /><br /> Required.|Edm.Int|Reserved unit type can be one of the following: `S1` (0), `S2` (1), `S3` (2).|  
|`CurrentReservedUnits`<br /><br /> Required.|Edm.Int|Current reserved units. The number of the encoding reserved units that you want to be provisioned for this account.<br /><br /> By default, every Media Services account can scale to up to 25 encoding units. To request a higher limit, see [How to request a higher limit for updatable quotas](http://msdn.microsoft.com/en-us/82f7e538-6bdf-4883-aa50-24574cc4996e).|  
|`MaxReservableUnits`<br /><br /> Read-only.|Edm.Int|Maximum number of units that can be reserved for the account.|  
  
##  <a name="get_EncodingReservedUnitType"></a> Get EncodingReservedUnitType  
 Details about the encoding reserved unit type associated with your account can be retrieved by using a GET HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|Gets information about the encoding reserved unit type associated with your account.<br /><br /> https://media.windows.net/api/EncodingReservedUnitTypes|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
GET https://testrest.cloudapp.net/api/EncodingReservedUnitTypes HTTP/1.1  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json;odata=minimalmetadata  
Accept-Charset: UTF-8  
x-ms-version: 2.11  
Content-Type: application/json;odata=minimalmetadata  
Host: <redirected host URI>  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
  
```  
  
 If successful, this operation returns **HTTP/1.1 200 OK**.  
  
##  <a name="update_EncodingReservedUnitType"></a> Update EncodingReservedUnitType  
 Updates EncodingReservedUnitType properties.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|PATCH/PUT/MERGE<br /><br /> For more information about these operations, see [PATCH/PUT/MERGE](http://msdn.microsoft.com/library/dd541276.aspx).|https://media.windows.net/api/EncodingReservedUnitTypes(guid'*accountid*')|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
  
PUT https://testrest.cloudapp.net/api/EncodingReservedUnitTypes(guid'61318ce3-0629-4400-8a1b-e716bc501314') HTTP/1.1  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json;odata=minimalmetadata  
Accept-Charset: UTF-8  
x-ms-version: 2.11  
Content-Type: application/json;odata=minimalmetadata  
Host: <redirected host URI>  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
  
```  
  
 Request body:  
  
```  
{CurrentReservedUnits:1}  
```  
  
 If successful, this operation returns **HTTP/1.1 204 No Content**.
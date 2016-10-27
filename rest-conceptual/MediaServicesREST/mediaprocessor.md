---
title: "MediaProcessor"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 32cf9c3a-c246-4e1b-9a1f-c40029e9d553
caps.latest.revision: 24
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
# MediaProcessor
A media processor transforms media content into a different output. For example, you can use a media processor to transcode video from one bitrate and codec into another or to watermark a video. For a list of Microsoft Azure Media Services MediaProcessors, see [Get a Media Processor](http://msdn.microsoft.com/en-us/76910667-c9db-4217-b7f7-c4a1a86c1a19).  
  
 This topic gives an overview of the `MediaProcessor` entity and also demonstrates how to execute various operations with the Media Services REST API.  
  
-   [MediaProcessor Entity Properties](../MediaServicesREST/mediaprocessor.md#mediaprocessor_entity_properties)  
  
-   [List MediaProcessors](../MediaServicesREST/mediaprocessor.md#list_mediaprocessors)  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://msdn.microsoft.com/en-us/42ae6204-93bc-4797-bf40-1c68512cfb73).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
##  <a name="mediaprocessor_entity_properties"></a> MediaProcessor Entity Properties  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`Id`<br /><br /> Read-only. Set by Media Services.|Edm.String|Unique identifier.|  
|`Name`<br /><br /> Read-only. Set by Media Services.|Edm.String|The friendly name of the MediaProcessor.|  
|`Description`<br /><br /> Read-only. Set by Media Services.|Edm.String|A description about the MediaProcessor.|  
|`Sku`<br /><br /> Read-only. Set by Media Services.|Edm.String|The SKU of the MediaProcessor.|  
|`Vendor`<br /><br /> Read-only. Set by Media Services.|Edm.String|The vendor name of the MediaProcessor|  
|`Version`<br /><br /> Read-only. Set by Media Services.|Edm.String|The version of the MediaProcessor.|  
  
##  <a name="list_mediaprocessors"></a> List MediaProcessors  
 MediaProcessors can be retrieved using a GET HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/MediaProcessors|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
GET https://media.windows.net/API/MediaProcessors HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337240173&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kzBQXYnddSnOK1Arueh7ZoOIzibNRotOfV66K1hobSc%3d  
Host: media.windows.net  
```  
  
## See Also  
 [ContentKey](../MediaServicesREST/contentkey.md)   
 [Asset](../MediaServicesREST/asset.md)   
 [AccessPolicy](../MediaServicesREST/accesspolicy.md)   
 [AssetFile](../MediaServicesREST/assetfile.md)   
 [JobTemplate](../MediaServicesREST/jobtemplate.md)   
 [Locator](../MediaServicesREST/locator.md)   
 [Job](../MediaServicesREST/job.md)   
 [Task](../MediaServicesREST/task.md)   
 [TaskTemplate](../MediaServicesREST/tasktemplate.md)   
 [Quotas and Limitations](http://msdn.microsoft.com/en-us/82f7e538-6bdf-4883-aa50-24574cc4996e)
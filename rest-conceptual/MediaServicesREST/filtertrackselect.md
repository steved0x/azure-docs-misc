---
title: "FilterTrackSelect"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b5fadb63-92c2-4424-92d5-e6da9efbb4ee
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
# FilterTrackSelect
`FilterTrackSelect` is used by manifest filters ([AssetFilter](../MediaServicesREST/assetfilter.md)s and global [Filter](../MediaServicesREST/filter.md)s). It contains a collection of `FilterTrackPropertyCondition`s.  
  
 For a detailed overview and code samples of dynamically generated manifests, see [Dynamic manifests overview](https://azure.microsoft.com/documentation/articles/media-services-dynamic-manifest-overview/).  
  
 Also, see [Filter](../MediaServicesREST/filter.md) and [AssetFilter](../MediaServicesREST/assetfilter.md).  
  
 This topic describes the `FilterTrackSelect` and `FilterTrackPropertyCondition` entities.  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://msdn.microsoft.com/en-us/42ae6204-93bc-4797-bf40-1c68512cfb73).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
## FilterTrackSelect properties  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`PropertyConditions`|Collection of [FilterTrackPropertyCondition properties](#FilterTrackPropertyCondition)|Contains a collection of `FilterTrackPropertyCondition`s.|  
  
##  <a name="FilterTrackPropertyCondition"></a> FilterTrackPropertyCondition properties  
 `FilterTrackPropertyCondition` enables you to specify based on which conditions the tracks of your stream (live or video-on-demand) should be included into dynamically created manifest.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`Property`|Edm.String|Allowed properties are:<br /><br /> `Type` - type of the track.<br /><br /> `Name` -  name of the track.<br /><br /> `Language` - track language.<br /><br /> `FourCC` - track FourCC.<br /><br /> `Bitrate` - bitrate of the track.|  
|`Value`|Edm.String|Allowed values for the following properties are:<br /><br /> -   `Type`<br />     The following values are allowed: `video`, `audio`, or `text`.<br />-   `Name`<br />-   `Language`<br />     Tag of a language you want to include, as specified in `RFC 5646`. For example, `en`.<br />-   `FourCC`<br />     The first element of codecs format, as specified in `RFC 6381`.<br />-   `Bitrate`<br />     A range of bitrates or a specific bitrate. For example, `0-2427000`.|  
|`Operator`|Edm.String|Allowed values are: `Equal` and `notEqual`.|
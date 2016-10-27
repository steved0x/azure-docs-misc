---
title: "AssetFilter"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 41a1076e-fbd9-49ef-a70f-c1006dd32231
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
# AssetFilter
`AssetFilter`s are used to define filters for your asset’s streaming manifests. Defined filters can be applied to any of the following streaming protocols: HLS, MPEG-DASH, Smooth Streaming, and HDS. Media Services dynamically generates manifests based on specified filters. Filters can be defined at a global level ([Filter](../MediaServicesREST/filter.md)) or asset level (`AssetFilter`). Use `AssetFilter` to apply filters to a specific asset. Use `Filter` to apply filters to any of your assets.  
  
 For a detailed overview and code samples of dynamically generated manifests, see [Dynamic manifests overview](https://azure.microsoft.com/documentation/articles/media-services-dynamic-manifest-overview/).  
  
 This topic gives an overview of the `AssetFilter` entity (used to define local filters) and also demonstrates how to execute various operations with the Media Services REST API.  
  
-   [AssetFilter Properties](#assetilter_properties)  
  
-   [Create an AssetFilter](#create_a_filter)  
  
-   [List AssetFilters](#list_filters)  
  
-   [Update a Filter](#update_a_filter)  
  
-   [Delete a Filter](#delete_a_filter)  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://msdn.microsoft.com/en-us/42ae6204-93bc-4797-bf40-1c68512cfb73).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
##  <a name="assetilter_properties"></a> AssetFilter properties  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`Id`<br /><br /> Read-only. Set by Media Services at creation time.|Edm.String|Unique identifier.|  
|`ParentAssetId`|Edm.String|The Id of a parent Asset that contains a collection of these filters.|  
|`Name`|Edm.String|Friendly name for the AssetFilter.|  
|`PresentationTimeRange`|[PresentationTimeRange](../MediaServicesREST/presentationtimerange.md)|The `PresentationTimeRange` rule group is used for filtering manifest start/end points, presentation window length, and the live start position. Media Services uses intersections of multiple ranges to define the final presentation window.|  
|`Tracks`|[FilterTrackSelect](../MediaServicesREST/filtertrackselect.md)|Contains a collection of `FilterTrackPropertyCondition`s.|  
|`FirstQuality`|FirstQuality|First Quality of Manifest Filter, indicates the first quality bitrate for HLS.|  
  
##  <a name="create_a_filter"></a> Create a filter  
 Create a filter using HTTP POST request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/API/AssetFilters|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab.  
  
 Make sure to use valid redirected host URI and authorization bearer token values. For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers  
  
```  
POST https://media.windows.net/API/AssetFilters HTTP/1.1  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
Content-Type: application/json  
Accept: application/json  
Accept-Charset: UTF-8  
Authorization: Bearer <token value>  
x-ms-version: 2.11  
x-ms-client-request-id: 00000000-0000-0000-0000-000000000000  
Host: media.windows.net  
  
```  
  
 Request body  
  
```  
  
{    
   "Name":"TestFilter",  
   "ParentAssetId":"nb:cid:UUID:536e555d-1500-80c3-92dc-f1e4fdc6c592",  
   "PresentationTimeRange":{    
      "StartTimestamp":"0",  
      "EndTimestamp":"9223372036854775807",  
      "PresentationWindowDuration":"12000000000",  
      "LiveBackoffDuration":"0",  
      "Timescale":"10000000"  
   },  
   "Tracks":[    
      {    
         "PropertyConditions":  
              [    
            {    
               "Property":"Type",  
               "Value":"audio",  
               "Operator":"Equal"  
            },  
            {    
               "Property":"Bitrate",  
               "Value":"0-2147483647",  
               "Operator":"Equal"  
            }  
         ]  
      }  
   ]  
}  
  
```  
  
### Response  
  
```  
HTTP/1.1 201 Created  
. . .  
  
```  
  
##  <a name="list_filters"></a> List filters  
 Return all AssetFilters associated with an asset.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/Assets('*assetId*')/AssetFilters()|HTTP/1.1|  
  
 Return a specific AssetFilters by specifying the AssetFilter Id that was returned when the entity was created.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/ AssetFilters('*assetFilterID*')|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab.  
  
 Make sure to use valid redirected host URI and authorization bearer token values. For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Get all AssetFilters associated with an asset.  
  
```  
GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
Accept: application/json  
Accept-Charset: UTF-8  
Authorization: Bearer <token value>  
x-ms-version: 2.11  
x-ms-client-request-id: 00000000-0000-0000-0000-000000000000  
Host: media.windows.net  
  
```  
  
 Get an AssetFilter based on its ID.  
  
```  
GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
Accept: application/json  
Accept-Charset: UTF-8  
Authorization: Bearer <token value>  
x-ms-version: 2.11  
x-ms-client-request-id: 00000000-0000-0000-0000-000000000000  
Host: media.windows.net  
  
```  
  
##  <a name="update_a_filter"></a> Update a filter  
 Use PATCH, PUT or MERGE to update an AssetFilter with new property values.  
  
> [!NOTE]
>  If you update a filter, it can take up to 2 minutes for streaming endpoint to refresh the rules. If the content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures. It is recommend to clear the cache after updating the filter. If this option is not possible, consider using a different filter.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|PATCH/PUT/MERGE<br /><br /> For more information about these operations, see [PATCH/PUT/MERGE](http://msdn.microsoft.com/library/dd541276.aspx).|https://media.windows.net/api/Filters(‘*filterName*’)|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab.  
  
 Make sure to use valid redirected host URI and authorization bearer token values. For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
MERGE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter')  HTTP/1.1  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
Content-Type: application/json  
Accept: application/json  
Accept-Charset: UTF-8  
Authorization: Bearer <token value>  
x-ms-version: 2.11  
x-ms-client-request-id: 00000000-0000-0000-0000-000000000000  
Host: media.windows.net  
  
```  
  
 Request body:  
  
```  
{  
   "Tracks":[    
      {    
         "PropertyConditions":  
         [    
            {    
               "Property":"Type",  
               "Value":"audio",  
               "Operator":"Equal"  
            },  
            {    
               "Property":"Bitrate",  
               "Value":"0-2147483647",  
               "Operator":"Equal"  
            }  
         ]  
      }  
   ]  
}  
  
```  
  
##  <a name="delete_a_filter"></a> Delete a filter  
 Filters can be deleted using a HTTP DELETE request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|DELETE|https://media.windows.net/API/AssetFilters('*assetFilterId*')|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab.  
  
 Make sure to use valid redirected host URI and authorization bearer token values. For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
Accept: application/json  
Accept-Charset: UTF-8  
Authorization: Bearer <token value>  
x-ms-version: 2.11  
Host: media.windows.net  
  
```
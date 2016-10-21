---
title: "Update Annotation"
ms.custom: na
ms.date: 2016-07-21
ms.prod: azure
ms.reviewer: na
ms.service: data-catalog
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 2b6dd7d3-f464-427b-a934-069bf2bc6151
caps.latest.revision: 22
author: spelluru
manager: jhubbard
translation.priority.mt: 
  - de-de
  - es-es
  - fr-fr
  - it-it
  - ja-jp
  - ko-kr
  - pt-br
  - ru-ru
  - zh-cn
  - zh-tw
---
# Update Annotation
---  
[Request](#request) | [Response](#response)  
<a name="top"/>  
  
The **Update Annotation** operation updates an annotation.  
The items can optionally contain ETag values to enable optimistic concurrency control for them.  
<a name="request"/>  
## Request  
PUT https://api.azuredatacatalog.com/catalogs/{catalog_name}/views/{view_name}/{view_item_id}/{nested_view_name}/{nested_non_singleton_view_item_id}?api-version={api-version}  
PUT https://api.azuredatacatalog.com/catalogs/{catalog_name}/views/{view_name}/{view_item_id}/{nested_view_name}?api-version={api-version}  
  
> [AZURE.NOTE] Some HTTP client implementations may automatically re-issue requests in response to a 302 from the server, but typically strip **Authorization headers** from the request. Since the Authorization header is required to make requests to ADC, you must ensure the Authorization header is still provided when re-issuing a request to a redirect location specified by ADC. Below is sample code demonstrating this using the .NET HttpWebRequest object.  
  
### Uri parameters  
|Name|Description|Data Type  
|-|-|-  
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String  
|view_name|Name of Data Asset View.|String  
|view_item_id|Id of a View item.|String  
|nested_view_name|Name of a nested View.|String  
|nested_non_singleton_view_item_id|Id of a nested non-singleton View item. Must be provided for a non-singleton view.|String  
|api-version|The API version.|String  
  
### PUT example for a singleton Documentation view  
PUT https://api.azuredatacatalog.com/catalogs/DefaultCatalog/views/tables/042297b0...1be45ecd462a/documentation?api-version=2016-03-30  
  
### Header  
Content-Type:   application/json; charset=utf-8    
x-ms-client-request-id:   059692ee-...-57490fcec42c    
Authorization:  Bearer eXJ0eyAiOiJKV1QiLCJhbGciOi...  
### Body schema  
  
    Body:  
        {  
            "fromSourceSystem": false,  
            "etag": "123456789",  
            "content": "<new documentation content>",  
            "mimetype": "text",  
        }  
<a name="response"/>  
## Response  
### Status codes  
|Code|Description  
|-|-  
|200|OK. An existing annotation was updated.  
|412|Precondition Failed. The request was cancelled because of the ETag mismatch in at least one item.  
  
### Content-Type  
application/json  
### Header  
x-ms-request-id: 3b8668da…1558d0f407c0  

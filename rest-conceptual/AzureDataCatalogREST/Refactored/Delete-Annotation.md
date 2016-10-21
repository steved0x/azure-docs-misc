---
title: "Delete Annotation"
ms.custom: na
ms.date: 2016-07-21
ms.prod: azure
ms.reviewer: na
ms.service: data-catalog
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: fd82293e-bf1a-4d07-9c37-7ef5498c05aa
caps.latest.revision: 19
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
# Delete Annotation
---  
[Request](#request) | [Response](#response)  
<a name="top"/>  
  
The **Delete Annotation** operation deletes an annotation and all nested annotations (if any).  
It supports optional If-Match header for optimistic concurrency control. Only weak format, such as W/"123456789", is supported.  
<a name="request"/>  
## Request  
DELETE https://api.azuredatacatalog.com/catalogs/{catalog_name}/views/{view_name}/{view_item_id}/{nested_view_name}/{nested_non_singleton_view_item_id}?api-version={api-version}  
DELETE https://api.azuredatacatalog.com/catalogs/{catalog_name}/views/{view_name}/{view_item_id}/{nested_view_name}?api-version={api-version}  
  
> [AZURE.NOTE] Some HTTP client implementations may automatically re-issue requests in response to a 302 from the server, but typically strip **Authorization headers** from the request. Since the Authorization header is required to make requests to ADC, you must ensure the Authorization header is still provided when re-issuing a request to a redirect location specified by ADC. Below is sample code demonstrating this using the .NET HttpWebRequest object.  
  
### Uri parameters  
|Name|Description|Data Type  
|-|-|-  
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String  
|view_name|Name of Data Asset View.|String  
|view_item_id|Id of a View item.|String  
|nested_view_name|Name of a nested View.|String  
|nested_non_singleton_view_item_id|Id of a nested non-singleton View item. Must be provided for a non-singleton View.|String  
|api-version|The API version.|String  
  
### DELETE example  
DELETE https://api.azuredatacatalog.com/catalogs/DefaultCatalog/views/tables/042297b0-c187-49cc-8f30-1be45ecd462a/experts/22c3fa019b3945dc97143ebc3ad74cbf-1111fa019b3945dc97143ebc3ad74cbf?api-version=2016-03-30  
### Header  
x-ms-client-request-id:   c8da5f08…67b203d77b2d  
Authorization:  Bearer eXJ0eyAiOiJKV1QiLCJhbGciOi...  
If-Match: W/"123456789"  
<a name="response"/>  
## Response  
### Status codes  
|Code|Description  
|-|-  
|204|NoContent  
|412|Precondition Failed. The request was cancelled because of the ETag mismatch.  
  
### Content-Type  
application/json  
### Header  
x-ms-request-id: 276b9dc4…e5f7017805c  
  

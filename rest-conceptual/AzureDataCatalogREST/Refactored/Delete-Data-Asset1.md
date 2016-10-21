---
title: "Delete Data Asset1"
ms.custom: na
ms.date: 2016-07-21
ms.prod: azure
ms.reviewer: na
ms.service: data-catalog
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
H1: Delete Data Asset
ms.assetid: 40772076-341d-4824-9cc1-fe7303b3672b
caps.latest.revision: 24
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
# Delete Data Asset1
---  
[Request](#request) | [Response](#response)  
<a name="top"/>  
  
The **Delete Data Asset** operation deletes a data asset and all annotations (if any) attached to it.  
It supports optional If-Match header for optimistic concurrency control. Only weak format, such as W/"123456789", is supported.  
<a name="request"/>  
## Request  
DELETE https://api.azuredatacatalog.com/catalogs/{catalog_name}/views/{view_name}/{view_item_id}?api-version={api-version}  
  
> [AZURE.NOTE] Some HTTP client implementations may automatically re-issue requests in response to a 302 from the server, but typically strip **Authorization headers** from the request. Since the Authorization header is required to make requests to ADC, you must ensure the Authorization header is still provided when re-issuing a request to a redirect location specified by ADC. Below is sample code demonstrating this using the .NET HttpWebRequest object.  
  
### Uri parameters  
|Name|Description|Data Type  
|-|-|-  
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String  
|view_name|Name of Data Asset View.|String  
|view_item_id|Id of a View item.|String  
|api-version|The API version.|String  
  
### DELETE example  
DELETE https://api.azuredatacatalog.com/catalogs/DefaultCatalog/views/tables/042297b0...1be45ecd462a?api-version=2016-03-30  
### Header  
x-ms-client-request-id: 59b68a46…46dc3ec8dcb8    
Authorization:  Bearer eXJ0eyAiOiJKV1QiLCJhbGciOi...    
If-Match: W/"123456789"  
<a name="response"/>  
## Response  
### Status codes  
|Code|Description  
|-|-  
|204|NoContent <br/> **NOTE**: Delete operation semantic is delete if exists, so if asset or annotation does not exist success status code 204 (NoContent) is returned.  
|412|Precondition Failed. The request was cancelled because of the ETag mismatch.  
  
### Content-Type  
application/json  
### Header  
x-ms-request-id: 664f86cf…5e512fa78e92  

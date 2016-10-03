---
title: "Delete a Single Glossary Term"
ms.custom: na
ms.date: 2016-07-21
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5cef446b-b15d-4753-88e4-fc2d033d59dd
caps.latest.revision: 4
author: spelluru
manager: jhubbard
---
# Delete a Single Glossary Term
---  
[Request](#request) | [Response](#response)  
<a name="top"/>  
  
The __Delete Glossary Term__ operation deletes a single glossary term.  
<a name="request"/>  
## Request  
DELETE https://api.azuredatacatalog.com/catalogs/{catalog_name}/glossaries/{glossary_name}/terms/{term_id}?api-version={api-version}  
  
[AZURE.NOTE] Some HTTP client implementations may automatically re-issue requests in response to a 302 from the server, but typically strip **Authorization headers** from the request. Since the Authorization header is required to make requests to ADC, you must ensure the Authorization header is still provided when re-issuing a request to a redirect location specified by ADC. Below is sample code demonstrating this using the .NET HttpWebRequest object.  
  
### Uri parameters  
|Name|Description|Data Type  
|---|---|---  
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String  
|glossary_name|Name of glossary, which is default to be the same as catalog_name. Use "DefaultGlossary" to choose the default glossary.|String  
|term_id|Id of a glossary term.|String  
|api-version|The API version.|String  
### DELETE example  
DELETE https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/DefaultCatalog/glossaries/DefaultGlossary/terms/e44b497d-7e58-4e31-9ac5-f9d9bd97e199?api-version=2016-03-30  
### Header  
x-ms-client-request-id: 8091955f…8f5b4c0acede Authorization: Bearer eXJ0eyAiOiJKV1QiLCJhbGciOi...  
<a name="response"/>  
## Response  
### Status codes  
|Code|Description  
|---|---  
|204|NoContent. Term doesn't exist or the deletion has been successful.  
|404|NotFound. Term is not found.  
|412|Precondition Failed. The request was cancelled because of the ETag mismatch.  
  
__NOTE__ Delete operation semantic is delete if exists, so if term does not exist success status code 204 (NoContent) will be returned.  
### Content-Type  
application/json  
### Header  
x-ms-request-id: 1095e88c…caffabd6dabd  

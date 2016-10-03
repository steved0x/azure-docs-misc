---
title: "Update a Single Glossary Term"
ms.custom: na
ms.date: 2016-07-21
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ebb8bda-a5dc-4a6e-a461-dc6fddc4f015
caps.latest.revision: 4
author: spelluru
manager: jhubbard
---
# Update a Single Glossary Term
---  
[Request](#request) | [Response](#response)  
<a name="top"/>  
  
The __Update Glossary Term__ operation updates a single glossary term.  
<a name="request"/>  
## Request  
PUT https://api.azuredatacatalog.com/catalogs/{catalog_name}/glossaries/{glossary_name}/terms/{term_id}?api-version={api-version}  
  
[AZURE.NOTE] Some HTTP client implementations may automatically re-issue requests in response to a 302 from the server, but typically strip **Authorization headers** from the request. Since the Authorization header is required to make requests to ADC, you must ensure the Authorization header is still provided when re-issuing a request to a redirect location specified by ADC. Below is sample code demonstrating this using the .NET HttpWebRequest object.  
  
### Uri parameters  
|Name|Description|Data Type  
|---|---|---  
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String  
|glossary_name|Name of glossary, which is default to be the same as catalog_name. Use "DefaultGlossary" to choose the default glossary.|String  
|term_id|Id of a glossary term.|String  
|api-version|The API version.|String  
### PUT example  
PUT https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/DefaultCatalog/glossaries/DefaultGlossary/terms/b04e39a9-b457-4ab3-9da9-58b42be29577?api-version=2016-03-30  
### Header  
Content-Type: application/json x-ms-client-request-id: 13c45c14…46ab469473f0 Authorization: Bearer eyJ0eX ... FWSXfwtQ  
<a name="response"/>  
### Body example  
```  
{  
  "parentId" : "https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/glossaries/MyCatalog/terms/e44b497d-7e58-4e31-9ac5-f9d9bd97e199"  
  "name" : "Child",  
  "definition" : "termDefinition",  
  "stakeholders" : [  
    {  
      "objectId" : "bedc9058-980c-43a5-8b3b-1e7ce98b8cef",  
      "upn" : "test@example.com"  
    }  
  ]  
}  
```  
## Response  
### Status codes  
|Code|Description  
|---|---  
|200|Ok. An existing term was updated.  
|404|NotFound. Term was not found.  
|409|Conflict. Duplicate term name already exists under the same parent term.  
|412|Precondition Failed. The request was cancelled because of the ETag mismatch.  
  
### Content-Type  
application/json  
### Header  
x-ms-request-id: 1095e88c…caffabd6dabd  
Location:  https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/glossaries/MyCatalog/terms/b04e39a9-b457-4ab3-9da9-58b42be29577  

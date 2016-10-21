---
title: "Get a Single Glossary Term"
ms.custom: na
ms.date: 2016-07-21
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c15241e-8064-4450-862a-b571ccec8491
caps.latest.revision: 4
author: spelluru
manager: jhubbard
---
# Get a Single Glossary Term
---  
[Request](#request) | [Response](#response)  
<a name="top"/>  
  
The __Get Glossary Term__ operation gets a single glossary term.  
<a name="request"/>  
## Request  
GET https://api.azuredatacatalog.com/catalogs/{catalog_name}/glossaries/{glossary_name}/terms/{term_id}?api-version={api-version}  
  
[AZURE.NOTE] Some HTTP client implementations may automatically re-issue requests in response to a 302 from the server, but typically strip **Authorization headers** from the request. Since the Authorization header is required to make requests to ADC, you must ensure the Authorization header is still provided when re-issuing a request to a redirect location specified by ADC. Below is sample code demonstrating this using the .NET HttpWebRequest object.  
  
### Uri parameters  
|Name|Description|Data Type  
|---|---|---  
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String  
|glossary_name|Name of glossary, which is default to be the same as catalog_name. Use "DefaultGlossary" to choose the default glossary.|String  
|term_id|Id of a glossary term.|String  
|api-version|The API version.|String  
### GET example  
GET https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/DefaultCatalog/glossaries/DefaultGlossary/terms/e44b497d-7e58-4e31-9ac5-f9d9bd97e199?api-version=2016-03-30  
### Header  
x-ms-client-request-id: 8091955f…8f5b4c0acede Authorization: Bearer eXJ0eyAiOiJKV1QiLCJhbGciOi...  
<a name="response"/>  
## Response  
### Status codes  
|Code|Description  
|---|---  
|200|OK. The response contains requested glossary term.  
|404|NotFound. Term was not found.  
### Content-Type  
application/json  
### Header  
x-ms-request-id: 1095e88c…caffabd6dabd  
Content-Type: application/json; charset=utf-8  
### Body  
```  
{  
  "id": "https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/glossaries/MyCatalog/terms/e44b497d-7e58-4e31-9ac5-f9d9bd97e199",  
  "name": "root1",  
  "definition": "termDefinition",  
  "description" : "some description",  
  "stakeholders": [  
    {  
      "objectId": "bedc9058-980c-43a5-8b3b-1e7ce98b8cef",  
      "upn": "holder@example.com"  
    }  
  ],  
  "createdBy": {  
    "objectId": "03dee373-5753-49c4-88f7-68041d39cc24",  
    "upn": "admin@billtest255158live.ccsctp.net"  
  },  
  "createdTime": "2016-03-03T17:15:25.6453233-08:00",  
  "modifiedBy": {  
    "objectId": "03dee373-5753-49c4-88f7-68041d39cc24",  
    "upn": "admin@billtest255158live.ccsctp.net"  
  },  
  "modifiedTime": "2016-03-03T17:15:25.6453233-08:00"  
}  
```  

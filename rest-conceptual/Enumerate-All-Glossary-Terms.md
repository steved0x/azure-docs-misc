---
title: "Enumerate All Glossary Terms"
ms.custom: na
ms.date: 2016-07-21
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9040f773-c93b-4edc-b816-0a47abeda1f4
caps.latest.revision: 4
author: spelluru
manager: jhubbard
---
# Enumerate All Glossary Terms
---  
[Request](#request) | [Response](#response)  
<a name="top"/>  
  
The __Enumerate Glossary Terms__ operation enumerate all terms in a glossary.  
<a name="request"/>  
## Request  
GET https://api.azuredatacatalog.com/catalogs/{catalog_name}/glossaries/{glossary_name}/terms?api-version={api-version}  
  
[AZURE.NOTE] Some HTTP client implementations may automatically re-issue requests in response to a 302 from the server, but typically strip **Authorization headers** from the request. Since the Authorization header is required to make requests to ADC, you must ensure the Authorization header is still provided when re-issuing a request to a redirect location specified by ADC. Below is sample code demonstrating this using the .NET HttpWebRequest object.  
  
### Uri parameters  
|Name|Description|Data Type  
|---|---|---  
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String  
|glossary_name|Name of glossary, which is default to be the same as catalog_name. Use "DefaultGlossary" to choose the default glossary.|String  
|api-version|The API version.|String  
### GET example  
GET https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/DefaultCatalog/glossaries/DefaultGlossary/terms?api-version=2016-03-30  
### Header  
x-ms-client-request-id: 8091955f…8f5b4c0acede Authorization: Bearer eXJ0eyAiOiJKV1QiLCJhbGciOi...  
<a name="response"/>  
## Response  
### Status codes  
|Code|Description  
|---|---  
|200|OK. The response contains list of glossary terms.  
### Content-Type  
application/json  
### Header  
x-ms-request-id: 1095e88c…caffabd6dabd  
Content-Type: application/json; charset=utf-8  
### Body  
__Note__ each enumeration operation returns at most 1000 terms. If there are more than 1000 terms in the glossary, a "nextLink" will be included in the response for continuous enumeration.  
```  
{  
  "value": [  
    {  
      "parentId": "https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/glossaries/MyCatalog/terms/e44b497d-7e58-4e31-9ac5-f9d9bd97e199",  
      "id": "https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/glossaries/MyCatalog/terms/0cb37c31-6743-4d9d-bb4a-35716984fc57",  
      "name": "child2",  
      "definition": "termDefinition",  
      "stakeholders": [  
        {  
          "objectId": "bedc9058-980c-43a5-8b3b-1e7ce98b8cef",  
          "upn": "test@sample.com"  
        }  
      ],  
      "createdBy": {  
        "objectId": "03dee373-5753-49c4-88f7-68041d39cc24",  
        "upn": "admin@billtest255158live.ccsctp.net"  
      },  
      "createdTime": "2016-03-03T17:18:09.6089982-08:00",  
      "modifiedBy": {  
        "objectId": "03dee373-5753-49c4-88f7-68041d39cc24",  
        "upn": "admin@billtest255158live.ccsctp.net"  
      },  
      "modifiedTime": "2016-03-03T17:18:09.6089982-08:00"  
    },  
    {  
      "parentId": "https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/glossaries/MyCatalog/terms/e44b497d-7e58-4e31-9ac5-f9d9bd97e199",  
      "id": "https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/glossaries/MyCatalog/terms/60d51213-84cb-42ec-a331-98e283612c6a",  
      "name": "child1",  
      "definition": "termDefinition",  
      "stakeholders": [  
        {  
          "objectId": "bedc9058-980c-43a5-8b3b-1e7ce98b8cef",  
          "upn": "test@sample.com"  
        }  
      ],  
      "createdBy": {  
        "objectId": "03dee373-5753-49c4-88f7-68041d39cc24",  
        "upn": "admin@billtest255158live.ccsctp.net"  
      },  
      "createdTime": "2016-03-03T17:18:00.3793795-08:00",  
      "modifiedBy": {  
        "objectId": "03dee373-5753-49c4-88f7-68041d39cc24",  
        "upn": "admin@billtest255158live.ccsctp.net"  
      },  
      "modifiedTime": "2016-03-03T17:18:00.3793795-08:00"  
    },  
    {  
      "id": "https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/glossaries/MyCatalog/terms/19ce15d9-b25e-4f80-8dee-cfa9bdb57f1c",  
      "name": "root2",  
      "definition": "termDefinition",  
      "stakeholders": [  
        {  
          "objectId": "bedc9058-980c-43a5-8b3b-1e7ce98b8cef",  
          "upn": "test@sample.com"  
        }  
      ],  
      "createdBy": {  
        "objectId": "03dee373-5753-49c4-88f7-68041d39cc24",  
        "upn": "admin@billtest255158live.ccsctp.net"  
      },  
      "createdTime": "2016-03-03T17:17:00.5490763-08:00",  
      "modifiedBy": {  
        "objectId": "03dee373-5753-49c4-88f7-68041d39cc24",  
        "upn": "admin@billtest255158live.ccsctp.net"  
      },  
      "modifiedTime": "2016-03-03T17:17:00.5490763-08:00"  
    },  
    {  
      "id": "https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/glossaries/MyCatalog/terms/e44b497d-7e58-4e31-9ac5-f9d9bd97e199",  
      "name": "root1",  
      "definition": "termDefinition",  
      "stakeholders": [  
        {  
          "objectId": "bedc9058-980c-43a5-8b3b-1e7ce98b8cef",  
          "upn": "test@sample.com"  
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
  ]  
}  
```  

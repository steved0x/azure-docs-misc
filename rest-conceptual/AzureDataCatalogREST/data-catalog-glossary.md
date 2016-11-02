# Glossary

## Create
Creates a single glossary term.
  

### Request  
	POST https://api.azuredatacatalog.com/catalogs/{catalog_name}/glossaries/{glossary_name}/terms?api-version={api-version}  
  
>[AZURE.NOTE] Some HTTP client implementations may automatically re-issue requests in response to a 302 from the server, but typically strip **Authorization headers** from the request. Since the Authorization header is required to make requests to ADC, you must ensure the Authorization header is still provided when re-issuing a request to a redirect location specified by ADC. Below is sample code demonstrating this using the .NET HttpWebRequest object.  
  
#### Uri parameters  
|Name|Description|Data Type  
|---|---|---  
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String  
|glossary_name|Name of glossary, which is default to be the same as catalog_name. Use "DefaultGlossary" to choose the default glossary.|String  
|api-version|The API version.|String  
#### POST example  
POST https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/DefaultCatalog/glossaries/DefaultGlossary/terms?api-version=2016-03-30  
#### Header  
Content-Type: application/json x-ms-client-request-id: 13c45c14…46ab469473f0 Authorization: Bearer eyJ0eX ... FWSXfwtQ  
<a name="response"/>  
#### Body example  
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
__Note__:  
1. If body does not include "parentId", the term created will be a root term and not have a parent.  
2. Two terms are not allowed to have the same name if they have the same parent term.  
  
### Response  
#### Status codes  
|Code|Description  
|---|---  
|201|Created. The request was fulfilled and a new term was created.  
|409|Conflict. Duplicate term name already exists under the same parent term.  
  
#### Content-Type  
application/json  
#### Header  
x-ms-request-id: 1095e88c…caffabd6dabd  
Location:  https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/glossaries/MyCatalog/terms/b04e39a9-b457-4ab3-9da9-58b42be29577  



## Delete
Deletes a single glossary term.  

 
### Request  
	DELETE https://api.azuredatacatalog.com/catalogs/{catalog_name}/glossaries/{glossary_name}/terms/{term_id}?api-version={api-version}  
  
>[AZURE.NOTE] Some HTTP client implementations may automatically re-issue requests in response to a 302 from the server, but typically strip **Authorization headers** from the request. Since the Authorization header is required to make requests to ADC, you must ensure the Authorization header is still provided when re-issuing a request to a redirect location specified by ADC. Below is sample code demonstrating this using the .NET HttpWebRequest object.  
  
#### Uri parameters  
|Name|Description|Data Type  
|---|---|---  
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String  
|glossary_name|Name of glossary, which is default to be the same as catalog_name. Use "DefaultGlossary" to choose the default glossary.|String  
|term_id|Id of a glossary term.|String  
|api-version|The API version.|String  
#### DELETE example  
DELETE https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/DefaultCatalog/glossaries/DefaultGlossary/terms/e44b497d-7e58-4e31-9ac5-f9d9bd97e199?api-version=2016-03-30  
#### Header  
x-ms-client-request-id: 8091955f…8f5b4c0acede Authorization: Bearer eXJ0eyAiOiJKV1QiLCJhbGciOi...  

 
### Response  
#### Status codes  
|Code|Description  
|---|---  
|204|NoContent. Term doesn't exist or the deletion has been successful.  
|404|NotFound. Term is not found.  
|412|Precondition Failed. The request was cancelled because of the ETag mismatch.  
  
__NOTE__ Delete operation semantic is delete if exists, so if term does not exist success status code 204 (NoContent) will be returned.  
#### Content-Type  
application/json  
#### Header  
x-ms-request-id: 1095e88c…caffabd6dabd  


## Enumerate
Enumerate all terms in a glossary. 
 

### Request  
	GET https://api.azuredatacatalog.com/catalogs/{catalog_name}/glossaries/{glossary_name}/terms?api-version={api-version}  
  
>[AZURE.NOTE] Some HTTP client implementations may automatically re-issue requests in response to a 302 from the server, but typically strip **Authorization headers** from the request. Since the Authorization header is required to make requests to ADC, you must ensure the Authorization header is still provided when re-issuing a request to a redirect location specified by ADC. Below is sample code demonstrating this using the .NET HttpWebRequest object.  
  
#### Uri parameters  
|Name|Description|Data Type  
|---|---|---  
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String  
|glossary_name|Name of glossary, which is default to be the same as catalog_name. Use "DefaultGlossary" to choose the default glossary.|String  
|api-version|The API version.|String  
#### GET example  
GET https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/DefaultCatalog/glossaries/DefaultGlossary/terms?api-version=2016-03-30  
#### Header  
x-ms-client-request-id: 8091955f…8f5b4c0acede Authorization: Bearer eXJ0eyAiOiJKV1QiLCJhbGciOi...  
  
### Response  
#### Status codes  
|Code|Description  
|---|---  
|200|OK. The response contains list of glossary terms.  
#### Content-Type  
application/json  
#### Header  
x-ms-request-id: 1095e88c…caffabd6dabd  
Content-Type: application/json; charset=utf-8  
#### Body  
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

## Get
Gets a single glossary term.  

 
### Request  
	GET https://api.azuredatacatalog.com/catalogs/{catalog_name}/glossaries/{glossary_name}/terms/{term_id}?api-version={api-version}  
  
[AZURE.NOTE] Some HTTP client implementations may automatically re-issue requests in response to a 302 from the server, but typically strip **Authorization headers** from the request. Since the Authorization header is required to make requests to ADC, you must ensure the Authorization header is still provided when re-issuing a request to a redirect location specified by ADC. Below is sample code demonstrating this using the .NET HttpWebRequest object.  
  
#### Uri parameters  
|Name|Description|Data Type  
|---|---|---  
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String  
|glossary_name|Name of glossary, which is default to be the same as catalog_name. Use "DefaultGlossary" to choose the default glossary.|String  
|term_id|Id of a glossary term.|String  
|api-version|The API version.|String  
#### GET example  

	GET https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/DefaultCatalog/glossaries/DefaultGlossary/terms/e44b497d-7e58-4e31-9ac5-f9d9bd97e199?api-version=2016-03-30  

### Header  
x-ms-client-request-id: 8091955f…8f5b4c0acede Authorization: Bearer eXJ0eyAiOiJKV1QiLCJhbGciOi...  

 
### Response  
#### Status codes  
|Code|Description  
|---|---  
|200|OK. The response contains requested glossary term.  
|404|NotFound. Term was not found.  
#### Content-Type  
application/json  
#### Header  
x-ms-request-id: 1095e88c…caffabd6dabd  
Content-Type: application/json; charset=utf-8  
#### Body  
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

## Update
Updates a single glossary term.
  
 
### Request  
PUT https://api.azuredatacatalog.com/catalogs/{catalog_name}/glossaries/{glossary_name}/terms/{term_id}?api-version={api-version}  
  
[AZURE.NOTE] Some HTTP client implementations may automatically re-issue requests in response to a 302 from the server, but typically strip **Authorization headers** from the request. Since the Authorization header is required to make requests to ADC, you must ensure the Authorization header is still provided when re-issuing a request to a redirect location specified by ADC. Below is sample code demonstrating this using the .NET HttpWebRequest object.  
  
#### Uri parameters  
|Name|Description|Data Type  
|---|---|---  
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String  
|glossary_name|Name of glossary, which is default to be the same as catalog_name. Use "DefaultGlossary" to choose the default glossary.|String  
|term_id|Id of a glossary term.|String  
|api-version|The API version.|String  
#### PUT example  
PUT https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/DefaultCatalog/glossaries/DefaultGlossary/terms/b04e39a9-b457-4ab3-9da9-58b42be29577?api-version=2016-03-30  
### Header  
Content-Type: application/json x-ms-client-request-id: 13c45c14…46ab469473f0 Authorization: Bearer eyJ0eX ... FWSXfwtQ  
<a name="response"/>  
#### Body example  
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
### Response  
#### Status codes  
|Code|Description  
|---|---  
|200|Ok. An existing term was updated.  
|404|NotFound. Term was not found.  
|409|Conflict. Duplicate term name already exists under the same parent term.  
|412|Precondition Failed. The request was cancelled because of the ETag mismatch.  
  
#### Content-Type  
application/json  
#### Header  
x-ms-request-id: 1095e88c…caffabd6dabd  
Location:  https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/glossaries/MyCatalog/terms/b04e39a9-b457-4ab3-9da9-58b42be29577  

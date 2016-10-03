---
title: "Enumerate Custom Data Source Protocols"
ms.custom: na
ms.date: 2016-07-21
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4f1e78cb-fb8c-4002-a63f-5017e5ebeb97
caps.latest.revision: 5
author: spelluru
manager: jhubbard
---
# Enumerate Custom Data Source Protocols
---  
[Request](#request) | [Response](#response)   
<a name="top"/>  
  
The **Enumerate Custom data Source Protocols** operation enumerates custom data source protocols which are registered with the catalog.  
<a name="request"/>  
## Request  
GET https://api.azuredatacatalog.com/catalogs/{catalog_name}/dataSourceProtocols?api-version={api-version}  
  
### Uri parameters  
|Name|Description|Data Type  
|---|---|---  
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String  
|api-version|The API version.|String  
  
### GET example  
GET https://api.azuredatacatalog.com/catalogs/DefaultCatalog/dataSourceProtocols?api-version=2016-03-30  
  
### Header  
Content-Type: application/json    
x-ms-client-request-id: 13c45c14…46ab469473f0    
Authorization: Bearer eyJ0eX ... FWSXfwtQ  
  
<a name="response"/>  
## Response  
### Status codes  
|Code|Description  
|---|---  
|200|OK. The response contains list of custom data source protocols.  
  
  
### Content-Type  
application/json  
  
### Header  
HTTP/1.1 201 Created  
x-ms-request-id: 72cf83c0…058f2b2a0c68  
  
### Body  
    {  
        "value": [  
            {  
                "namespace": "Test.Test.MyTestProtocols",  
                "name": "abc-def",  
                "identityProperties": [  
                    {  
                        "name": "prop1",  
                        "type": "string",  
                        "ignoreCase": true  
                    },  
                    {  
                        "name": "prop2",  
                        "type": "int"  
                    }  
                ],  
                "identitySets": [  
                    {  
                        "properties": [  
                            "prop1"  
                        ]  
                    },  
                    {  
                        "properties": [  
                            "prop1",  
                            "prop2"  
                        ]  
                    }  
                ],  
                "id": "https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/dataSourceProtocols/753a4d5a-26af-6491-610c-c3e069b904b1",  
                "timestamp": "2016-04-27T00:45:55.8094373"  
            }  
        ]  
    }  
  
If Response body contains non-null value for the "nextLink" property, client should use the url specified in the "nextLink" property to continue enumeration until value of the "nextLink" property is null (or not present in the response body).  

---
title: "Get Data Asset with Annotations2"
ms.custom: na
ms.date: 2016-07-21
ms.prod: azure
ms.reviewer: na
ms.service: data-catalog
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
H1: Get Data Asset with Annotations
ms.assetid: 38d30874-032d-4953-9852-ab527c9d7bff
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
# Get Data Asset with Annotations2
---  
[Request](#request) | [Response](#response)  
<a name="top"/>  
  
The **Get Data Asset with Annotations** operation gets a data asset with annotations.  
It supports optional Accept header parameter adc.metadata that requests ETags to be included in the response for all the items. Use values minimal or full to get ETags in response. The valid values are none, minimal and full.  
<a name="request"/>  
## Request  
GET https://api.azuredatacatalog.com/catalogs/{catalog_name}/views/{view_name}/{view_item_id}?api-version={api-version}  
  
> [AZURE.NOTE] Some HTTP client implementations may automatically re-issue requests in response to a 302 from the server, but typically strip **Authorization headers** from the request. Since the Authorization header is required to make requests to ADC, you must ensure the Authorization header is still provided when re-issuing a request to a redirect location specified by ADC. Below is sample code demonstrating this using the .NET HttpWebRequest object.  
  
### Uri parameters  
|Name|Description|Data Type  
|-|-|-  
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String  
|view_name|Name of Data Asset View.|String  
|view_item_id|Id of a View item.|String  
|api-version|The API version.|String  
  
### GET example  
GET https://api.azuredatacatalog.com/catalogs/DefaultCatalog/views/tables/042297b...1be45ecd462a?api-version=2016-03-30  
### Header  
x-ms-client-request-id: 8091955f…8f5b4c0acede    
Authorization:  Bearer eXJ0eyAiOiJKV1QiLCJhbGciOi...    
Accept: application/json;adc.metadata=full  
<a name="response"/>  
## Response  
  
### Status codes  
|Code|Description  
|-|-  
|200|OK. The response contains requested asset view.  
  
### Content-Type  
application/json  
### Header  
x-ms-request-id: 1095e88c…caffabd6dabd  
Content-Type:   application/json; charset=utf-8  
### Body  
    {  
        "id": "https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/views/tables/042297b0-...-1be45ecd462a",  
        "etag": "1234567891",  
        "timestamp": "2015-05-15T03:48:39.2425547",  
        "roles": [  
            {  
                "role": "Contributor",  
                "members": [  
                    {  
                        "objectId": "00000000-0000-0000-0000-000000000201"  
                    }  
                ]  
            }  
        ],  
        "effectiveRights": [  
            "Read",  
            "Delete",  
            "ChangeOwnership",  
            "ChangeVisibility",  
            "ViewPermissions",  
            "ViewRoles",  
            "Update",  
            "TakeOwnership"  
        ],  
        "properties": {  
            "fromSourceSystem": true,  
        "name": "Orders",  
        "dataSource": {  
            "sourceType": "SQL Server",  
                "objectType": "Table"  
        },  
        "dsl": {  
            "protocol": "tds",  
            "authentication": "windows",  
            "address": {  
                "server": "MyServer.contoso.com",  
                "database": "NORTHWND",  
                "schema": "dbo",  
                "object": "Orders"  
            }  
        },  
        "lastRegisteredBy": {  
            "upn": "user1@contoso.com",  
            "firstName": "User1FirstName",  
            "lastName": "User1LastName"  
        },  
            "containerId": "containers/3b2c00be-...-1f15367f54e4"  
        },  
        "annotations": {  
            "schema": {  
                "id": "https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/views/tables/042297b0-...-1be45ecd462a/schema",  
                "etag": "1234567892",  
                "timestamp": "2015-05-15T03:48:39.2425547",  
                "roles": [  
                    {  
                        "role": "Contributor",  
                        "members": [  
            {  
                                "objectId": "00000000-0000-0000-0000-000000000201"  
                            }  
                        ]  
                    }  
                ],  
                "effectiveRights": [  
                        "Read",  
                        "Delete",  
                        "ViewRoles",  
                        "Update"  
                    ],  
                "properties": {  
                    "fromSourceSystem": true,  
                "columns": [  
                    {  
                        "name": "OrderID",  
                        "isNullable": false,  
                        "type": "int",  
                        "maxLength": 4,  
                        "precision": 10  
                    },  
                    {  
                        "name": "CustomerID",  
                        "isNullable": true,  
                        "type": "nchar",  
                        "maxLength": 10,  
                        "precision": 0  
                    },  
                    {  
                        "name": "EmployeeID",  
                        "isNullable": true,  
                        "type": "int",  
                        "maxLength": 4,  
                        "precision": 10  
                    },  
                    {  
                        "name": "OrderDate",  
                        "isNullable": true,  
                        "type": "datetime",  
                        "maxLength": 8,  
                        "precision": 23  
                    }  
                    ]  
            }  
            },  
        "experts": [  
            {  
                    "id": "https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/views/tables/042297b0-...-1be45ecd462a/experts/22c3fa019b3945dc97143ebc3ad74cbf-1111fa019b3945dc97143ebc3ad74cbf",  
                    "etag": "1234567893",  
                    "timestamp": "2015-05-15T03:48:39.2425547",  
                    "roles": [  
                        {  
                            "role": "Contributor",  
                            "members": [  
                                {  
                                    "objectId": "22c3fa01-9b39-45dc-9714-3ebc3ad74cbf"  
                                }  
                            ]  
                        }  
                    ],  
                    "effectiveRights": [  
                        "Read",  
                        "Delete",  
                        "ViewRoles",  
                        "Update"  
                    ],  
                    "properties": {  
                        "fromSourceSystem": false,  
                        "key": "22c3fa019b3945dc97143ebc3ad74cbf-1111fa019b3945dc97143ebc3ad74cbf",  
                        "expert": {  
                            "upn": "expert1@contoso.com",  
                            "objectId": "1111fa019b3945dc97143ebc3ad74cbf"  
                        }  
                    }  
            }  
        ]  
    }  
    }  

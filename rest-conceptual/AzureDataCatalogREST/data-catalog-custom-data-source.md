# Custom Data Source

## Enumerate
Enumerates custom data source protocols which are registered with the catalog.  

 
### Request  
	GET https://api.azuredatacatalog.com/catalogs/{catalog_name}/dataSourceProtocols?api-version={api-version}  
  
#### Uri parameters  
|Name|Description|Data Type  
|---|---|---  
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String  
|api-version|The API version.|String  
  
#### GET example  
	GET https://api.azuredatacatalog.com/catalogs/DefaultCatalog/dataSourceProtocols?api-version=2016-03-30  
  
#### Header  
Content-Type: application/json    
x-ms-client-request-id: 13c45c14…46ab469473f0    
Authorization: Bearer eyJ0eX ... FWSXfwtQ  
  


### Response  
#### Status codes  
|Code|Description  
|---|---  
|200|OK. The response contains list of custom data source protocols.  
  
  
#### Content-Type  
application/json  
  
#### Header  
HTTP/1.1 201 Created  
x-ms-request-id: 72cf83c0…058f2b2a0c68  
  
#### Body  
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


## Register
Registers a new data source protocol that can be referenced in the "dsl" property when publishing an asset.  


### Request  
	POST https://api.azuredatacatalog.com/catalogs/{catalog_name}/dataSourceProtocols?api-version={api-version}  
  
#### Uri parameters  
|Name|Description|Data Type  
|---|---|---  
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String  
|api-version|The API version.|String  
  
#### POST example  
	POST https://api.azuredatacatalog.com/catalogs/DefaultCatalog/dataSourceProtocols?api-version=2016-03-30  
  
#### Header  
Content-Type: application/json    
x-ms-client-request-id: 12345c14…46ab469473f0    
Authorization: Bearer eyJ0eX ... FWSXfwtQ  
  
#### Body example  
    {  
        "namespace": "Test.MyTestProtocols",  
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
        ]  
    }  
  

 
##### Response  
### Status codes  
|Code|Description  
|---|---  
|200|Ok. The request was fulfilled and a new custom data source protocol was created.  
|400|BadRequest. The request was cancelled because request payload does not conform to the data source protocol specification. Refer to the response's body for error details.  
|400|BadRequest with the error code ImmutableViewItem. The request was cancelled because the data source protocol with the specified namespace and name already exists and cannot be updated.  
  
### Content-Type  
application/json  
  
#### Header  
HTTP/1.1 201 Created  
x-ms-request-id: 72cf83c0…058f2b2a0c68  
Location: https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/dataSourceProtocols/753a4d5a-26af-6491-610c-c3e069b904b1  
  
### How to use custom data source protocol when publishing an asset  
Use namespace-qualified name of the custom data source protocol as the value of the "protocol" property in the asset's "dsl" property and provide values for identity properties in "address" property bag:  
  
	POST https://api.azuredatacatalog.com/catalogs/DefaultCatalog/views/tables?api-version=2016-03-30  
Body:  
  
use identity set which contains only "prop1":  
  
    {  
        "properties": {  
            ....  
            "dsl": {  
                "protocol": "Test.MyTestProtocols.abc-def",  
                "authentication": "windows",  
                "address": {  
                    "prop1": "location1"  
                }  
            },  
            ...  
        },  
        "annotations": {  
            ...  
        }  
    }  
  
or use identity set which contains both "prop1" and "prop2":  
  
    {  
        "properties": {  
            ....  
            "dsl": {  
                "protocol": "Test.MyTestProtocols.abc-def",  
                "authentication": "windows",  
                "address": {  
                    "prop1": "location1",  
                    "prop2": 123,  
                }  
            },  
            ...  
        },  
        "annotations": {  
            ...  
        }  
    }  
  
> [AZURE.NOTE]  If "address" property bag contains only "prop2", the publish request will be rejected (as BadRequest) because there is no matching identity set defined by the protocol.  
  
Please refer <a href="https://azure.microsoft.com/en-us/documentation/articles/data-catalog-developer-concepts/">here</a> for the custom data source protocol specification.  

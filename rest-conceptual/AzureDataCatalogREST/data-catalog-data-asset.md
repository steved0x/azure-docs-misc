# Data Asset

## Annotate
Aannotates an asset.

`etag` property is optional and is used for concurrency control.


	POST https://api.azuredatacatalog.com/catalogs/{catalog_name}/views/{view_name}/{view_item_id}/{nested_view_name}?api-version={api-version}


> [AZURE.NOTE] Some HTTP client implementations may automatically re-issue requests in response to a 302 from the server, but typically strip **Authorization headers** from the request. Since the Authorization header is required to make requests to ADC, you must ensure the Authorization header is still provided when re-issuing a request to a redirect location specified by ADC. Below is sample code demonstrating this using the .NET HttpWebRequest object.

### Uri parameters

|Name|Description|Data Type
|-|-|-
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String
|view_name|Name of Data Asset View.|String
|view_item_id|Id of a View item.|String
|nested_view_name|Name of a nested View item.|String
|api-version|The API version.|String

### Example: Add Experts
POST https://api.azuredatacatalog.com/catalogs/DefaultCatalog/views/tables/042297b0...1be45ecd462a/experts?api-version=2016-03-30
#### Header
Content-Type: application/json
x-ms-client-request-id:   13d9f885…a92d-8a9f8cf9f707
Authorization: Bearer eyJ0eX ... FWSXfwtQ
#### Body

    {
        "etag": "59085E253E2244A59F664A2F447E675E",
        "properties":
        {
            "fromSourceSystem": false,
            "key": "22c3fa019b3945dc97143ebc3ad74cbf--1111fa019b3945dc97143ebc3ad74cbf",
            "expert":
            {
                "upn": "expert1@contoso.com",
                "objectId": "1111fa019b3945dc97143ebc3ad74cbf"
            },
        }
    }

### Example: Add Glossary Term Tags
POST https://api.azuredatacatalog.com/catalogs/DefaultCatalog/views/tables/042297b0...1be45ecd462a/termTags?api-version=2016-03-30
#### Header
Content-Type: application/json
x-ms-client-request-id:   13d9f885…a92d-8a9f8cf9f707
Authorization: Bearer eyJ0eX ... FWSXfwtQ
#### Body

    {
        "etag": "59085E253E2244A59F664A2F447E675E",
        "properties":
        {
            "fromSourceSystem": false,
            "key": "22c3fa019b3945dc97143ebc3ad74cbf--1111fa019b3945dc97143ebc3ad74cbf",
            "termId": "https://test.catalog.com/catalogs/DefaultCatalog/glossaries/DefaultGlossary/terms/ed975c9d-2fb2-49a3-b6f2-222389cefd7e",
        }
    }

### Example: Add Glossary Column Term Tags
POST https://api.azuredatacatalog.com/catalogs/DefaultCatalog/views/tables/042297b0...1be45ecd462a/columnTermTags?api-version=2016-03-30
#### Header
Content-Type: application/json
x-ms-client-request-id:   13d9f885…a92d-8a9f8cf9f707
Authorization: Bearer eyJ0eX ... FWSXfwtQ
#### Body

    {
        "etag": "59085E253E2244A59F664A2F447E675E",
        "properties":
        {
            "fromSourceSystem": false,
            "key": "22c3fa019b3945dc97143ebc3ad74cbf--1111fa019b3945dc97143ebc3ad74cbf",
            "columnName": "Col1",
            "termId": "https://test.catalog.com/catalogs/DefaultCatalog/glossaries/DefaultGlossary/terms/ed975c9d-2fb2-49a3-b6f2-222389cefd7e",
        }
    }


### Response
#### Status codes
|Code|Description
|-|-
|201|Created. The request was fulfilled and a new annotation was created.
|200|OK. An existing annotation was updated.
|412|Precondition Failed. The request was cancelled because of the ETag mismatch in at least one item.

#### Content-Type
application/json
#### Header
HTTP/1.1 201 Created
x-ms-request-id: 72cf83c0…058f2b2a0c68
Location: https://api.azuredatacatalog.com/catalogs/DefaultCatalog/views/tables/042297b0...1be45ecd462a/experts/22c3fa019b3945dc97143ebc3ad74cbf-1111fa019b3945dc97143ebc3ad74cbf


## Register or Update
Registers a new data asset or updates an existing one if an asset with the same identity already exists. The items can optionally contain ETag values to enable optimistic concurrency control for them.  


[Get started sample on GitHub](https://github.com/Azure-Samples/data-catalog-dotnet-get-started)  

### Request  
	POST https://api.azuredatacatalog.com/catalogs/{catalog_name}/views/{view_name}?api-version={api-version}  

> [AZURE.NOTE] Some HTTP client implementations may automatically re-issue requests in response to a 302 from the server, but typically strip Authorization headers from the request. Since the Authorization header is required to make requests to ADC, you must ensure the Authorization header is still provided when re-issuing a request to a redirect location specified by ADC. Below is sample code demonstrating this using the .NET HttpWebRequest object.  

### Uri parameters  
|Name|Description|Data Type  
|---|---|---  
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String  
|view_name|Name of Data Asset View.|String  
|api-version|The API version.|String  
  
### POST example  
POST https://api.azuredatacatalog.com/catalogs/DefaultCatalog/views/tables?api-version=2016-03-30  
  
### Header  
Content-Type: application/json    
x-ms-client-request-id: 13c45c14…46ab469473f0    
Authorization: Bearer eyJ0eX ... FWSXfwtQ  
  
### Body example  
    {  
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
            }  
        }  
    }  
  
 
### Response  
#### Status codes  
|Code|Description  
|---|---  
|200|OK. An existing asset was updated.  
|201|Created. The request was fulfilled and a new asset was created.  
|412|Precondition Failed. The request was cancelled because of the ETag mismatch in at least one item.  
  
#### Content-Type  
application/json  
  
#### Header  
HTTP/1.1 201 Created  
x-ms-request-id: 72cf83c0…058f2b2a0c68  
Location: https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/views/tables/042297b0…1be45ecd462a  
  
### Supported Data Sources  
  
Please refer [Azure Data Catalog supported data sources](https://azure.microsoft.com/en-us/documentation/articles/data-catalog-dsr/) for the list of currently supported data sources objects.  
  
  
### Example  
This example shows you how to get an Azure AD access token, and perform a **Register** operation.  
  
**Note** This example uses the **DefaultCatalog** keyword to update the user's default catalog. You may alternately specify the actual catalog name. To find the **Catalog** name, sign into **Azure Data Catalog**, and choose **User**. You will see the **Catalog** name.  
  
        using System;  
        using System.Net;  
        using Microsoft.IdentityModel.Clients.ActiveDirectory;  
        using System.IO;  
  
        ...  
  
        //To learn how to register a client app and get a Client ID,  
        // see https://msdn.microsoft.com/en-us/library/azure/mt403303.aspx#clientID  
        static string clientIDFromAzureAppRegistration = "{clientID}";  
  
        static void Main(string[] args)  
        {  
            //Note: This example uses the "DefaultCatalog" keyword to update the user's default catalog.  You may alternately  
            //specify the actual catalog name.  
            string catalogName = "DefaultCatalog";  
  
            string registerJson = Register(catalogName, OrdersJsonWithEveryoneContributor());  
  
            Console.ReadLine();  
        }  
  
        static AuthenticationResult AccessToken()  
        {  
            //Get access token:  
            // To call a Data Catalog REST operation, create an instance of AuthenticationContext and call AcquireToken  
            // AuthenticationContext is part of the Active Directory Authentication Library NuGet package  
            // To install the Active Directory Authentication Library NuGet package in Visual Studio,  
            //  run "Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory" from the nuget Package Manager Console.  
  
            //Resource Uri for Data Catalog API  
            string resourceUri = "https://api.azuredatacatalog.com";  
  
            //To learn how to register a client app and get a Client ID, see https://msdn.microsoft.com/en-us/library/azure/mt403303.aspx#clientID     
            string clientId = clientIDFromAzureAppRegistration;  
  
            //A redirect uri gives AAD more details about the specific application that it will authenticate.  
            //Since a client app does not have an external service to redirect to, this Uri is the standard placeholder for a client app.  
            string redirectUri = "https://login.live.com/oauth20_desktop.srf";  
  
            // Create an instance of AuthenticationContext to acquire an Azure access token  
            // OAuth2 authority Uri  
            string authorityUri = "https://login.windows.net/common/oauth2/authorize";  
            AuthenticationContext authContext = new AuthenticationContext(authorityUri);  
  
            // Call AcquireToken to get an Azure token from Azure Active Directory token issuance endpoint  
            //  AcquireToken takes a Client Id that Azure AD creates when you register your client app.  
            return authContext.AcquireToken(resourceUri, clientId, new Uri(redirectUri), PromptBehavior.RefreshSession);  
        }  
  
        static string Register(string catalogName, string json)  
        {  
            string location = string.Empty;  
            string fullUri = string.Format("https://api.azuredatacatalog.com/catalogs/{0}/views/{1}?api-version=2016-03-30", catalogName, viewType);  
  
            //Create a POST WebRequest as a Json content type  
            HttpWebRequest request = System.Net.WebRequest.Create(fullUri) as System.Net.HttpWebRequest;  
            request.KeepAlive = true;  
            request.Method = "POST";  
            try  
            {  
                var response = SetRequestAndGetResponse(request, json);  
  
                //Get the Response header which contains the data asset ID  
                //The format is: tables/{data asset ID}  
                location = httpWebResponse.Headers["Location"];  
            }  
            catch (WebException ex)  
            {  
                Console.WriteLine(ex.Message);  
                Console.WriteLine(ex.Status);  
                if (ex.Response != null)  
                {  
                    // can use ex.Response.Status, .StatusDescription  
                    if (ex.Response.ContentLength != 0)  
                    {  
                        using (var stream = ex.Response.GetResponseStream())  
                        {  
                            using (var reader = new StreamReader(stream))  
                            {  
                                Console.WriteLine(reader.ReadToEnd());  
                            }  
                        }  
                    }  
                }  
                location = null;  
            }  
            return location;  
        }  
  
        static HttpWebResponse SetRequestAndGetResponse(HttpWebRequest request, string payload = null)  
        {  
            while (true)  
            {  
                //To authorize the operation call, you need an access token which is part of the Authorization header  
                request.Headers.Add("Authorization", AccessToken().CreateAuthorizationHeader());  
                //Set to false to be able to intercept redirects  
                request.AllowAutoRedirect = false;  
  
                if (!string.IsNullOrEmpty(payload))  
                {  
                    byte[] byteArray = Encoding.UTF8.GetBytes(payload);  
                    request.ContentLength = byteArray.Length;  
                    request.ContentType = "application/json";  
                    //Write JSON byte[] into a Stream  
                    request.GetRequestStream().Write(byteArray, 0, byteArray.Length);  
                }  
                else  
                {  
                    request.ContentLength = 0;  
                }  
  
                HttpWebResponse response = request.GetResponse() as HttpWebResponse;  
  
                // Requests to **Azure Data Catalog (ADC)** may return an HTTP 302 response to indicate  
                // redirection to a different endpoint. In response to a 302, the caller must re-issue  
                // the request to the URL specified by the Location response header.  
                if (response.StatusCode == HttpStatusCode.Redirect)  
                {  
                    string redirectedUrl = response.Headers["Location"];  
                    HttpWebRequest nextRequest = WebRequest.Create(redirectedUrl) as HttpWebRequest;  
                    nextRequest.Method = request.Method;  
                    request = nextRequest;  
                }  
                else  
                {  
                    return response;  
                    break;  
                }  
            }  
        }  
  
        static string OrdersJsonWithEveryoneContributor()  
        {  
            return @"  
            {  
                'roles': [  
                    {  
                        'role': 'Contributor',  
                        'members': [  
                            {  
                                'objectId': '00000000-0000-0000-0000-000000000201'  
                            }  
                        ]  
                    }  
                ],  
                'properties': {  
                    'fromSourceSystem': 'true',  
                    'name': 'Orders',  
                    'dataSource': {  
                        'sourceType': 'SQL Server',  
                        'objectType': 'Table'  
                    },  
                    'dsl': {  
                        'protocol': 'tds',  
                        'authentication': 'windows',  
                        'address': {  
                            'server': 'MyServer.contoso.com',  
                            'database': 'NORTHWND',  
                            'schema': 'dbo',  
                            'object': 'Orders'  
                        }  
                    },  
                    'lastRegisteredBy': {  
                        'upn': 'user1@contoso.com',  
                        'firstName': 'User1FirstName',  
                        'lastName': 'User1LastName'  
                    },  
                    'containerId': 'containers/a9f8a2e1-d826-7c0c-b186-c7f4334a6b4f'  
                },  
                'annotations': {  
                    'schema': {  
                        'roles': [  
                            {  
                                'role': 'Contributor',  
                                'members': [  
                                    {  
                                        'objectId': '00000000-0000-0000-0000-000000000201'  
                                    }  
                                ]  
                            }  
                        ],  
                        'properties': {  
                            'fromSourceSystem': 'true',  
                            'columns': [  
                                {  
                                    'name': 'OrderID',  
                                    'isNullable': false,  
                                    'type': 'int',  
                                    'maxLength': 4,  
                                    'precision': 10  
                                },  
                                {  
                                    'name': 'CustomerID',  
                                    'isNullable': true,  
                                    'type': 'nchar',  
                                    'maxLength': 10,  
                                    'precision': 0  
                                },  
                                {  
                                    'name': 'EmployeeID',  
                                    'isNullable': true,  
                                    'type': 'int',  
                                    'maxLength': 4,  
                                    'precision': 10  
                                },  
                                {  
                                    'name': 'OrderDate',  
                                    'isNullable': true,  
                                    'type': 'datetime',  
                                    'maxLength': 8,  
                                    'precision': 23  
                                }  
                            ]  
                        }  
                    }  
                }  
            }";  
        }  



## Get with Annotations
Gets a data asset with annotations. 
 
It supports optional Accept header parameter `adc.metadata` that requests ETags to be included in the response for all the items. Use values minimal or full to get ETags in response. The valid values are `none`, `minimal`, and `full`.  

### Request  
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

 
### Response  
  
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



## Search
Searches over data assets based on the search terms provided. 
 


### Request  
	GET https://api.azuredatacatalog.com/catalogs/{catalog_name}/search/search?api-version={api-version}&searchTerms={search_terms}&facets={facet_terms}&startPage={start_page}&count={count}&view={data_source}  
  
> [AZURE.NOTE] Some HTTP client implementations may automatically re-issue requests in response to a 302 from the server, but typically strip **Authorization headers** from the request. Since the Authorization header is required to make requests to ADC, you must ensure the Authorization header is still provided when re-issuing a request to a redirect location specified by ADC. Below is sample code demonstrating this using the .NET HttpWebRequest object.  
  
### Uri parameters  
|Name|Description|Data Type  
|-|-|-  
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String  
|api-version|The API version.|String  
  
### Query parameters  
|Name|Description|Data Type  
|-|-|-  
|searchTerms|Required. Terms to search on.|String  
|facets|Optional A comma separated field names to facet the results on.|String  
|startPage|Optional Start Page of the results used for Paging along with count parameter. Allowed values are greater than 0, if a value less than or equal to 0 is passed, an HTTP error with error code 400 is returned.|String  
|count|Optional Number of results wanted in one page (Paging). The default value is 10. Allowed values are in interval from 1 to 100 inclusive. If a value out of this range is passed, an HTTP error with error code 400 is returned. To get the next portion of search results, repeat the request but increase startPage by 1.|Integer  
|view|Optional Gets the view the client wants to see, for now the only supported option in DataSource.|String  
  
### GET example  
https://api.azuredatacatalog.com/catalogs/DefaultCatalog/search/search?searchTerms=My_Server&count=10&startPage=1&api-version=2016-03-30  
### Header  
x-ms-client-request-id: 546f053a…a1612f3a3d69  
Authorization:  Bearer eXJ0eyAiOiJKV1QiLCJhbGciOi...  
  

### Response  
### Status codes  
|Code|Description  
|-|-  
|200|OK. A successful operation with search result.  
  
### Content-Type  
application/json  
### Header  
x-ms-request-id: 0ab2e798…088223257ad2  
Content-Length:  3926  
### Body  
    {  
        "query": {  
            "id": "bd067219...4ba9a56e204b",  
            "searchTerms": "My_server",  
            "startIndex": 1,  
            "startPage": 1,  
            "count": 1,  
        "id": "bd067219...4ba9a56e204b",  
        "totalResults": 508,  
        "startIndex": 1,  
        "itemsPerPage": 1,  
        "results": [{  
            "updated": "0001-01-01T00:00:00",  
            "content": {  
                  "properties": {  
                    "fromSourceSystem": true,  
                    "name": "MyTable",  
                    "dsl": {  
                      "protocol": "tds",  
                      "authentication": "windows",  
                      "address": {  
                        "server": "My_SERVER",  
                        "database": "my_DB",  
                        "schema": "my_SCHEMA",  
                        "object": "my_TABLE"  
                      }  
                    },  
                    "dataSource": {  
                      "sourceType": "SQL Server",  
                      "objectType": "Table"  
                    },  
                    "lastRegisteredBy": {  
                      "upn": "user1@contoso.com",  
                      "firstName": "User1FirstName",  
                      "lastName": "User1LastName"  
                    },  
                    "containerId": "https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/views/containers/a9f8a2e1-d826-7c0c-b186-c7f4334a6b4f"  
                  },  
                  "id": "https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/views/tables/08d91f0d-26a0-1e8e-ab3b-d463ac3e62cb",  
                  "type": "Microsoft.DataSource.Table.1",  
                  "timestamp": "2016-03-15T23:20:12.5423855",  
                  "annotations": {  
                    "schema": {  
                      "properties": {  
                        "fromSourceSystem": true,  
                        "columns": [  
                          {  
                            "name": "ID",  
                            "type": "int",  
                            "maxLength": 4,  
                            "precision": 10,  
                            "isNullable": false  
                          },  
                          {  
                            "name": "Column2",  
                            "type": "nchar",  
                            "maxLength": 10,  
                            "precision": 0,  
                            "isNullable": true  
                          }  
                        ]  
                      },  
                      "id": "https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/views/tables/08d91f0d-26a0-1e8e-ab3b-d463ac3e62cb/schema",  
                      "type": "Microsoft.DataSource.Schema.1",  
                      "timestamp": "2016-03-15T23:20:12.5423855",  
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
                      ]  
                    }  
                  },  
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
                  ]  
                },  
            "hitProperties": [{  
                "fieldPath": "properties.dsl.address.server",  
                "highlightDetail": [{  
                    "highlightedWords": [{  
                        "word": "My_sERVER"  
                    }],  
                    "highlightedFragment": "My_sERVER"  
                }]  
            },  
            {  
                "fieldPath": "properties.dataSource.sourceType",  
                "highlightDetail": [{  
                    "highlightedWords": [{  
                        "word": "Server"  
                    }],  
                    "highlightedFragment": "SQL Server"  
                }]  
            },  
            {  
                "fieldPath": "properties.dsl.address.object",  
                "highlightDetail": [{  
                    "highlightedWords": [{  
                        "word": "my"  
                    }],  
                    "highlightedFragment": "my_TABLE"  
                }]  
            },  
            {  
                "fieldPath": "properties.dsl.address.database",  
                "highlightDetail": [{  
                    "highlightedWords": [{  
                        "word": "my"  
                    }],  
                    "highlightedFragment": "my_DB"  
                }]  
            },  
            {  
                "fieldPath": "properties.dsl.address.schema",  
                "highlightDetail": [{  
                    "highlightedWords": [{  
                        "word": "my"  
                    }],  
                    "highlightedFragment": "my_SCHEMA"  
                }]  
            }]  
        }]  
    }  
  

### Example  
This example shows you how to get an Azure AD access token, and perform a **Search** operation.  
  
**Note** To find the **Catalog** name, sign into **Azure Data Catalog**, and choose **User**. You will see the **Catalog** name.  
  
        using System;  
        using System.Net;  
        using Microsoft.IdentityModel.Clients.ActiveDirectory;  
        using System.IO;  
  
        ...  
  
        //To learn how to register a client app and get a Client ID,  
        // see https://msdn.microsoft.com/en-us/library/azure/mt403303.aspx#clientID  
        static string clientIDFromAzureAppRegistration = "{clientID}";  
  
        static void Main(string[] args)  
        {  
            //Note: This example uses the "DefaultCatalog" keyword to update the user's default catalog.  You may alternately  
            //specify the actual catalog name.  
            string catalogName = "DefaultCatalog";  
  
            //Search everything  
            string searchTerm = string.Empty;  
  
            string searchJson = Search(catalogName, searchTerm);  
            //Other examples "tags:=Sales", "upn:{username}"  
  
            Console.WriteLine(searchJson);  
        }  
  
        static AuthenticationResult AccessToken()  
        {  
            //Get access token:  
            // To call a Data Catalog REST operation, create an instance of AuthenticationContext and call AcquireToken  
            // AuthenticationContext is part of the Active Directory Authentication Library NuGet package  
            // To install the Active Directory Authentication Library NuGet package in Visual Studio,  
            //  run "Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory" from the nuget Package Manager Console.  
  
            //Resource Uri for Data Catalog API  
            string resourceUri = "https://api.azuredatacatalog.com";  
  
            //To learn how to register a client app and get a Client ID, see https://msdn.microsoft.com/en-us/library/azure/mt403303.aspx#clientID    
            string clientId = clientIDFromAzureAppRegistration;  
  
            //A redirect uri gives AAD more details about the specific application that it will authenticate.  
            //Since a client app does not have an external service to redirect to, this Uri is the standard placeholder for a client app.  
            string redirectUri = "https://login.live.com/oauth20_desktop.srf";  
  
            // Create an instance of AuthenticationContext to acquire an Azure access token  
            // OAuth2 authority Uri  
            string authorityUri = "https://login.windows.net/common/oauth2/authorize";  
            AuthenticationContext authContext = new AuthenticationContext(authorityUri);  
  
            // Call AcquireToken to get an Azure token from Azure Active Directory token issuance endpoint  
            //  AcquireToken takes a Client Id that Azure AD creates when you register your client app.  
            return authContext.AcquireToken(resourceUri, clientId, new Uri(redirectUri), PromptBehavior.RefreshSession);  
        }  
  
        static string Search(string catalogName, string searchTerm)  
        {  
            string responseContent = string.Empty;  
  
            //NOTE: To find the Catalog Name, sign into Azure Data Catalog, and choose User. You will see a list of Catalog names.            
            string fullUri =  
                string.Format("https://api.azuredatacatalog.com/catalogs/{0}/search/search?searchTerms={1}&count=10&api-version=2016-03-30", catalogName, searchTerm);  
  
            //Create a GET WebRequest  
            HttpWebRequest request = (HttpWebRequest)WebRequest.Create(fullUri);  
            request.Method = "GET";  
  
            try  
            {  
                //Get HttpWebResponse from GET request  
                using (HttpWebResponse httpResponse = SetRequestAndGetResponse(request))  
                {  
                    //Get StreamReader that holds the response stream  
                    using (StreamReader reader = new System.IO.StreamReader(httpResponse.GetResponseStream()))  
                    {  
                        responseContent = reader.ReadToEnd();  
                    }  
                }  
            }  
            catch (WebException ex)  
            {  
                Console.WriteLine(ex.Message);  
                Console.WriteLine(ex.Status);  
                if (ex.Response != null)  
                {  
                    // can use ex.Response.Status, .StatusDescription  
                    if (ex.Response.ContentLength != 0)  
                    {  
                        using (var stream = ex.Response.GetResponseStream())  
                        {  
                            using (var reader = new StreamReader(stream))  
                            {  
                                Console.WriteLine(reader.ReadToEnd());  
                            }  
                        }  
                    }  
                }  
                return null;  
            }  
  
            return responseContent;  
        }  
  
        static HttpWebResponse SetRequestAndGetResponse(HttpWebRequest request, string payload = null)  
        {  
            while (true)  
            {  
                //To authorize the operation call, you need an access token which is part of the Authorization header  
                request.Headers.Add("Authorization", AccessToken().CreateAuthorizationHeader());  
                //Set to false to be able to intercept redirects  
                request.AllowAutoRedirect = false;  
  
                if (!string.IsNullOrEmpty(payload))  
                {  
                    byte[] byteArray = Encoding.UTF8.GetBytes(payload);  
                    request.ContentLength = byteArray.Length;  
                    request.ContentType = "application/json";  
                    //Write JSON byte[] into a Stream  
                    request.GetRequestStream().Write(byteArray, 0, byteArray.Length);  
                }  
                else  
                {  
                    request.ContentLength = 0;  
                }  
  
                HttpWebResponse response = request.GetResponse() as HttpWebResponse;  
  
                // Requests to **Azure Data Catalog (ADC)** may return an HTTP 302 response to indicate  
                // redirection to a different endpoint. In response to a 302, the caller must re-issue  
                // the request to the URL specified by the Location response header.    
                if (response.StatusCode == HttpStatusCode.Redirect)  
                {  
                    string redirectedUrl = response.Headers["Location"];  
                    HttpWebRequest nextRequest = WebRequest.Create(redirectedUrl) as HttpWebRequest;  
                    nextRequest.Method = request.Method;  
                    request = nextRequest;  
                }  
                else  
                {  
                    return response;  
                    break;  
                }  
            }  
        }


## Delete
Deletes a data asset and all annotations (if any) attached to it.  

It supports optional If-Match header for optimistic concurrency control. Only weak format, such as W/"123456789", is supported.  


### Request  
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


### Response  
### Status codes  
|Code|Description  
|-|-  
|204|NoContent <br/> **NOTE**: Delete operation semantic is delete if exists, so if asset or annotation does not exist success status code 204 (NoContent) is returned.  
|412|Precondition Failed. The request was cancelled because of the ETag mismatch.  
  
### Content-Type  
application/json  
### Header  
x-ms-request-id: 664f86cf…5e512fa78e92  

## Update Annotation
Updates an annotation.  

The items can optionally contain ETag values to enable optimistic concurrency control for them.  

### Request  
	PUT https://api.azuredatacatalog.com/catalogs/{catalog_name}/views/{view_name}/{view_item_id}/{nested_view_name}/{nested_non_singleton_view_item_id}?api-version={api-version} 
 
	PUT https://api.azuredatacatalog.com/catalogs/{catalog_name}/views/{view_name}/{view_item_id}/{nested_view_name}?api-version={api-version}  
  
> [AZURE.NOTE] Some HTTP client implementations may automatically re-issue requests in response to a 302 from the server, but typically strip **Authorization headers** from the request. Since the Authorization header is required to make requests to ADC, you must ensure the Authorization header is still provided when re-issuing a request to a redirect location specified by ADC. Below is sample code demonstrating this using the .NET HttpWebRequest object.  
  
### Uri parameters  
|Name|Description|Data Type  
|-|-|-  
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String  
|view_name|Name of Data Asset View.|String  
|view_item_id|Id of a View item.|String  
|nested_view_name|Name of a nested View.|String  
|nested_non_singleton_view_item_id|Id of a nested non-singleton View item. Must be provided for a non-singleton view.|String  
|api-version|The API version.|String  
  
### PUT example for a singleton Documentation view  
PUT https://api.azuredatacatalog.com/catalogs/DefaultCatalog/views/tables/042297b0...1be45ecd462a/documentation?api-version=2016-03-30  
  
### Header  
Content-Type:   application/json; charset=utf-8    
x-ms-client-request-id:   059692ee-...-57490fcec42c    
Authorization:  Bearer eXJ0eyAiOiJKV1QiLCJhbGciOi...  
### Body schema  
  
    Body:  
        {  
            "fromSourceSystem": false,  
            "etag": "123456789",  
            "content": "<new documentation content>",  
            "mimetype": "text",  
        }  


### Response  
#### Status codes  
|Code|Description  
|-|-  
|200|OK. An existing annotation was updated.  
|412|Precondition Failed. The request was cancelled because of the ETag mismatch in at least one item.  
  
#### Content-Type  
application/json  
#### Header  
x-ms-request-id: 3b8668da…1558d0f407c0  



## Delete Annotation
Deletes an annotation and all nested annotations (if any). 
 
It supports optional If-Match header for optimistic concurrency control. Only weak format, such as W/"123456789", is supported.  



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


### Response  
#### Status codes  
|Code|Description  
|-|-  
|204|NoContent  
|412|Precondition Failed. The request was cancelled because of the ETag mismatch.  
  
#### Content-Type  
application/json  
#### Header  
x-ms-request-id: 276b9dc4…e5f7017805c  
  

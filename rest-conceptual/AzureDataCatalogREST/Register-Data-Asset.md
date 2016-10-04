---
title: "Register Data Asset"
ms.custom: na
ms.date: 2016-07-21
ms.prod: azure
ms.reviewer: na
ms.service: data-catalog
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 16a784a4-ad83-4a5c-82dd-5f3a4acf9dc1
caps.latest.revision: 53
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
# Register Data Asset
---  
[Request](#request) | [Response](#response) | [Example](#example) | [Get started sample on GitHub](https://github.com/Azure-Samples/data-catalog-dotnet-get-started)  
<a name="top"/>  
  
The **Register Data Asset** operation registers a new data asset or updates an existing one if an asset with the same identity already exists. The items can optionally contain ETag values to enable optimistic concurrency control for them.  
<a name="request"/>  
## Request  
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
  
<a name="response"/>  
## Response  
### Status codes  
|Code|Description  
|---|---  
|200|OK. An existing asset was updated.  
|201|Created. The request was fulfilled and a new asset was created.  
|412|Precondition Failed. The request was cancelled because of the ETag mismatch in at least one item.  
  
### Content-Type  
application/json  
  
### Header  
HTTP/1.1 201 Created  
x-ms-request-id: 72cf83c0…058f2b2a0c68  
Location: https://e2255231-6dd3-1a0d-a6d8-7fc96dd780c2-mycatalog.api.azuredatacatalog.com/catalogs/MyCatalog/views/tables/042297b0…1be45ecd462a  
  
## Supported Data Sources  
  
Please refer <a href="https://azure.microsoft.com/en-us/documentation/articles/data-catalog-dsr/">here</a> for the list of currently supported data sources objects.  
  
  
<a name="example"/>  
## Example  
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

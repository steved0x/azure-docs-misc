---
title: "Search Data Asset1"
ms.custom: na
ms.date: 2016-07-21
ms.prod: azure
ms.reviewer: na
ms.service: data-catalog
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
H1: Search Data Asset
ms.assetid: a259794c-c6bb-4486-ae7a-34307346bda9
caps.latest.revision: 34
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
# Search Data Asset1
---  
[Request](#request) | [Response](#response) | [Example](#example)  
<a name="top"/>  
  
The **Search Data Asset** operation searches over data assets based on the search terms provided.  
<a name="request"/>  
## Request  
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
  
<a name="response"/>  
## Response  
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
  
<a name="example"/>  
## Example  
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
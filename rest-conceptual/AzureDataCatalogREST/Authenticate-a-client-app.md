---
title: "Authenticate a client app"
ms.custom: na
ms.date: 2016-07-21
ms.prod: azure
ms.reviewer: na
ms.service: data-catalog
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: f9ed3fd6-b083-495e-ab77-baa88b4c2f04
caps.latest.revision: 25
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
# Authenticate a client app
---  
This article shows you how to authenticate a Data Catalog client app. It includes examples in C#; however, the authentication process is the same for other programming languages.  
  
## In this article  
- [What you need to authenticate a Data Catalog client app](#What)  
- [How to make a request to Data Catalog REST API using a token](#Datarequest)  
- [Azure Authentication Context Flow](#Flow)  

  
Data Catalog client apps use Active Directory (AAD) to authenticate users and protect applications. Authentication is the process of identifying an app or user. To identify your client app in AAD, you register your app with AAD. When you register a client app in Azure Active Directory, you give your app access to the Data Catalog APIs. To learn how to register your Data Catalog client app, see [Register a client app](../AzureDataCatalogREST/Register-a-client-app.md).  
  
Data Catalog REST API calls are made on behalf of an authenticated user by passing a token in the "Authorization" header of the request. The token is acquired through Azure Active Directory.  
<a name="What"></a>  
## What you need to authenticate a Data Catalog client app  
To authenticate a Data Catalog client app and perform a REST web request, you need to:  
  
1. **Register your client app** - To register a Data Catalog client app, see [Register a client app](../AzureDataCatalogREST/Register-a-client-app.md). When you register a client app in **Azure Active Directory**, you give your app access to the Data Catalog APIs.  
2. **Assign the client id for your app** - To get the client id for your app, see [How to get a client app id](../AzureDataCatalogREST/Register-a-client-app.md#clientID). The Client ID is used by the application to identify themselves to the users that they are requesting permissions from.   
    - In your client app code, assign the **clientID** variable to the client id of your Azure application.  
3. **Assign the redirect Uri** - For a client app, a redirect uri gives AAD more details about the specific application it will authenticate. A uniform resource identifier (URI) is a value to identify a name of a resource.  
    - In your client app code, assign the **redirectUri** to https://login.live.com/oauth20_desktop.srf. Since a client app does not have an external service to redirect to, this URI is the standard placeholder for client apps.  
              
4. **Assign the resource Uri for Data Catalog API** - The resource Uri identifies the Data Catalog API resource.  
    - In your client app code, assign the **resourceUri** to "https://datacatalog.azure.com".  
5. **Assign the OAuth2 authority uri** - The authority Uri identifies the OAuth2 authority resource.  
    - In your client app code, assign an authority Uri to "https://login.windows.net/common/oauth2/authorize".    
  
To make a data request to the Data Catalog REST service, you need to supply an access token. In a .NET client app, you use the [Windows Azure Authentication Library (ADAL)](https://msdn.microsoft.com/library/azure/jj573266.aspx) to get an access token. Here’s the process. Below is an example **AccessToken()** method.  
  
**Important** To authenticate a client app, you must add a reference to **Microsoft.IdentityModel.Clients.ActiveDirectory**, which is included in the Windows Azure Authentication Library (ADAL). The sample code in this article works only with the version 2.19.208020213 of Microsoft.IdentityModel.Clients.ActiveDirectory.  Run the following command from NuGet Package Manager Console.

   ```  
  Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory Version 2.19.208020213 
   ```  
  
## Steps to get an access token  
1. **Create an instance of AuthenticationContext** - AuthenticationContext is the main class representing the token issuing authority for Azure AD resources. The constructor takes:  
    - An OAuth2 authorityUri   
  
    ```  
    string authorityUri = "https://login.windows.net/common/oauth2/authorize";  
      AuthenticationContext authContext = new AuthenticationContext(authorityUri);  
    ```  
2. **Call AuthenticationContext.AcquireToken() to get a token** -  The method takes:  
    - Data Catalog API resourceUri  
    - Your Data Catalog app clientID  
    - Your Data Catalog app redirectUri   
  
    ```  
      AuthenticationResult token = authContext.AcquireToken(resourceUri, clientId, new Uri(redirectUri), PromptBehavior.RefreshSession);  
    ```  
  
      You can get the token with **authResult.AccessToken** or **authResult.CreateAuthorizationHeader()**. CreateAuthorizationHeader returns a fully qualified **Bearer** header such as the following:  
  
      ```  
      Bearer eyJ0eXAiOiJKV1QiLCJhbGciO...  
      ```  
      
For more information about what **AuthenticationContext** does to get a token, see [Azure Authentication Context Flow](#Flow).  
  
### C# example - Get access token  
 
**Important** The sample code in this article works only with the version **2.19.208020213** of **Microsoft.IdentityModel.Clients.ActiveDirectory**.  Run the following command from NuGet Package Manager Console (Tools -> NuGet Package Manager -> Package Manager Console).

   ```  
  Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory Version 2.19.208020213 
   ```  
  
In a .NET client app, you use **AuthenticationContext** to get an access token.   
  
```  
        static AuthenticationResult AccessToken()  
        {  
            //Get access token:   
            // To call a Data Catalog REST operation, create an instance of AuthenticationContext and call AcquireToken  
            // AuthenticationContext is part of the Active Directory Authentication Library NuGet package  
            // To install the Active Directory Authentication Library NuGet package in Visual Studio,   
            //  run "Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory Version 2.19.208020213" from the nuget Package Manager Console.  
  
            //Resource Uri for Data Catalog API  
            string resourceUri = "https://datacatalog.azure.com";  
  
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
```  
  
<a name="Datarequest"></a>  
## Make a request to Data Catalog REST API using a token  
  
After you get an access token from Active Directory (AAD), you use the token to make a web request to the Data Catalog REST API. To create a Data Catalog REST web request, you add an access token to a request header. For example, in a .NET app, add the   
  
```  
HttpWebRequest request = System.Net.WebRequest.Create(apiUrl) as System.Net.HttpWebRequest;  
...  
string authHeader = authResult.CreateAuthorizationHeader();             
request.Headers.Add("Authorization", authHeader);  
```  
  
<a name="Flow"></a>  
## Azure Authentication Context Flow  
In a .NET client app, you use **AuthenticationContext** to acquire an Azure access token. **AuthenticationContext** is the main class representing the token issuing authority for Azure AD resources. **AuthenticationContext** does the following:  
1.  AuthenticationContext starts the flow by redirecting the user agent to the Azure Active Directory authorization endpoint. The user authenticates and consents, if consent is required.  
2.  The Azure Active Directory authorization endpoint redirects the user agent back to the AuthenticationContext with an authorization code. The user agent returns an authorization code to the client application’s redirect URI.  
3.  The AuthenticationContext requests an access token from the Azure Active Directory token issuance endpoint. It presents the authorization code to prove that the user has consented.  
4.  The Azure Active Directory token issuance endpoint returns an access token.  
5.  The client application uses the access token to authenticate to the Web API.  
6.  After authenticating the client application, the Data Catalog REST API returns the requested data.  
  
To learn more about Azure Active Directory (Azure AD) authorization flow, see [Authorization Code Grant Flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).  
   
  
## Related topics  
- [Azure AD Authentication Library for .NET](https://msdn.microsoft.com/library/azure/jj573266.aspx)  
- [Active Directory Authentication Library (ADAL) v1 for .NET](http://www.cloudidentity.com/blog/2013/09/12/active-directory-authentication-library-adal-v1-for-net-general-availability/)  
- [OAuth 2.0 in Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx)  
- [Authorization Code Grant Flow](https://msdn.microsoft.com/library/azure/dn645542.aspx)  
- [Authentication Scenarios for Azure AD](https://msdn.microsoft.com/library/azure/dn499820.aspx)  

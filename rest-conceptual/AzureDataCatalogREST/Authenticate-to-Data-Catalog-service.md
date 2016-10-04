---
title: "Authenticate to Data Catalog service"
ms.custom: na
ms.date: 2016-07-21
ms.prod: azure
ms.reviewer: na
ms.service: data-catalog
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 0dae6844-5732-4374-8c43-c62e3071df44
caps.latest.revision: 16
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
# Authenticate to Data Catalog service
The Data Catalog REST API is a REST-based API that provides programmatic access to Data Catalog resources to register, annotate and search data assets programmatically.  
### In this article  
- [Introduction to authentication in Data Catalog](#intro)  
- [Azure app client ID](#clientID)  
  
<a name="intro"/>  
## Introduction to authentication in Data Catalog  
Data Catalog apps are integrated with **Azure Active Directory** (Azure AD) to provide secure sign in and authorization for your app. To integrate a Data Catalog app with Azure AD, you register the details about your application with Azure AD by using the Azure Management Portal. When you register an app in Azure Active Directory, the application outsources authentication to Azure AD. App registration involves telling Azure AD about your application including the URL where it is located, the URL to send replies after authentication, and the URI to identify your application. When you register a client app or web app in Azure AD, you give your app access to the Data Catalog REST API.  
  
A Data Catalog app uses a **Client ID** to identify itself to Azure AD. See [Azure app client ID](#clientID).  
  
To learn how to register and authenticate a Data Catalog app:  
  
- **Data Catalog client app**: See [Register a client app](../AzureDataCatalogREST/Register-a-client-app.md) and [Authenticate a Data Catalog client app](../AzureDataCatalogREST/Authenticate-a-client-app.md).  
  
- To learn how to use Azure authentication on different platforms: The [Azure Authentication Libraries](https://msdn.microsoft.com/library/azure/dn151135.aspx) are available on different platforms to help developers easily authenticate users to cloud or on premise Active Directory (AD) to obtain access tokens for securing API calls. This topic contains a roadmap to the authentication libraries available on different platforms and to helpful resources for each, including source code and samples.  
  
<a name="clientID"/>  
## Azure app client ID  
An Azure app has a **Client ID** that is used by the application to identify themselves to the users that they are requesting permissions from. You use a **Client ID** to get an authentication token. To get an Azure **Client ID**, see [How to get a client app id](../AzureDataCatalogREST/Register-a-client-app.md#clientID).  
  
For a complete sample of how to use an Azure **Client ID** to authenticate a client app, see [Authenticate a client app](../AzureDataCatalogREST/Authenticate-a-client-app.md).  
  

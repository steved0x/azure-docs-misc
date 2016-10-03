---
title: "API Management REST"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: api-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 1b96aa01-6b6a-4d20-b8f3-ccd1d668b2f9
caps.latest.revision: 20
author: steved0x
manager: douge
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
# API Management REST
Azure API Management provides a REST API for performing operations on selected entities, such as users, groups, products, and subscriptions. This reference provides a guide for working with the API Management REST API, as well as specific reference information for each available operation, grouped by entity.  
  
 For more information about working with the REST API, see the [API Management .NET REST API Sample](https://github.com/Azure/api-management-samples/tree/master/restApiDemo) and the [Getting Started with Azure API Management REST API](http://azure.microsoft.com/documentation/videos/getting-started-with-azure-api-management-rest-api/) video.  
  
## In this topic  
  
-   [Prerequisites](../rest-conceptual/API-Management-REST.md#Prerequisites)  
  
    -   [Enable access to the REST API](../rest-conceptual/API-Management-REST.md#EnableRESTAPI)  
  
    -   [Default media type](../rest-conceptual/API-Management-REST.md#DefaultMediaType)  
  
    -   [Authentication](../rest-conceptual/API-Management-REST.md#Authentication)  
  
    -   [Base URL](../rest-conceptual/API-Management-REST.md#BaseURL)  
  
    -   [Version Query Parameter](../rest-conceptual/API-Management-REST.md#VersionQueryParameter)  
  
-   [API Management REST API version history](../rest-conceptual/API-Management-REST.md#VersionHistory)  
  
-   [API Management REST API entities](../rest-conceptual/API-Management-REST.md#Entities)  
  
##  <a name="Prerequisites"></a> Prerequisites  
 To successfully make calls to the API Management REST API, the following prerequisites must be met.  
  
-   [Enable access to the REST API](../rest-conceptual/API-Management-REST.md#EnableRESTAPI)  
  
-   [Default media type](../rest-conceptual/API-Management-REST.md#DefaultMediaType)  
  
-   [Authentication](../rest-conceptual/API-Management-REST.md#Authentication)  
  
-   [Base URL](../rest-conceptual/API-Management-REST.md#BaseURL)  
  
-   [Version Query Parameter](../rest-conceptual/API-Management-REST.md#VersionQueryParameter)  
  
###  <a name="EnableRESTAPI"></a> Enable access to the REST API  
 Access to the API Management REST API must be granted before calls can be successfully made. To enable access, sign into the [Azure Classic Portal](https://manage.windowsazure.com/), navigate to your API Management service instance, and click **Manage** to open the publisher portal.  
  
 ![API Management Console](../rest-conceptual/media/APIManagementConsole.jpg "APIManagementConsole")  
  
 Click **Security** in the **API Management** section of the left navigation menu, select the **API Management REST API** tab, and ensure that the **Enable API Management REST API** checkbox is checked.  
  
 ![API Management System Settings](../rest-conceptual/media/APIManagementSystemSettings.jpg "APIManagementSystemSettings")  
  
> [!IMPORTANT]
>  If the **Enable API Management REST API** checkbox is not checked, calls made to the REST API for that service instance will fail.  
  
###  <a name="DefaultMediaType"></a> Default media type  
 The default media type for requests and responses is `application/json`. Where noted, some operations support other content types. If no additional content type is mentioned for a specific operation, then the media type is `application/json`.  
  
###  <a name="Authentication"></a> Authentication  
 Each request to the API Management REST API must be accompanied by an `Authorization` header containing a valid shared access token, as shown in the following example.  
  
```  
Authorization: SharedAccessSignature uid=53dd860e1b72ff0467030003&ex=2014-08-04T22:03:00.0000000Z&sn=ItH6scUyCazNKHULKA0Yv6T+Skk4bdVmLqcPPPdWoxl2n1+rVbhKlplFrqjkoUFRr0og4wjeDz4yfThC82OjfQ==  
```  
  
 This access token can be generated programmatically or from within the API Management publisher portal. For instructions on generating and retrieving the access token, see [To manually create an access token](../rest-conceptual/Azure-API-Management-REST-API-Authentication.md#ManuallyCreateToken) and [To programmatically create an access token](../rest-conceptual/Azure-API-Management-REST-API-Authentication.md#ProgrammaticallyCreateToken).  
  
###  <a name="BaseURL"></a> Base URL  
 The Base URL of the API Management REST API conforms to the following template.  
  
 `https://{servicename}.management.azure-api.net`  
  
 This template contains the following parameter.  
  
-   `{serviceName}` is the service name as it was specified during service creation, for example `https://contosoapi.management.azure-api.net`.  
  
 All URLs returned by the API Management REST API are relative to this base URL, and all requests to the REST API must use this base URL template.  
  
###  <a name="VersionQueryParameter"></a> Version Query Parameter  
 All operations expect an `api-version` query parameter with a value in the format of `YYYY-MM-DD`, for example `2014-02-14`.  
  
> [!NOTE]
>  During the preview period for API Management, `-preview` is appended to the version query parameter, for example `2014-02-14-preview`.  
  
 If this query parameter is not passed in the query string of a request, the server will return a status code of `400 Bad Request`. For a list of supported versions, see the following [API Management REST API version history](../rest-conceptual/API-Management-REST.md#VersionHistory) section.  
  
##  <a name="VersionHistory"></a> API Management REST API version history  
 The following table shows the API Management REST API versions, and the major modifications that were made to each version. Each version is identified by a date, which is used as the value for the [Version Query Parameter](../rest-conceptual/API-Management-REST.md#VersionQueryParameter) when making an HTTP request.  
  
|Version|Description|  
|-------------|-----------------|  
|`2014-02-14-preview`|Initial public release of the API Management REST API.|  
  
## In this section  
  
###  <a name="Entities"></a> API Management REST API entities  
  
-   [API](../rest-conceptual/Azure-API-Management-REST-API-API-entity.md)  
  
-   [Authorization server](../rest-conceptual/Azure-API-Management-REST-API-Authorization-Server-entity.md)  
  
-   [Backend](../rest-conceptual/Azure-API-Management-REST-API-Backend-entity.md)  
  
-   [Certificate](../rest-conceptual/Azure-API-Management-REST-API-Certificate-entity.md)  
  
-   [Group](../rest-conceptual/Azure-API-Management-REST-API-Group-entity.md)  
  
-   [Logger](../rest-conceptual/Azure-API-Management-REST-API-Logger-entity.md)  
  
-   [Product](../rest-conceptual/Azure-API-Management-REST-API-Product-Entity.md)  
  
-   [Property](../rest-conceptual/Azure-API-Management-REST-API-Property-Entity.md)  
  
-   [Report](../rest-conceptual/Azure-API-Management-REST-API-Report-entity.md)  
  
-   [Subscription](../rest-conceptual/Azure-API-Management-REST-API-Subscription-entity.md)  
  
-   [Tenant](../rest-conceptual/Azure-API-Management-REST-API-Tenant-entity.md)  
  
-   [User](../rest-conceptual/Azure-API-Management-REST-API-User-entity.md)  
  
### Additional topics in this section  
  
-   [REST API contract reference](../rest-conceptual/Azure-API-Management-REST-API-contract-reference.md)  
  
-   [Authentication](../rest-conceptual/Azure-API-Management-REST-API-Authentication.md)
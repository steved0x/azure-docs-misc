---
title: "Azure API Management REST API Authorization Server entity"
ms.custom: na
ms.date: 2016-05-09
ms.prod: azure
ms.reviewer: na
ms.service: api-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 837d3669-12d4-4205-a95b-103729deb4fc
caps.latest.revision: 9
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
# Azure API Management REST API Authorization Server entity
This topic describes how to manage OAuth2 authorization servers using the API Management REST API.  
  
 For more information about working with the REST API, see the [API Management .NET REST API Sample](https://github.com/Azure/api-management-samples/tree/master/restApiDemo) and the [Getting Started with Azure API Management REST API](http://azure.microsoft.com/documentation/videos/getting-started-with-azure-api-management-rest-api/) video.  
  
## In this topic  
  
-   [Prerequisites](../ApiManagementREST/Azure-API-Management-REST-API-Authorization-Server-entity.md#Prerequisites)  
  
-   [Get a list of authorization servers](../ApiManagementREST/Azure-API-Management-REST-API-Authorization-Server-entity.md#List)  
  
-   [Get a specific authorization server](../ApiManagementREST/Azure-API-Management-REST-API-Authorization-Server-entity.md#Get)  
  
-   [Get the metadata for a specific authorization server](../ApiManagementREST/Azure-API-Management-REST-API-Authorization-Server-entity.md#HEAD)  
  
-   [Create a new authorization server](../ApiManagementREST/Azure-API-Management-REST-API-Authorization-Server-entity.md#PUT)  
  
-   [Update an authorization server](../ApiManagementREST/Azure-API-Management-REST-API-Authorization-Server-entity.md#PATCH)  
  
-   [Delete an authorization server](../ApiManagementREST/Azure-API-Management-REST-API-Authorization-Server-entity.md#DELETE)  
  
##  <a name="Prerequisites"></a> Prerequisites  
  
> [!IMPORTANT]
>  Before making any calls into the API Management REST API, please review the [Prerequisites](../ApiManagementREST/API-Management-REST.md#Prerequisites) section of the [API Management REST](../ApiManagementREST/API-Management-REST.md) guide. This specifies the necessary authentication, version parameters, supported media types, and other information required in order to successfully call the API Management REST API.  
  
##  <a name="List"></a> Get a list of authorization servers  
 This operation returns a collection of authorization servers defined within a service instance.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/authorizationServers|  
  
#### Request Parameters  
 None.  
  
#### Request Headers  
 None.  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|You can filter the results using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported<br /><br /> id:<br /><br /> - ge, le, eq, ne, gt, lt : substringof, startswith, endswith<br /><br /> name:<br /><br /> - ge, le, eq, ne, gt, lt : substringof, startswith, endswith|  
|$top|string|The number of entities to return.|  
|$skip|string|The number of entities to skip.|  
  
#### Request Body  
 None.  
  
### Responses  
  
#### 200 OK  
 A [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of the [Authorization Server](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#AuthorizationServer) entities for the specified API Management service instance.  
  
##  <a name="Get"></a> Get a specific authorization server  
 This operation returns the details of the authorization server specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/authorizationServers/{authsid}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|authsid|string|Authorization server identifier.|  
  
#### Request Headers  
 None.  
  
#### Query Parameters  
 None.  
  
#### Request Body  
 None.  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The response headers contain the following metatada about the authorization server.  
  
|Headers|||  
|-------------|-|-|  
|ETag|string|Current entity state version. Should be treated as opaque and used to make conditional HTTP requests.|  
  
 The response body contains the specified [Authorization Server](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#AuthorizationServer) entity.  
  
#### 404 Not Found  
 The specified authorization server does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="HEAD"></a> Get the metadata for a specific authorization server  
 This operation returns the metadata for the authorization server specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|HEAD|/authorizationServers/{authsid}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|authsid|string|Authorization server identifier.|  
  
#### Request Headers  
 None.  
  
#### Query Parameters  
 None.  
  
#### Request Body  
 None.  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The response headers contain the following metatada about the authorization server.  
  
|Headers|||  
|-------------|-|-|  
|ETag|string|Current entity state version. Should be treated as opaque and used to make conditional HTTP requests.|  
  
#### 404 Not Found  
 The specified authorization server does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="PUT"></a> Create a new authorization server  
 This operation creates a new authorization server.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PUT|/authorizationServers/{authsid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|authsid|string|Authorization server identifier. Must be unique in the current API Management service instance. Maximum length is 256 characters.|  
  
#### Request Headers  
 None.  
  
#### Query Parameters  
 None.  
  
#### Request body  
 The request body contains an [Authorization Server](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#AuthorizationServer) entity. For a complete list of eligible properties for this operation, see the [Authorization Server](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#AuthorizationServer) properties in the [Contract reference](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md).  
  
### Responses  
 This operation has the following responses.  
  
#### 201 Created  
 Authorization server was successfully registered.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 409 Conflict  
 Authorization server with the same identifier already exists.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="PATCH"></a> Update an authorization server  
 This operation updates the details of the authorization server specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PATCH|/authorizationServers/{authsid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|authsid|string|Authorization server identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the authorization server to update. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
#### Query Parameters  
 None.  
  
#### Request body  
 The request body contains an [Authorization Server](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#AuthorizationServer) entity. Only [Authorization Server](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#AuthorizationServer) properties being updated may be specified in the request body. For a complete list of eligible properties for this operation, see the [Authorization Server](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#AuthorizationServer) properties in the [Contract reference](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md).  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The authorization server settings were successfully updated.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="DELETE"></a> Delete an authorization server  
 This operation deletes the authorization server specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|DELETE|/authorizationServers/{authsid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|authsid|string|Authorization server identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the authorization server to delete. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
#### Query Parameters  
 None.  
  
#### Request body  
 None.  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The authorization server was successfully deleted.  
  
#### 400 Bad Request  
 Cannot delete authorization server because it is assigned to an operation.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified authorization server does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.
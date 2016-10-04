---
title: "Azure API Management REST API Backend entity"
ms.custom: na
ms.date: 2016-05-09
ms.prod: azure
ms.reviewer: na
ms.service: api-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 1bb37828-5694-468e-b3e9-4984abd6da49
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
# Azure API Management REST API Backend entity
The Backend entity in API Management represents a backend service that is configured to skip certification chain validation when using a self-signed certificate to test mutual certificate authentication. A typical usage scenario is as follows.  
  
-   An API is configured in API Management.  
  
-   The API is secured using [How to secure back-end services using client certificate authentication in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-howto-mutual-certificates/).  
  
-   During testing, you may want to use a self-signed certificate. To do so, use the [Create a backend](#PUT) operation to explicitly create a backend entity, configure the entity to reference your backend service, and set the `skipCertificateChainValidation` property to `true`.  
  
-   When testing is complete, you can either call the [Delete a backend](#DELETE) operation to delete the test configuration or you can call [Update a backend](#PATCH) and set `skipCertificateChainValidation` to `false`.  
  
 This topic describes how to manage backend services by using the API Management REST API.  
  
> [!NOTE]
>  For more information about working with the REST API, see the [API Management .NET REST API Sample](https://github.com/Azure/api-management-samples/tree/master/restApiDemo) and the [Getting Started with Azure API Management REST API](http://azure.microsoft.com/documentation/videos/getting-started-with-azure-api-management-rest-api/) video.  
  
## In this topic  
  
-   [Prerequisites](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#Prerequisites)  
  
-   [List backend services](../ApiManagementREST/Azure-API-Management-REST-API-Backend-entity.md#List)  
  
-   [Get a specific backend](../ApiManagementREST/Azure-API-Management-REST-API-Backend-entity.md#GET)  
  
-   [Get the metadata for a specific backend](../ApiManagementREST/Azure-API-Management-REST-API-Backend-entity.md#GetUserMetadata)  
  
-   [Create a backend](../ApiManagementREST/Azure-API-Management-REST-API-Backend-entity.md#PUT)  
  
-   [Update a backend](../ApiManagementREST/Azure-API-Management-REST-API-Backend-entity.md#PATCH)  
  
-   [Delete a backend](../ApiManagementREST/Azure-API-Management-REST-API-Backend-entity.md#DELETE)  
  
##  <a name="Prerequisites"></a> Prerequisites  
  
> [!IMPORTANT]
>  Before making any calls into the API Management REST API, please review the [Prerequisites](../ApiManagementREST/API-Management-REST.md#Prerequisites) section of the [API Management REST](../ApiManagementREST/API-Management-REST.md) guide. This specifies the necessary authentication, version parameters, supported media types, and other information required in order to successfully call the API Management REST API.  
  
##  <a name="List"></a> List backend services  
 This operation returns a collection of backend services in the specified service instance.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/backends|  
  
#### Request parameters  
 None.  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|You can filter the results using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported<br /><br /> id:<br /><br /> - ge, le, eq, ne, gt, lt: substringof, startswith, endswith<br /><br /> host:<br /><br /> - ge, le, eq, ne, gt, lt: substringof, startswith, endswith|  
|$top|string|The number of entities to return.|  
|$skip|string|The number of entities to skip.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 This operation returns a [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of [Backend](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Backend) entities.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="GET"></a> Get a specific backend  
 This operation returns the details of the backend specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/backends/{backendId}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|backendId|string|Backend identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The response headers contain the following metatada about the backend.  
  
|Headers|||  
|-------------|-|-|  
|ETag|string|Current entity state version. Should be treated as opaque and used to make conditional HTTP requests.|  
  
 The response body contains the specified [Backend](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Backend) entity.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified backend does not exist.  
  
##  <a name="GetUserMetadata"></a> Get the metadata for a specific backend  
 This operation returns the metadata for the backend specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|HEAD|/backends/{backendId}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|backendId|string|Backend identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The operation was successful.  
  
|Headers|||  
|-------------|-|-|  
|ETag|string|Current entity state version. Should be treated as opaque and used to make conditional HTTP requests.|  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not found  
 The specified backend does not exist.  
  
##  <a name="PUT"></a> Create a backend  
 This operation creates a new backend.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PUT|/backends/{backendId}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|backendId|string|Backend identifier. Must be unique in the current API Management service instance. Maximum length is 256 characters.|  
  
#### Request body  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|host|string|Host attribute of the backend. Host is a pure hostname without a port or suffix, for example `backend.contoso.com`. Must not be empty. Maximum length is 255 characters.|  
|skipCertificateChainValidation|boolean|Flag indicating whether SSL certificate chain validation should be skipped when using self-signed certificates for this backend host.|  
  
### Responses  
 This operation has the following responses.  
  
#### 201 Created  
 Backend was successfully created.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 409 Conflict  
 Backend with the same identifier already exists.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="PATCH"></a> Update a backend  
 This operation updates an existing backend.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PATCH|/backends/{backendId}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|backendId|string|Backend identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the backend to update. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
#### Request body  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|host|string|Host attribute of the backend. Host is a pure hostname without a port or suffix, for example `backend.contoso.com`. Must not be empty. Maximum length is 255 characters.|  
|skipCertificateChainValidation|boolean|Flag indicating whether SSL certificate chain validation should be skipped when using self-signed certificates for this backend host.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The existing backend was successfully updated.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the backend resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="DELETE"></a> Delete a backend  
 This operation deletes the specified backend.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|DELETE|/backends/{backendId}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|backendId|string|Backend identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the backend to delete. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The backend was successfully deleted.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the backend resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.
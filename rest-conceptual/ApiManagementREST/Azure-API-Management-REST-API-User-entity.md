---
title: "Azure API Management REST API User entity"
ms.custom: na
ms.date: 2016-05-09
ms.prod: azure
ms.reviewer: na
ms.service: api-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 9ac2756a-b563-45b4-9007-132fdb14c599
caps.latest.revision: 27
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
# Azure API Management REST API User entity
The User entity in API Management represents the developers that call the APIs of the products to which they are subscribed.  
  
 This topic describes how to manage users by using the API Management REST API. For more information about working with developer accounts in the publisher portal, see [How to manage developer accounts in Azure API Management](http://go.microsoft.com/fwlink/?LinkId=444488).  
  
 For more information about working with the REST API, see the [API Management .NET REST API Sample](https://github.com/Azure/api-management-samples/tree/master/restApiDemo) and the [Getting Started with Azure API Management REST API](http://azure.microsoft.com/documentation/videos/getting-started-with-azure-api-management-rest-api/) video.  
  
## In this topic  
  
-   [Prerequisites](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#Prerequisites)  
  
-   [List registered users](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#List)  
  
-   [Get a specific user](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#GetUser)  
  
-   [Get the metadata for a specific user](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#GetUserMetadata)  
  
-   [Create a new user](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#CreateUser)  
  
-   [Update a user](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#UpdateUser)  
  
-   [Delete a user](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#DeleteUser)  
  
-   [List developer groups associated with a user](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#ListGroups)  
  
-   [List subscriptions for a specific user](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#ListSubscriptions)  
  
-   [Get single sign-on URL for a user](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#SSO)  
  
##  <a name="Prerequisites"></a> Prerequisites  
  
> [!IMPORTANT]
>  Before making any calls into the API Management REST API, please review the [Prerequisites](../ApiManagementREST/API-Management-REST.md#Prerequisites) section of the [API Management REST](../ApiManagementREST/API-Management-REST.md) guide. This specifies the necessary authentication, version parameters, supported media types, and other information required in order to successfully call the API Management REST API.  
  
##  <a name="List"></a> List registered users  
 This operation returns a collection of registered users in the specified service instance.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/users|  
  
#### Request parameters  
 None.  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|You can filter the results using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported<br /><br /> id<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> firstName<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> lastName<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> email<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> state<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - N/A<br /><br /> registrationDate<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - N/A<br /><br /> note<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith|  
|$top|string|The number of entities to return.|  
|$skip|string|The number of entities to skip.|  
|expandGroups|boolean|When set to `true`, the response contains an array of groups to which the user belongs. The default is `false`.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 This operation returns a [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of [User](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#User) entities.  
  
##### Sample response body  
  
```json  
{  
  "value": [  
    {  
      "id": "/users/1",  
      "firstName": "Administrator",  
      "lastName": "",  
      "email": "Stephan.Denman@contoso.com",  
      "state": "active",  
      "registrationDate": "2014-08-05T17:06:32.733",  
      "note": null  
    },  
    {  
      "id": "/users/53e11e52ad662f0c74ab4e95",  
      "firstName": "Clayton",  
      "lastName": "Gragg",  
      "email": "Clayton.Gragg@contoso.com",  
      "state": "active",  
      "registrationDate": "2014-08-05T18:11:31.42",  
      "note": "He's a jolly good fellow."  
    }  
  ],  
  "count": 2,  
  "nextLink": null  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="GetUser"></a> Get a specific user  
 This operation returns the details of the user specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/users/{uid}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|uid|string|User identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The response headers contain the following metatada about the user.  
  
|Headers|||  
|-------------|-|-|  
|ETag|string|Current entity state version. Should be treated as opaque and used to make conditional HTTP requests.|  
  
 The response body contains the specified [User](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#User) entity.  
  
##### Sample response body  
  
```json  
{  
  "id": "/users/53e11e52ad662f0c74ab4e95",  
  "firstName": "Clayton",  
  "lastName": "Gragg",  
  "email": "Clayton.Gragg@contoso.com",  
  "state": "active",  
  "registrationDate": "2014-08-05T18:11:31.42”,  
  “note": “He's a jolly good fellow."  
}  
  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified user does not exist.  
  
##  <a name="GetUserMetadata"></a> Get the metadata for a specific user  
 This operation returns the metadata for the user specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|HEAD|/users/{uid}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|uid|string|User identifier.|  
  
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
 The specified user does not exist.  
  
##  <a name="CreateUser"></a> Create a new user  
 This operation creates a new user.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PUT|/users/{uid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|uid|string|User identifier. Must be unique in the current API Management service instance. Maximum length is 256 characters.|  
  
#### Request body  
 The request body contains a [User](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#User) entity. For a complete list of eligible properties for this operation, see the [User](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#User) properties in the [Contract reference](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md).  
  
```json  
{  
  "firstName": "Special",  
  "lastName": "Developer",  
  "email": "sd@contoso.com",  
  "password": "Passw0rd!"  
}  
```  
  
### Responses  
 This operation has the following responses.  
  
#### 201 Created  
 User was successfully created.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 409 Conflict  
 User with the same identifier already exists.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="UpdateUser"></a> Update a user  
 This operation updates the details of the user specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PATCH|/users/{uid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|uid|string|User identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the user to update. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
#### Request Body  
 The request body contains a [User](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#User) entity. Only [User](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#User) properties being updated may be specified in the request body. The following sample request updates the password for a user. For a complete list of eligible properties for this operation, see the [User](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#User) properties in the [Contract reference](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md).  
  
```json  
{  
  "password": "NewPassw0rd!"  
}  
```  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The user details were successfully updated.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified user doesn’t exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 405 Method Not Allowed  
 Administrator user cannot be modified.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the user resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="DeleteUser"></a> Delete a user  
 This operation deletes the specified user account.  
  
> [!NOTE]
>  If the user account has any associated subscriptions, this operation will fail with `400 Bad Request` unless the `deleteSubscriptions` query parameter is set to `true`.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|DELETE|/users/{uid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|uid|string|User identifier.|  
  
#### Query parameters  
  
||||  
|-|-|-|  
|Query Parameter|Type|Description|  
|deleteSubscriptions|boolean|Specify `true` to indicate that any subscriptions associated with this user should be deleted; otherwise `false`. If this query parameter is missing, the default is `false`.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the user to delete. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The user was successfully deleted.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
> [!NOTE]
>  If the user account has any associated subscriptions, this operation will fail with `400 Bad Request` unless the `deleteSubscriptions` query parameter is set to `true`.  
  
#### 405 Method Not Allowed  
 Administrator user cannot be deleted.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the user resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="ListGroups"></a> List developer groups associated with a user  
 This operations returns the developer groups associated with the specified user.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/users/{uid}/groups|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|uid|string|User identifier.|  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|You can filter the results using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported<br /><br /> id<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> name<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> description<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith|  
|$top|string|The number of entities to return.|  
|$skip|string|The number of entities to skip.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 This operation returns a [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of [Group](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Group) entities.  
  
##### Sample response body  
  
```json  
{  
  "value": [  
    {  
      "id": "/groups/53e10f187e888000b4020002",  
      "name": "Developers",  
      "description": "Developers is a built-in group. Its membership is managed by the system. Signed-in users fall into this group.",  
      "builtIn": true  
    },  
    {  
      "id": "/groups/53e11f14ad662f0c74ab4e96",  
      "name": "Partners",  
      "description": "This is a custom group for developers that are part of a few trusted partner organizations.",  
      "builtIn": false  
    }  
  ],  
  "count": 2,  
  "nextLink": null  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified user does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="ListSubscriptions"></a> List subscriptions for a specific user  
 This operations returns the subscriptions of the specified user.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/users/{uid}/subscriptions|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|uid|string|User identifier.|  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|You can filter the results using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported<br /><br /> id<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> primaryKey<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> secondaryKey<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> stateComment<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> userId<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> productId<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith|  
|$top|string|The number of entities to return.|  
|$skip|string|The number of entities to skip.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 This operation returns a [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of [Subscription](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Subscription) entities.  
  
##### Sample response body  
  
```json  
{  
  "value": [  
    {  
      "id": "/subscriptions/53e1208cad662f0c74ab4e97",  
      "userId": "/users/53e11e52ad662f0c74ab4e95",  
      "productId": "/products/53e10f187e888000b4060002",  
      "state": "active",  
      "createdDate": "2014-08-05T18:21:00.9",  
      "startDate": "2014-08-05T00:00:00",  
      "primaryKey": "5420878819a6413f81b397359ae61dd9",  
      "secondaryKey": "672b72e66ea4401ba4db4c486ea5701e"  
    }  
  ],  
  "count": 1,  
  "nextLink": null  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified user does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="SSO"></a> Get single sign-on URL for a user  
 This operation retrieves a redirection URL containing an authentication token for signing a given user into the developer portal.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|POST|/users/{uid}/generateSsoUrl|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|uid|string|User identifier.|  
  
#### Request body  
 None.  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The operation was successful.  
  
 The response body contains the single sign-on URL.  
  
##### Sample response body  
  
```json  
{  
  "value": "https://mytenant.portal.azure-api.net/signin-sso?token=..."  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The user doesn’t exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.
---
title: "Azure API Management REST API Group entity"
ms.custom: na
ms.date: 2016-05-09
ms.prod: azure
ms.reviewer: na
ms.service: api-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 8bd74256-fece-451d-b571-2c3cf929d635
caps.latest.revision: 23
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
# Azure API Management REST API Group entity
Groups are used to manage the visibility of products to developers. Each API Management service instance comes with the following immutable system groups whose membership is automatically managed by API Management.  
  
-   **Administrators** - Azure subscription administrators are members of this group.  
  
-   **Developers** - Authenticated developer portal users fall into this group.  
  
-   **Guests** - Unauthenticated developer portal users are placed into this group.  
  
 In addition to these system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants](https://azure.microsoft.com/documentation/articles/api-management-howto-aad/#how-to-add-an-external-azure-active-directory-group). Custom and external groups can be used alongside system groups in giving developers visibility and access to API products. For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access to the APIs from a product containing relevant APIs only. A user can be a member of more than one group.  
  
 This topic describes how to manage groups using the API Management REST API. For more information about working with groups in the publisher portal, see [How to create and use groups to manage developer accounts in Azure API Management](http://go.microsoft.com/fwlink/?LinkId=404000). For more information about adding external Azure Active Directory groups, see [How to add an external Azure Active Directory Group](http://azure.microsoft.com/documentation/articles/api-management-howto-aad/#how-to-add-an-external-azure-active-directory-group).  
  
 For more information about working with the REST API, see the [API Management .NET REST API Sample](https://github.com/Azure/api-management-samples/tree/master/restApiDemo) and the [Getting Started with Azure API Management REST API](http://azure.microsoft.com/documentation/videos/getting-started-with-azure-api-management-rest-api/) video.  
  
## In this topic  
  
-   [Prerequisites](../ApiManagementREST/Azure-API-Management-REST-API-Group-entity.md#Prerequisites)  
  
-   [Get a list of all groups](../ApiManagementREST/Azure-API-Management-REST-API-Group-entity.md#ListGroups)  
  
-   [Get a specific group](../ApiManagementREST/Azure-API-Management-REST-API-Group-entity.md#GetGroup)  
  
-   [Get the metadata for a specific group](../ApiManagementREST/Azure-API-Management-REST-API-Group-entity.md#GetGroupMetadata)  
  
-   [Create a new group](../ApiManagementREST/Azure-API-Management-REST-API-Group-entity.md#CreateGroup)  
  
-   [Update an existing group](../ApiManagementREST/Azure-API-Management-REST-API-Group-entity.md#UpdateGroup)  
  
-   [Delete a group](../ApiManagementREST/Azure-API-Management-REST-API-Group-entity.md#DeleteGroup)  
  
-   [List group members](../ApiManagementREST/Azure-API-Management-REST-API-Group-entity.md#ListGroupMembers)  
  
-   [Add a member to a group](../ApiManagementREST/Azure-API-Management-REST-API-Group-entity.md#AddMember)  
  
-   [Remove a member from a group](../ApiManagementREST/Azure-API-Management-REST-API-Group-entity.md#RemoveMember)  
  
-   [Check membership in a group](../ApiManagementREST/Azure-API-Management-REST-API-Group-entity.md#CheckMembership)  
  
##  <a name="Prerequisites"></a> Prerequisites  
  
> [!IMPORTANT]
>  Before making any calls into the API Management REST API, please review the [Prerequisites](../ApiManagementREST/API-Management-REST.md#Prerequisites) section of the [API Management REST](../ApiManagementREST/API-Management-REST.md) guide. This specifies the necessary authentication, version parameters, supported media types, and other information required in order to successfully call the API Management REST API.  
  
##  <a name="ListGroups"></a> Get a list of all groups  
 This operation returns a collection of groups defined within a service instance.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/groups|  
  
#### Request Parameters  
 None.  
  
#### Request Headers  
 None.  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|You can filter the results using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported<br /><br /> id:<br /><br /> - ge, le, eq, ne, gt, lt : substringof, startswith, endswith<br /><br /> name:<br /><br /> - ge, le, eq, ne, gt, lt : substringof, startswith, endswith<br /><br /> description:<br /><br /> - ge, le, eq, ne, gt, lt : substringof, startswith, endswith<br /><br /> type:<br /><br /> - eq, ne : N/A|  
|$top|string|The number of entities to return.|  
|$skip|string|The number of entities to skip.|  
  
#### Request Body  
 None.  
  
### Responses  
  
#### 200 OK  
 A [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of the [Group](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Group) entities for the specified API Management service instance.  
  
##### Sample response body  
  
```json  
{  
  "value": [  
    {  
      "id": "/groups/53c765632095310385020001",  
      "name": "Administrators",  
      "description": "Administrators is a built-in group. Its membership is managed by the system. Microsoft Azure subscription administrators fall into this group.",  
      "builtIn": true,  
      "type": "system",  
      "externalId": null  
    },  
    {  
      "id": "/groups/5500579df0be6b01208725f7",  
      "name": "Contoso 5 Developers (contoso5api.onmicrosoft.com)",  
      "description": "Contoso 5 Developers group",  
      "builtIn": false,  
      "type": "external",  
      "externalId": "aad://contoso5api.onmicrosoft.com/groups/1bab325a-1423-4643-d413-2f2ebbad3f4c"  
    },  
    {  
      "id": "/groups/54dced8af0be6b0ab4491415",  
      "name": "Partners",  
      "description": "This is a custom group for developers that are part of a few trusted partner organizations. ",  
      "builtIn": false,  
      "type": "custom",  
      "externalId": null  
    },  
    {  
      "id": "/groups/53c765632095310385020002",  
      "name": "Developers",  
      "description": "Developers is a built-in group. Its membership is managed by the system. Signed-in users fall into this group.",  
      "builtIn": true,  
      "type": "system",  
      "externalId": null  
    },  
    {  
      "id": "/groups/53c765632095310385020003",  
      "name": "Guests",  
      "description": "Guests is a built-in group. Its membership is managed by the system. Unauthenticated users visiting the developer portal fall into this group.",  
      "builtIn": true,  
      "type": "system",  
      "externalId": null  
    }  
  ],  
  "count": 5,  
  "nextLink": null  
}  
```  
  
##  <a name="GetGroup"></a> Get a specific group  
 This operation returns the details of the group specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/groups/{gid}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|gid|string|Group identifier.|  
  
#### Request Body  
 None.  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The response headers contain the following metatada about the group.  
  
|Headers|||  
|-------------|-|-|  
|ETag|string|Current entity state version. Should be treated as opaque and used to make conditional HTTP requests.|  
  
 The response body contains the specified [Group](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Group) entity.  
  
##### Sample response body  
  
```json  
{  
  "id": "/groups/54dced8af0be6b0ab4491415",  
  "name": "Partners",  
  "description": "This is a custom group for developers that are part of a few trusted partner organizations.",  
  "builtIn": false,  
   "type": "custom",  
   "externalId": null  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified group does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="GetGroupMetadata"></a> Get the metadata for a specific group  
 This operation returns the metadata for the group specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|HEAD|/groups/{gid}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|gid|string|Group identifier.|  
  
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
 The specified group does not exist.  
  
##  <a name="CreateGroup"></a> Create a new group  
 This operation creates a new group.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PUT|/groups/{gid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|gid|string|Group identifier for the new group. Must be unique in the current API Management service instance. Maximum length is 256 characters.|  
  
#### Request body  
 [Group](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Group)  
  
 The request body contains a [Group](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Group) entity. For a complete list of eligible properties for this operation, see the [Group](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Group) properties in the [Contract reference](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md).  
  
```json  
{  
  "name": "Partners",  
  "description": "This is a custom group for developers that are part of a few trusted partner organizations."  
}  
```  
  
### Responses  
 This operation has the following responses.  
  
#### 201 Created  
 Group was successfully created.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 409 Conflict  
 Group with the specified identifier already exists.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="UpdateGroup"></a> Update an existing group  
 This operation updates the details of the group specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PATCH|/groups/{gid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|gid|string|Group identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the group to update. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
#### Request Body  
 The request body contains a [Group](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Group) entity. Only [Group](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Group) properties being updated may be specified in the request body. The following sample request updates the description for a group. For a complete list of eligible properties for this operation, see the [Group](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Group) properties in the [Contract reference](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md).  
  
```json  
{  
  "description": "New group description."  
}  
```  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The group details were successfully updated.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified group doesn’t exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 405 Method Not Allowed  
 The specified group cannot be updated because it is a built-in group.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the group resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="DeleteGroup"></a> Delete a group  
 This operation deletes the specified group.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|DELETE|/groups/{gid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|gid|string|Group identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the group to delete. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The group was successfully deleted.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 405 Method Not Allowed  
 The specified group cannot be deleted because it is a built-in group.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="ListGroupMembers"></a> List group members  
 This operation lists the members of the group, specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/groups/{gid}/users|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|gid|string|Group identifier.|  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|You can filter the results using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported<br /><br /> id:<br /><br /> - ge, le, eq, ne, gt, lt : substringof, startswith, endswith<br /><br /> firstName:<br /><br /> - ge, le, eq, ne, gt, lt : substringof, startswith, endswith<br /><br /> lastName:<br /><br /> - ge, le, eq, ne, gt, lt : substringof, startswith, endswith<br /><br /> email:<br /><br /> - ge, le, eq, ne, gt, lt : substringof, startswith, endswith<br /><br /> registrationDate:<br /><br /> - ge, le, eq, ne, gt, lt : N/A<br /><br /> note:<br /><br /> - ge, le, eq, ne, gt, lt : substringof, startswith, endswith|  
|$top|string|The number of entities to return.|  
|$skip|string|The number of entities to skip.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 This operation returns a [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of [user](ABC) entities.  
  
##### Sample response body  
  
```json  
{  
  "value": [  
    {  
      "id": "/users/53e11e52ad662f0c74ab4e95",  
      "firstName": "Anton",  
      "lastName": "Babadjanov",  
      "email": "ab@babadjanov.org",  
      "state": "active",  
      "registrationDate": "2014-08-05T18:11:31.42"  
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
 The specified group does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="AddMember"></a> Add a member to a group  
 This operation adds a user to a group.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PUT|/groups/{gid}/users/{uid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|gid|string|Group identifier.|  
|uid|string|User identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 201 Created  
 The user was successfully added to the group.  
  
#### 204 No Content  
 The specified user is already a member of the specified group.  
  
#### 400 Bad Request  
 Request validation failed. This is typically caused by an invalid user identifier.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified group doesn’t exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 405 Method Not Allowed  
 Attempt was made to add a user to a built-in group. Built-in group membership is managed by the system.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="RemoveMember"></a> Remove a member from a group  
 This operation removes the specified user from the specified group.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|DELETE|/groups/{gid}/users/{uid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|gid|string|Group identifier.|  
|uid|string|User identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The user was successfully removed from the group.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified group does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 405 Method Not Allowed  
 Attempt was made to remove a user from a built-in group. Built-in group membership is managed by the system.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="CheckMembership"></a> Check membership in a group  
 This operation checks to see if a user is a member of the specified group.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|HEAD|/groups/{gid}/users/{uid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|gid|string|Group identifier.|  
|uid|string|User identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The user is a member of the specified group.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The user is not a member of the group or the group does not exist.
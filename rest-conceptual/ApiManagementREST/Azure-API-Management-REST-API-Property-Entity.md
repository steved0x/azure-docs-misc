---
title: "Azure API Management REST API Property Entity"
ms.custom: na
ms.date: 2016-05-09
ms.prod: azure
ms.reviewer: na
ms.service: api-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 16b8f92e-5f5d-4c5a-9b42-58eee08bee3f
caps.latest.revision: 8
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
# Azure API Management REST API Property Entity
API Management policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration. Policies are a collection of statements that are executed sequentially on the request or response of an API. Policy statements can be constructed using literal text values, policy expressions, and properties.   Each API Management service instance has a properties collection of key/value pairs that are global to the service instance. These properties can be used to manage constant string values across all API configuration and policies.  
  
 This topic describes how to manage properties using the API Management REST API. For more information about working with properties in the publisher portal, see [How to use properties in Azure API Management policies](http://azure.microsoft.com/documentation/articles/api-management-howto-properties/).  
  
 For more information about working with the REST API, see the [API Management .NET REST API Sample](https://github.com/Azure/api-management-samples/tree/master/restApiDemo) and the [Getting Started with Azure API Management REST API](http://azure.microsoft.com/documentation/videos/getting-started-with-azure-api-management-rest-api/) video.  
  
## In this topic  
  
-   [Prerequisites](#Prerequisites)  
  
-   [Get a list of all properties](#List)  
  
-   [Get a specific property](#Get)  
  
-   [Get the metadata for a specific property](#Head)  
  
-   [Create a new property](#Put)  
  
-   [Update an existing property](#Patch)  
  
-   [Delete a property](#Delete)  
  
##  <a name="Prerequisites"></a> Prerequisites  
  
> [!IMPORTANT]
>  Before making any calls into the API Management REST API, please review the [Prerequisites](../ApiManagementREST/API-Management-REST.md#Prerequisites) section of the [API Management REST](../ApiManagementREST/API-Management-REST.md) guide. This specifies the necessary authentication, version parameters, supported media types, and other information required in order to successfully call the API Management REST API.  
  
##  <a name="List"></a> Get a list of all properties  
 This operation returns a collection of properties defined within a service instance.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/properties|  
  
#### Request Parameters  
 None.  
  
#### Request Headers  
 None.  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|You can filter the results using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported<br /><br /> tags:<br /><br /> - ge, le, eq, ne, gt, lt: substringof, startswith, endswith<br /><br /> name:<br /><br /> - ge, le, eq, ne, gt, lt: substringof, startswith, endswith|  
|$top|string|The number of entities to return.|  
|$skip|string|The number of entities to skip.|  
  
#### Request Body  
 None.  
  
### Responses  
  
#### 200 OK  
 A [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of the [Property](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Property) entities for the specified API Management service instance.  
  
##### Sample response body  
  
```json  
{  
  "value": [  
    {  
      "id": "/properties/56c64b13848fb20d2c6c931f",  
      "name": "ContosoHeader",  
      "value": "TrackingId",  
      "tags": [  
        "Contoso"  
      ],  
      "secret": false  
    },  
    {  
      "id": "/properties/56c64b30848fb20d2c6c9320",  
      "name": "ContosoHeaderValue",  
      "value": "C3B179D1-3101-46A0-9905-C6DDA79B33AD",  
      "tags": [  
        "Contoso"  
      ],  
      "secret": true  
    },  
    {  
      "id": "/properties/56c64b42848fb20d2c6c9321",  
      "name": "ExpressionProperty",  
      "value": "@(DateTime.Now.ToString())",  
      "tags": [],  
      "secret": false  
    }  
  ],  
  "count": 3,  
  "nextLink": null  
}  
```  
  
##  <a name="Get"></a> Get a specific property  
 This operation returns the details of the property specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/properties/{propId}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|propId|string|Property identifier.|  
  
#### Request Body  
 None.  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The response headers contain the following metatada about the group.  
  
|Headers|||  
|-------------|-|-|  
|ETag|string|Current entity state version. Should be treated as opaque and used to make conditional HTTP requests.|  
  
 The response body contains the specified [Property](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Property) entity.  
  
##### Sample response body  
  
```json  
{  
  "id": "/properties/56c64b13848fb20d2c6c931f",  
  "name": "ContosoHeader",  
  "value": "TrackingId",  
  "tags": [  
    "Contoso"  
  ],  
  "secret": false  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified property does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="Head"></a> Get the metadata for a specific property  
 This operation returns the metadata for the property specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|HEAD|/properties/{propId}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|propId|string|Property identifier.|  
  
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
 The specified property does not exist.  
  
##  <a name="Put"></a> Create a new property  
 This operation creates a new property.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PUT|/properties/{propId}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|propId|string|Property identifier for the new property. Must be unique in the current API Management service instance. Maximum length is 256 characters.|  
  
#### Request body  
 The request body contains a [Property](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Property) entity. For a complete list of eligible properties for this operation, see the [Property](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Property) properties in the [Contract reference](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md).  
  
```json  
{  
  "name": "ContosoHeader",  
  "value": "TrackingId",  
  "tags": [  
    "Contoso"  
  ],  
  "secret": false  
}  
```  
  
### Responses  
 This operation has the following responses.  
  
#### 201 Created  
 Property was successfully created.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 409 Conflict  
 Property with the specified identifier already exists.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="Patch"></a> Update an existing property  
 This operation updates the details of the property specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PATCH|/properties/{propId}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|propId|string|Property identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the property to update. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
#### Request Body  
 The request body contains a [Property](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Property) entity. Only [Property](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Property) properties being updated may be specified in the request body. In this example, the tags are updated for the property. For a complete list of eligible properties for this operation, see the [Property](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Property) properties in the [Contract reference](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md).  
  
```json  
{  
   "tags": [  
    "Contoso", "Management"  
  ]  
}  
```  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The property details were successfully updated.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified property doesn’t exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the property resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="Delete"></a> Delete a property  
 This operation deletes the specified property.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|DELETE|/properties/{propId}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|propId|string|Group identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the property to delete. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The property was successfully deleted.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 405 Method Not Allowed  
 The specified property cannot be deleted because it is in use in a policy. You must remove all references to this property before it can be deleted.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.
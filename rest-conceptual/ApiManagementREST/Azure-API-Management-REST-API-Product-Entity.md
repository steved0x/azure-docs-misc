---
title: "Azure API Management REST API Product Entity"
ms.custom: na
ms.date: 2016-09-22
ms.prod: azure
ms.reviewer: na
ms.service: api-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: f426a139-1098-47dd-9ec1-1f0f00800ef9
caps.latest.revision: 30
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
# Azure API Management REST API Product Entity
The Product entity represents a product in API Management. Products include one or more APIs and their associated terms of use. Once a product is published, developers can subscribe to the product and begin to use the product’s APIs.  
  
 This topic describes how to manage products using the API Management REST API. For more information about working with products in the publisher portal, see [How create and publish a product in Azure API Management](http://go.microsoft.com/fwlink/?LinkId=404274) and [How create and configure advanced product settings in Azure API Management](http://go.microsoft.com/fwlink/?LinkId=404275).  
  
 For more information about working with the REST API, see the [API Management .NET REST API Sample](https://github.com/Azure/api-management-samples/tree/master/restApiDemo) and the [Getting Started with Azure API Management REST API](http://azure.microsoft.com/documentation/videos/getting-started-with-azure-api-management-rest-api/) video.  
  
## In this topic  
  
-   [Prerequisites](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md#Prerequisites)  
  
-   [Get a list of all products](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md#ListProducts)  
  
-   [Get a specific product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md#GetProduct)  
  
-   [Get the metadata for a specific product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md#GetProductMetadata)  
  
-   [Create a new product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md#CreateProduct)  
  
-   [Update a product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md#UpdateProduct)  
  
-   [Delete a product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md#DeleteProduct)  
  
-   [List APIs associated with a product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md#ListAPIs)  
  
-   [Check API membership in a product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md#CheckAPIMembership)  
  
-   [Add an API to a product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md#AddAPI)  
  
-   [Remove an API from a product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md#RemoveAPI)  
  
-   [List subscriptions to a product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md#ListSubscriptions)  
  
-   [Get policy configuration for a product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md#GetPolicy)  
  
-   [Check a product for attached policy configuration](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md#CheckPolicy)  
  
-   [Set policy configuration for a product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md#SetPolicy)  
  
-   [Remove policy configuration from a product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md#RemovePolicy)  
  
-   [List developer groups associated with a product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md#ListGroups)  
  
-   [Associate a developer group with a product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md#AddGroup)  
  
-   [Delete a developer group association with a product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md#RemoveGroup)  
  
##  <a name="Prerequisites"></a> Prerequisites  
  
> [!IMPORTANT]
>  Before making any calls into the API Management REST API, please review the [Prerequisites](../ApiManagementREST/API-Management-REST.md#Prerequisites) section of the [API Management REST](../ApiManagementREST/API-Management-REST.md) guide. This specifies the necessary authentication, version parameters, supported media types, and other information required in order to successfully call the API Management REST API.  
  
##  <a name="ListProducts"></a> Get a list of all products  
 This operation returns a collection of products in the specified service instance.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/products|  
  
#### Request Parameters  
 None.  
  
#### Request Headers  
 None.  
  
#### Request Body  
 None.  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|You can filter the results using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported<br /><br /> id<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> name<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> description<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> terms<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith|  
|$top|string|The number of entities to return.|  
|$skip|string|The number of entities to skip.|  
|expandGroups|boolean|When set to `true`, the response contains an array of groups that have visibility to the product. The default is `false`.|  
  
### Responses  
  
#### 200 OK  
 A [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of the [Product](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Product) entities for the specified API Management service instance.  
  
##### Sample response body with expandGroups=false  
  
```json  
{  
  "value": [  
    {  
      "id": "/products/53e10f187e888000b4060001",  
      "name": "Starter",  
      "description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
      "terms": "",  
      "subscriptionPeriod": {  
        "value": 15,  
        "interval": "day"  
      },  
      "notificationPeriod": {  
        "value": 12,  
        "interval": "day"  
      },  
      "subscriptionRequired": true,  
      "approvalRequired": false,  
      "subscriptionsLimit": null,  
      "state": "published"  
    },  
    {  
      "id": "/products/53e10f187e888000b4060002",  
      "name": "Unlimited",  
      "description": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
      "subscriptionRequired": true,  
      "approvalRequired": true,  
      "subscriptionsLimit": null,  
      "state": "published"  
    }  
  ],  
  "count": 2,  
  "nextLink": null  
}  
```  
  
##### Sample response body with expandGroups=true  
  
```json  
{  
  "value": [  
    {  
      "id": "/products/544d9a6d0fe876031c060001",  
      "name": "Starter",  
      "description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
      "terms": "",  
      "subscriptionRequired": true,  
      "approvalRequired": false,  
      "subscriptionsLimit": null,  
      "state": "published",  
      "groups": [  
        {  
          "id": "/groups/544d9a6d0fe876031c020001",  
          "name": "Administrators",  
          "description": "Administrators is a built-in group. Its membership is managed by the system. Microsoft Azure subscription administrators fall into this group.",  
          "builtIn": true  
        },  
        {  
          "id": "/groups/544d9a6d0fe876031c020002",  
          "name": "Developers",  
          "description": "Developers is a built-in group. Its membership is managed by the system. Signed-in users fall into this group.",  
          "builtIn": true  
        },  
        {  
          "id": "/groups/544d9a6d0fe876031c020003",  
          "name": "Guests",  
          "description": "Guests is a built-in group. Its membership is managed by the system. Unauthenticated users visiting the developer portal fall into this group.",  
          "builtIn": true  
        }  
      ]  
    },  
    {  
      "id": "/products/544d9a6d0fe876031c060002",  
      "name": "Unlimited",  
      "description": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
      "terms": null,  
      "subscriptionRequired": true,  
      "approvalRequired": true,  
      "subscriptionsLimit": null,  
      "state": "published",  
      "groups": [  
        {  
          "id": "/groups/544d9a6d0fe876031c020001",  
          "name": "Administrators",  
          "description": "Administrators is a built-in group. Its membership is managed by the system. Microsoft Azure subscription administrators fall into this group.",  
          "builtIn": true  
        },  
        {  
          "id": "/groups/544d9a6d0fe876031c020002",  
          "name": "Developers",  
          "description": "Developers is a built-in group. Its membership is managed by the system. Signed-in users fall into this group.",  
          "builtIn": true  
        },  
        {  
          "id": "/groups/544d9a6d0fe876031c020003",  
          "name": "Guests",  
          "description": "Guests is a built-in group. Its membership is managed by the system. Unauthenticated users visiting the developer portal fall into this group.",  
          "builtIn": true  
        }  
      ]  
    }  
  ],  
  "count": 2,  
  "nextLink": null  
}  
  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="GetProduct"></a> Get a specific product  
 This operation returns the details of the product specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/products/{pid}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|pid|string|Product identifier.|  
  
#### Request Body  
 None.  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The response headers contain the following metatada about the group.  
  
|Headers|||  
|-------------|-|-|  
|ETag|string|Current entity state version. Should be treated as opaque and used to make conditional HTTP requests.|  
  
 The response body contains the specified [Product](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Product) entity.  
  
##### Sample response body  
  
```json  
{  
  "id": "/products/53e10f187e888000b4060002",  
  "name": "Unlimited",  
  "description": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
  "subscriptionRequired": true,  
  "approvalRequired": true,  
  "subscriptionsLimit": null,  
  "state": "published"  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified product does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="GetProductMetadata"></a> Get the metadata for a specific product  
 This operation returns the metadata for the product specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|HEAD|/products/{pid}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|pid|string|Product identifier.|  
  
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
 The specified product does not exist.  
  
##  <a name="CreateProduct"></a> Create a new product  
 This operation creates a new product.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PUT|/products/{pid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|pid|string|Product identifier. Must be unique in the current API Management service instance. Maximum length is 256 characters.|  
  
#### Request body  
 [Product](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Product)  
  
 The request body contains a [Product](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Product) entity. For a complete list of eligible properties for this operation, see the [Product](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Product) properties in the [Contract reference](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md).  
  
```json  
{  
  "name": "Unlimited",  
  "description": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
  "subscriptionRequired": true,  
  "approvalRequired": true,  
  "subscriptionsLimit": null,  
  "state": "published"  
}  
```  
  
### Responses  
 This operation has the following responses.  
  
#### 201 Created  
 Product was successfully created.  
  
#### 400 Bad Request  
 Request validation failed. One cause for request validation to fail is if either one or both of the `approvalRequired` and `subscriptionLimit` properties are present in the request body along with the `subscriptionRequired` property set to `false`.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 409 Conflict  
 Product with the same identifier already exists.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="UpdateProduct"></a> Update a product  
 This operation updates the details of the group specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PATCH|/products/{pid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|pid|string|Product identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the product to update. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
#### Request Body  
 The request body contains a [Product](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Product) entity. Only [Product](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Product) properties being updated may be specified in the request body. In the following example, the product in unpublished. For a complete list of eligible properties for this operation, see the [Product](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Product) properties in the [Contract reference](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md).  
  
```json  
{  
    "state": "notPublished"  
}  
```  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The product details were successfully updated.  
  
#### 400 Bad Request  
 Request validation failed. One cause for request validation to fail is if either one or both of the `approvalRequired` and `subscriptionLimit` properties are present in the request body along with the `subscriptionRequired` property set to `false`.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified product doesn’t exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the product resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="DeleteProduct"></a> Delete a product  
 This operation deletes the specified product.  
  
> [!NOTE]
>  If the product has any associated subscriptions, this operation will fail with `400 Bad Request` unless the `deleteSubscriptions` query parameter is set to `true`.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|DELETE|/products/{pid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|pid|string|Product identifier.|  
  
#### Query parameters  
  
||||  
|-|-|-|  
|Query Parameter|Type|Description|  
|deleteSubscriptions|boolean|Specify `true` to indicate that any subscriptions associated with this product should be deleted; otherwise `false`. If this query parameter is missing, the default is `false`.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the product. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The product was successfully deleted.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
> [!NOTE]
>  If the product has any associated subscriptions, this operation will fail with `400 Bad Request` unless the `deleteSubscriptions` query parameter is set to `true`.  
  
#### 412 Precondition Failed  
 Returned if the product resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="ListAPIs"></a> List APIs associated with a product  
 This operation lists the APIs associated with a product.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/products/{pid}/apis|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|pid|string|Product identifier.|  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|You can filter the results using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported<br /><br /> id<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> name<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> description<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> serviceUrl<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> path<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith|  
|$top|string|The number of entities to return.|  
|$skip|string|The number of entities to skip.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 This operation returns a [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of [api](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#api) details.  
  
##### Sample response body  
  
```json  
{  
  "value": [  
    {  
      "id": "/apis/53e10f187e888000b4040001",  
      "name": "Echo API",  
      "serviceUrl": "http://echoapi.cloudapp.net/api",  
      "path": "echo"  
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
 The specified product does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="CheckAPIMembership"></a> Check API membership in a product  
 This operation determines whether the product includes the specified API.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|HEAD|/products/{pid}/apis/{aid}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|pid|string|Product identifier.|  
|aid|string|API identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The operation was successful.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not found  
 The specified product does not exist or the specified API is not part of the product.  
  
##  <a name="AddAPI"></a> Add an API to a product  
 This operation adds an API to the specified product.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PUT|/products/{pid}/apis/{aid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|pid|string|Product identifier.|  
|aid|string|API identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 201 Created  
 The API was successfully added to the product.  
  
#### 204 No Content  
 The specified API is already added to the product.  
  
#### 400 Bad Request  
 Request validation failed. This is typically caused by an invalid product or API id.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified product doesn’t exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="RemoveAPI"></a> Remove an API from a product  
 This operation removes the specified API from the specified product.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|DELETE|/products/{pid}/apis/{aid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|pid|string|Product identifier.|  
|aid|string|API identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The API was successfully removed from the product.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified product doesn’t exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="ListSubscriptions"></a> List subscriptions to a product  
 This operations returns the subscriptions to the specified product.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/products/{pid}/subscriptions|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|pid|string|Product identifier.|  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|You can filter the results using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported<br /><br /> id<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> primaryKey<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> secondaryKey<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> stateComment<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> userId<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> productId<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith|  
|$top|string|The number of entities to return.|  
|$skip|string|The number of entities to skip.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 This operation returns a [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of [Subscription](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#subscription) entities.  
  
##### Sample response body  
  
```json  
{  
  "value": [  
    {  
      "id": "/subscriptions/53e10f187e888000b4070002",  
      "userId": "/users/1",  
      "productId": "/products/53e10f187e888000b4060002",  
      "state": "active",  
      "createdDate": "2014-08-05T17:06:32.777",  
      "primaryKey": "b5c68549265e49bfa45a5823afb8b8a9",  
      "secondaryKey": "b0f1cf5e4345425881c951397aec373f"  
    },  
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
  "count": 2,  
  "nextLink": null  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified product does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="GetPolicy"></a> Get policy configuration for a product  
 This operation returns the policy configuration for the specified product.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/products/{pid}/policy|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|pid|string|Product identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The response headers contain the following metatada about the group.  
  
|Headers|||  
|-------------|-|-|  
|ETag|string|Current entity state version.|  
  
 The response body contains a [Policy](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Policy) response type. The media type for this response is `application/vnd.ms-azure-apim.policy+xml`.  
  
##### Sample response body  
  
```xml  
<policies>  
    <inbound>  
        <rate-limit calls="5" renewal-period="60" />  
        <quota calls="100" renewal-period="604800" />  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified product does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="CheckPolicy"></a> Check a product for attached policy configuration  
 This operation determines if policy configuration is attached to the specified product.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|HEAD|/products/{pid}/policy|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|pid|string|Product identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 Policy configuration is attached to the specified product.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not found  
 The specified product does not exist or there is no policy configuration attached.  
  
##  <a name="SetPolicy"></a> Set policy configuration for a product  
 This operation sets the policy configuration for the specified product.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PUT|/products/{pid}/policy|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|pid|string|Product identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the product to update. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
|Content-Type|Possible values are `application/vnd.ms-azure-apim.policy+xml` and `application/vnd.ms-azure-apim.policy.raw+xml`.<br /><br /> When using `application/vnd.ms-azure-apim.policy+xml`, expressions contained within the policy must be XML-escaped.<br /><br /> When using `application/vnd.ms-azure-apim.policy.raw+xml` no escaping is necessary.|  
  
#### Request Body  
 The request body is the desired [Policy](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Policy) representation.  
  
```xml  
<policies>  
    <inbound>  
        <rate-limit calls="5" renewal-period="60" />  
        <quota calls="100" renewal-period="604800" />  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### Responses  
 This operation has the following responses.  
  
#### 201 Created  
 The policy configuration was successfully attached to the product.  
  
#### 204 No Content  
 The existing policy configuration was successfully updated.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified product does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the policy resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="RemovePolicy"></a> Remove policy configuration from a product  
 This operation removes the policy configuration for the specified product.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|DELETE|/products/{pid}/policy|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|pid|string|Product identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the product. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The policy configuration was successfully removed from the product.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified product does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the product resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="ListGroups"></a> List developer groups associated with a product  
 This operations returns the developer groups associated with the specified product.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/products/{pid}/groups|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|pid|string|Product identifier.|  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|You can filter the results using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported<br /><br /> id<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> name<br /><br /> - eq, ne<br /><br /> - substringof, startswith, endswith<br /><br /> description<br /><br /> - eq, ne<br /><br /> - substringof, startswith, endswith|  
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
      "externalId": "aad://contoso5api.onmicrosoft.com/groups/12ad42b1-592f-4664-a77b4250-2f2e82579f4c"  
    },  
    {  
      "id": "/groups/53c765632095310385020002",  
      "name": "Developers",  
      "description": "Developers is a built-in group. Its membership is managed by the system. Signed-in usersfall into this group.",  
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
    },  
    {  
      "id": "/groups/54dced8af0be6b0ab4491415",  
      "name": "Partners",  
      "description": "This is a custom group for developers that are part of a few trusted partner organizations.",  
      "builtIn": false,  
      "type": "custom",  
      "externalId": null  
    }  
  ],  
  "count": 5,  
  "nextLink": null  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified product does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="AddGroup"></a> Associate a developer group with a product  
 This operation associates the specified developer group with the specified product.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PUT|/products/{pid}/groups/{gid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|pid|string|Product identifier.|  
|gid|string|Group identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 201 Created  
 The group was successfully associated with the product.  
  
#### 204 No Content  
 The specified group is already associated with the product.  
  
#### 400 Bad Request  
 Request validation failed. This is typically caused by an invalid product or group id.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="RemoveGroup"></a> Delete a developer group association with a product  
 This operation removes the association between the specified group and product.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|DELETE|/products/{pid}/groups/{gid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|pid|string|Product identifier.|  
|gid|string|Group identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The group was successfully disassociated with the product.  
  
#### 400 Bad Request  
 The specified product does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.
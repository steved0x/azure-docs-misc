---
title: "Azure API Management REST API Subscription entity"
ms.custom: na
ms.date: 2016-05-09
ms.prod: azure
ms.reviewer: na
ms.service: api-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 12b2a652-117e-4b9a-b281-f2323d8b6202
caps.latest.revision: 19
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
# Azure API Management REST API Subscription entity
The Subscription entity represents the association between a user and a product in API Management. Products contain one or more APIs, and once a product is published, developers can subscribe to the product and begin to use the product’s APIs.  
  
 This topic describes how to manage subscriptions using the API Management REST API.  
  
> [!NOTE]
>  For more information about working with products and subscriptions in the publisher portal, see [How create and publish a product in Azure API Management](http://go.microsoft.com/fwlink/?LinkId=404274) and [How create and configure advanced product settings in Azure API Management](http://go.microsoft.com/fwlink/?LinkId=404275).  
  
 For more information about working with the REST API, see the [API Management .NET REST API Sample](https://github.com/Azure/api-management-samples/tree/master/restApiDemo) and the [Getting Started with Azure API Management REST API](http://azure.microsoft.com/documentation/videos/getting-started-with-azure-api-management-rest-api/) video.  
  
## In this topic  
  
-   [Prerequisites](../ApiManagementREST/Azure-API-Management-REST-API-Subscription-entity.md#Prerequisites)  
  
-   [Get a list of all subscriptions](../ApiManagementREST/Azure-API-Management-REST-API-Subscription-entity.md#ListSubscriptions)  
  
-   [Get subscription details](../ApiManagementREST/Azure-API-Management-REST-API-Subscription-entity.md#GetSubscription)  
  
-   [Get the metadata for a subscription](../ApiManagementREST/Azure-API-Management-REST-API-Subscription-entity.md#GetMetadata)  
  
-   [Subscribe a user to a product](../ApiManagementREST/Azure-API-Management-REST-API-Subscription-entity.md#SubscribeProduct)  
  
-   [Update subscription details](../ApiManagementREST/Azure-API-Management-REST-API-Subscription-entity.md#UpdateSubscription)  
  
-   [Delete a subscription](../ApiManagementREST/Azure-API-Management-REST-API-Subscription-entity.md#DeleteSubscription)  
  
-   [Regenerate subscription primary key](../ApiManagementREST/Azure-API-Management-REST-API-Subscription-entity.md#RegeneratePrimaryKey)  
  
-   [Regenerate subscription secondary key](../ApiManagementREST/Azure-API-Management-REST-API-Subscription-entity.md#RegenrateSecondaryKey)  
  
> [!NOTE]
>  To return all the subscriptions for a specific product, see [List subscriptions to a product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md#ListSubscriptions) in the [Product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md) reference documentation.  
  
##  <a name="Prerequisites"></a> Prerequisites  
  
> [!IMPORTANT]
>  Before making any calls into the API Management REST API, please review the [Prerequisites](../ApiManagementREST/API-Management-REST.md#Prerequisites) section of the [API Management REST](../ApiManagementREST/API-Management-REST.md) guide. This specifies the necessary authentication, version parameters, supported media types, and other information required in order to successfully call the API Management REST API.  
  
##  <a name="ListSubscriptions"></a> Get a list of all subscriptions  
 This operation returns a collection of subscriptions in the specified service instance.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/subscriptions|  
  
#### Request Parameters  
 None.  
  
#### Request Headers  
 None.  
  
#### Request Body  
 None.  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|You can filter the results using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported<br /><br /> id<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> stateComment<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> userId<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith<br /><br /> productId<br /><br /> - ge, le, eq, ne, gt, lt<br /><br /> - substringof, startswith, endswith|  
|$top|string|The number of entities to return.|  
|$skip|string|The number of entities to skip.|  
  
### Responses  
  
#### 200 OK  
 A [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of the [Subscription](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Subscription) entities for the specified API Management service instance.  
  
##### Sample response body  
  
```json  
{  
  "value": [  
    {  
      "id": "/subscriptions/53c765632095310385070001",  
      "userId": "/users/1",  
      "productId": "/products/53c765632095310385060001",  
      "name": null,  
      "state": "active",  
      "createdDate": "2014-05-19T14:05:54.707",  
      "startDate": null,  
      "expirationDate": null,  
      "endDate": null,  
      "notificationDate": null,  
      "primaryKey": "5f7f411234a44a68a2ea71062d271a59",  
      "secondaryKey": "98cf2f23221a4e123bca922adcf3f8de",  
      "stateComment": null  
    },  
    {  
      "id": "/subscriptions/53c765632095310385070002",  
      "userId": "/users/1",  
      "productId": "/products/53c765632095310385060002",  
      "name": null,  
      "state": "active",  
      "createdDate": "2014-05-19T14:05:54.713",  
      "startDate": null,  
      "expirationDate": null,  
      "endDate": null,  
      "notificationDate": null,  
      "primaryKey": "96da3775321a4b718dcea6a8adb70b27",  
      "secondaryKey": "aa8cba6326fc4b22b602b8464d96c92b",  
      "stateComment": null  
    },  
    {  
      "id": "/subscriptions/53c765632095310385070003",  
      "userId": "/users/1",  
      "productId": "/products/53c765632095310385060003",  
      "name": null,  
      "state": "active",  
      "createdDate": "2014-05-19T14:29:44.267",  
      "startDate": "2014-05-19T00:00:00",  
      "expirationDate": null,  
      "endDate": null,  
      "notificationDate": null,  
      "primaryKey": "e14ec3123246457b9bc81027466138c8",  
      "secondaryKey": "37b8c0aabc0c4c548481923c83228e11",  
      "stateComment": null  
    },  
    {  
      "id": "/subscriptions/54762a7ff0be6b1360b2628e",  
      "userId": "/users/53cff61af0be6b0a8ca83c79",  
      "productId": "/products/53c765632095310385060001",  
      "name": "Developer access #1",  
      "state": "cancelled",  
      "createdDate": "2014-11-26T19:31:12.927",  
      "startDate": "2014-11-26T00:00:00",  
      "expirationDate": "2014-12-11T00:00:00",  
      "endDate": "2015-05-22T00:00:00",  
      "notificationDate": "2014-11-29T00:00:00",  
      "primaryKey": "bef123a3035f4bb3b099261171a5bff8",  
      "secondaryKey": "ecae345663c54534be34df9e6b38bdb3",  
      "stateComment": null  
    }  
  ],  
  "count": 4,  
  "nextLink": null  
}  
  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="GetSubscription"></a> Get subscription details  
 This operation returns the details of the specified subscription.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/subscriptions/{sid}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|sid|string|Subscription identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The response headers contain the following metadata about the entity.  
  
|Headers|||  
|-------------|-|-|  
|ETag|string|Current entity state version. Should be treated as opaque and used to make conditional HTTP requests.|  
  
 The response body contains the specified [Subscription](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Subscription) entity.  
  
##### Sample response body  
  
```json  
{  
"id": "/subscriptions/53c765632095310385070001",  
"userId": "/users/1",  
"productId": "/products/53c765632095310385060001",  
"name": null,  
"state": "active",  
"createdDate": "2014-05-19T14:05:54.707",  
"startDate": null,  
"expirationDate": null,  
"endDate": null,  
"notificationDate": null,  
"primaryKey": "5f7f411234a44a68a2ea71062d271a59",  
"secondaryKey": "98cf2f23221a4e123bca922adcf3f8de",  
"stateComment": null  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified subscription does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="GetMetadata"></a> Get the metadata for a subscription  
 This operation retrieves the metadata for the subscription specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|HEAD|/subscriptions/{sid}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|sid|string|Subscription identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The operation was successful.  
  
|Headers|||  
|-------------|-|-|  
|ETag|string|Current entity state version|  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not found  
 The specified subscription does not exist.  
  
##  <a name="SubscribeProduct"></a> Subscribe a user to a product  
 This operation subscribes the specified user to the specified product.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PUT|/subscriptions/{sid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|sid|string|Subscription identifier. The identifier must be unique in the current API Management service instance.|  
  
#### Request body  
 The request body contains a [Subscription](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Subscription) entity. For a complete list of eligible properties for this operation, see the [Subscription](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Subscription) properties in the [Contract reference](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md).  
  
```json  
{  
"userId": "/users/1",  
"productId": "/products/53c765632095310385060001",  
"name": "My subscription,  
"state": "active"  
}  
```  
  
### Responses  
 This operation has the following responses.  
  
#### 201 Created  
 The user was successfully subscribed to the product.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 409 Conflict  
 Subscription with the same identifier already exists.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="UpdateSubscription"></a> Update subscription details  
 This operation updates the details of a subscription.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PATCH|/subscriptions/{sid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|sid|string|Subscription identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the subscription to update. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
#### Request Body  
 The request body contains a [Subscription](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Subscription) entity. Only [Subscription](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Subscription) properties being updated may be specified in the request body. For a complete list of eligible properties for this operation, see the [Subscription](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Subscription) properties in the [Contract reference](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md).  
  
```json  
{  
"state": "suspended"  
}  
```  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The subscription details were successfully updated.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified subscription doesn’t exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="DeleteSubscription"></a> Delete a subscription  
 This operation deletes the specified subscription.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|DELETE|/subscriptions/{sid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|sid|string|Subscription identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the subscription to delete. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The subscription was successfully deleted.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="RegeneratePrimaryKey"></a> Regenerate subscription primary key  
 This operation regenerates the primary key for the specified subscription.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|POST|/subscriptions/{sid}/regeneratePrimaryKey|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|sid|string|Subscription identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The primary key was successfully regenerated.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not found  
 The specified subscription does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 409 Conflict  
 The operation is not allowed due to the current subscription state.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="RegenrateSecondaryKey"></a> Regenerate subscription secondary key  
 This operation regenerates the secondary key for the specified subscription.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|POST|/subscriptions/{sid}/regenerateSecondaryKey|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|sid|string|Subscription identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The secondary key was successfully regenerated.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not found  
 The specified subscription does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 409 Conflict  
 The operation is not allowed due to the current subscription state.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.
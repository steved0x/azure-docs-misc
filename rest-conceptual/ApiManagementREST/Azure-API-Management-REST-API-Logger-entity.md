---
title: "Azure API Management REST API Logger entity"
ms.custom: na
ms.date: 2016-05-09
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 267af3ea-73ac-4483-93ce-462bd162b7c8
caps.latest.revision: 10
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
# Azure API Management REST API Logger entity
The Logger entity in API Management represents an event sink that you can use to log API Management events. Currently the Logger entity supports logging API Management events to [Azure Event Hubs](http://azure.microsoft.com/services/event-hubs/).  
  
 This topic describes how to manage loggers by using the API Management REST API.  
  
> [!NOTE]
>  For a step-by-step guide on configuring an event hub and logging events, see [How to log API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).  
>   
>  For more information about working with the REST API, see the [API Management .NET REST API Sample](https://github.com/Azure/api-management-samples/tree/master/restApiDemo) and the [Getting Started with Azure API Management REST API](http://azure.microsoft.com/documentation/videos/getting-started-with-azure-api-management-rest-api/) video.  
  
## In this topic  
  
-   [Prerequisites](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#Prerequisites)  
  
-   [List loggers](../ApiManagementREST/Azure-API-Management-REST-API-Logger-entity.md#List)  
  
-   [Get a specific logger](../ApiManagementREST/Azure-API-Management-REST-API-Logger-entity.md#GET)  
  
-   [Get the metadata for a specific logger](../ApiManagementREST/Azure-API-Management-REST-API-Logger-entity.md#HEAD)  
  
-   [Create a logger](../ApiManagementREST/Azure-API-Management-REST-API-Logger-entity.md#PUT)  
  
-   [Update a logger](../ApiManagementREST/Azure-API-Management-REST-API-Logger-entity.md#PATCH)  
  
-   [Delete a logger](../ApiManagementREST/Azure-API-Management-REST-API-Logger-entity.md#DELETE)  
  
##  <a name="Prerequisites"></a> Prerequisites  
  
> [!IMPORTANT]
>  Before making any calls into the API Management REST API, please review the [Prerequisites](../ApiManagementREST/API-Management-REST.md#Prerequisites) section of the [API Management REST](../ApiManagementREST/API-Management-REST.md) guide. This specifies the necessary authentication, version parameters, supported media types, and other information required in order to successfully call the API Management REST API.  
  
##  <a name="List"></a> List loggers  
 This operation returns a collection of loggers in the specified service instance.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/loggers|  
  
#### Request parameters  
 None.  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|You can filter the results using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported<br /><br /> id:<br /><br /> - ge, le, eq, ne, gt, lt : substringof, startswith, endswith<br /><br /> type:<br /><br /> - ge, le, eq, ne, gt, lt : substringof, startswith, endswith|  
|$top|string|The number of entities to return.|  
|$skip|string|The number of entities to skip.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 This operation returns a [collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of [Logger](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Logger) entities.  
  
##### Sample response body  
  
```json  
{  
  "value": [  
    {  
      "id": "/loggers/123456",  
      "type": "azureEventHub",  
      "description": "Sample description"  
    },  
    {  
      "id": "/loggers/contoso",  
      "type": "azureEventHub",  
      "description": "Sample description"  
    },  
    {  
      "id": "/loggers/contosodemo",  
      "type": "azureEventHub",  
      "description": "Sample description"  
    },  
    {  
      "id": "/loggers/contosologger",  
      "type": "azureEventHub",  
      "description": "Sample description"  
    }  
  ],  
  "count": 7,  
  "nextLink": null  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="GET"></a> Get a specific logger  
 This operation returns the details of the logger specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/loggers/{loggerId}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|loggerId|string|Logger identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The response headers contain the following metatada about the logger.  
  
|Headers|||  
|-------------|-|-|  
|ETag|string|Current entity state version. Should be treated as opaque and used to make conditional HTTP requests.|  
  
 The response body contains the specified [Logger](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Logger) entity.  
  
##### Sample response body  
  
```json  
  
{  
    "id": "/loggers/123",  
    "type": "azureEventHub",  
    "description": "This is my test event hub"  
}  
  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified logger does not exist.  
  
##  <a name="HEAD"></a> Get the metadata for a specific logger  
 This operation returns the metadata for the logger specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|HEAD|/loggers/{loggerId}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|loggerId|string|Logger identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The operation was successful.  
  
|Headers|||  
|-------------|-|-|  
|ETag|string|Current entity state version. Should be treated as opaque and used to make conditional HTTP requests.|  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not found  
 The specified logger does not exist.  
  
##  <a name="PUT"></a> Create a logger  
 This operation creates a new logger.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PUT|/loggers/{loggerId}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|loggerId|string|Logger identifier. Must be unique in the current API Management service instance. Maximum length is 256 characters.|  
  
#### Request body  
 The request body contains a [Logger](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Logger) entity. For a complete list of eligible properties for this operation, see the [Logger](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Logger) properties in the [Contract reference](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md).  
  
```json  
{  
  "type": "AzureEventHub",  
  "description": "Sample description",  
  "credentials": {  
    "name": "apim",  
    "connectionString": "Endpoint=sb://contoso-ns.servicebus.windows.net/;SharedAccessKeyName=Sender;SharedAccessKey=..."  
  }  
}  
```  
  
### Responses  
 This operation has the following responses.  
  
#### 201 Created  
 Logger was successfully created.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 409 Conflict  
 Logger with the same identifier already exists.  
  
 The response body contains an [error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="PATCH"></a> Update a logger  
 This operation updates an existing logger.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PATCH|/loggers/{loggerId}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|loggerId|string|Logger identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the logger to update. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
#### Request body  
 The request body contains a [Logger](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Logger) entity. Only properties being updated may be included in the request body. For a complete list of eligible properties for this operation, see the [Logger](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Logger) properties in the [Contract reference](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md).  
  
```json  
{  
   "description": "Updated description"  
}  
```  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The existing logger was successfully updated.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the logger resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="DELETE"></a> Delete a logger  
 This operation deletes the specified logger.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|DELETE|/loggers/{loggerId}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|loggerId|string|Logger identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the logger to delete. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The logger was successfully deleted.  
  
#### 400 Bad Request  
 The logger cannot be deleted because it is being used by one or more policies.  
  
 The response body contains an [error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the logger resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.
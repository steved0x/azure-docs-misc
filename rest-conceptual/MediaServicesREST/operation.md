---
title: "Operation"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: efaa0faf-4072-4054-bbda-f3963feb4ca8
caps.latest.revision: 11
author: "Juliako"
ms.author: "juliako"
manager: "erikre"
translation.priority.mt: 
  - "de-de"
  - "es-es"
  - "fr-fr"
  - "it-it"
  - "ja-jp"
  - "ko-kr"
  - "pt-br"
  - "ru-ru"
  - "zh-cn"
  - "zh-tw"
---
# Operation
Represents the current state of a long-running operation. Examples of long-running operations include starting, stopping, and deleting an Origin.  
  
 This topic gives an overview of the `Operation` entity and also demonstrates how to execute various operations with the Media Services REST API.  
  
-   [Operation Entity Properties](#operation_properties)  
  
-   [Query Operations](#query_operations)  
  
-   [Operation Error Codes](#error_codes)  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://msdn.microsoft.com/en-us/42ae6204-93bc-4797-bf40-1c68512cfb73).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
##  <a name="operation_properties"></a> Operation Entity Properties  
  
|`Property`|Type|Description|  
|----------------|----------|-----------------|  
|`Id`<br /><br /> Read only.|String|The operation ID, assigned by Media Services on creation of an operation. The format is:<br /><br /> `nb:opid:UUID:<GUID>`.|  
|`ErrorCode`<br /><br /> Read only.|String|The error code of the failed operation. For information on possible error codes, see, [Operation Error Codes](#error_codes).|  
|`ErrorMessage`<br /><br /> Read only.|String|The detailed error message of the failed operation.|  
|`State`<br /><br /> Read only.|String|The current state. Possible values include:<br /><br /> -   Succeeded<br />-   Failed<br />-   InProgress|  
|`TargetEntityId`<br /><br /> Read only.|String|The ID of the target of the action.|  
  
##  <a name="query_operations"></a> Query Operations  
 Queries the specified operation.  
  
|Method|Request URI|HTTP version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/api/Operations(‘*OperationId*’)|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
GET api/Operations('nb:opid:UUID:ab66eff9-8945-4323-9f91-d257a695899b') HTTP/1.1  
MaxDataServiceVersion: 3.0;NetFx  
Content-Type: application/json;odata=minimalmetadata  
Accept: application/json;odata=minimalmetadata  
Authorization: Bearer <token value>  
x-ms-version: 2.11  
Host: <redirected host URI>  
Content-Length: 0  
  
```  
  
 If successful, a **200 OK** status code is returned along with a status message in the response body, as shown in the following example.  
  
### Sample Response  
  
```  
HTTP/1.1 200 OK  
Cache-Control: no-cache  
Content-Length: 280  
Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8  
Server: Microsoft-IIS/7.5  
request-id: c3f3501a-8563-4cff-8aeb-66f68f9bdb8b  
x-ms-request-id: c3f3501a-8563-4cff-8aeb-66f68f9bdb8b  
X-Content-Type-Options: nosniff  
DataServiceVersion: 3.0;  
X-Powered-By: ASP.NET  
Date: Wed, 15 Jan 2014 19:31:13 GMT  
  
{"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Operations/@Element","Id":"nb:opid:UUID:ab66eff9-8945-4323-9f91-d257a695899b","State":"Succeeded","TargetEntityId":"nb:chid:UUID:1e518dbc-91ef-4044-a8bd-d20769dae833","ErrorCode":null,"ErrorMessage":null}  
```  
  
###  <a name="error_codes"></a> Operation Error Codes  
 Operation error codes are listed here.  
  
|Error Code|Description|  
|----------------|-----------------|  
|BadRequest|Sent when no other error is applicable, or the exact error is unknown.|  
|InsufficientCapacity|The data center has insufficient capacity.|  
|InternalError|Unexpected errors occurred from the service.|  
|InvalidIdentifierFormat|The entity ID format is invalid.|  
|InvalidOperation|The request is invalid in the entity’s current state.|  
|InvalidResourceName|The specified Origin name is invalid.|  
|OperationInProgress|Another operation is already in progress on the specified entity.|  
|OperationNotFound|The operation record is not found for the specified operation ID. The operation may have been removed after a time span, or the ID is wrong.|  
|ResourceNameTaken|Trying to create a new Origin with a name that is already in use.|  
|ResourceNotFound|The specified resource is not found.|  
|ExceededResourceQuota|The request exceeds the resource quota limit.|  
|Timeout|The asynchronous operation has timed out.|  
|DeleteNotAllowedOnDefaultOrigin|You tried to delete the default Origin.|  
|SettingsUpdateInProgress|An update is already in progress.|
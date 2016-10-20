---
title: "Delete a Gateway"
ms.custom: na
ms.date: 2016-07-21
ms.prod: azure
ms.reviewer: na
ms.service: data-factory
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 38b89452-73e7-45b2-af8e-f73fcb367b83
caps.latest.revision: 7
author: spelluru
manager: jhubbard
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
# Delete a Gateway
  The Delete Gateway operation deletes the specific gateway.  
  
## Request  
 The Delete Gateway request may be constructed as follows (HTTPS is recommended):  
  
|**HTTP Verb**|**Request URI**|**HTTP Version**|  
|-|-|-|  
|DELETE|https://management.azure.com/subscriptions/<SubscriptionID\>/resourcegroups/<ResourceGroupName\>/providers/Microsoft.DataFactory/datafactories/<DataFactoryName\>/gateways/<GatewayName\>?api-version=<Api-Version>|HTTP/1.1|  
  
### URI Parameters  
  
|**URI Parameter**|**Required**|**Description**|  
|-|-|-|  
|SubscriptionID|Yes|Your Azure subscription ID.|  
|ResourceGroupName|Yes|A unique name for the resource group that hosts your Azure data factory.|  
|DataFactoryName|Yes|Name for the data factory that you want to create your gateway in.|  
|GatewayName|Yes|Name of gateway you want to create.|  
|Api-Version|Yes|Specifies the version of the protocol used to make this request.|  
  
### Request Headers  
 The following table describes the request headers.  
  
|**Request Header**|**Required**|**Description**|  
|-|-|-|  
|x-ms-client-request-id|Yes|The operation id for this request.|  
  
### Request Body  
 None.  
  
## Response  
 The response includes an HTTP status code, a set of response headers, and a response body.  
  
### Status Code  
  
-   200 (OK) - if the request was completed successfully.  
  
-   400 (Bad Request) - if the request body fails validation.  
  
-   404 (NotFound) - if the subscription or resource group does not exist.  
  
-   412 (Precondition Failed) - if the condition specified by If-Match header failed.  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|**Response Header**|**Description**|  
|-|-|  
|x-ms-request-id|A unique identifier for the current operation, service generated.|  
|x-ms-ratelimit-remaining-subscription-writes|The remaining limit for current subscription.|  
|x-ms-correlation-request-id|Specifies the tracing correlation Id for the request. The resource provider must log this so that end-to-end requests can be correlated across Azure.|  
|x-ms-routing-request-id|Location+DateTime+correlation-request-ID|  
  
### Response Body  
 None.  
  
## Sample Request and Response  
 Example URI:  
  
```  
DELETE: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/adf/providers/Microsoft.DataFactory/datafactories/test/gateways/gatewaytest?api-version=2014-12-01-preview  
```  
  
 The request is sent with the following headers.  
  
```  
  
x-ms-client-request-id: 00000000-0000-0000-0000-000000000000  
  
```  
  
 After the request has been sent, the following response is returned.  
  
```  
  
Status Code:  
OK   
  
Headers:  
Pragma                        : no-cache  
x-ms-request-id               : 00000000-1111-1111-1111-000000000000  
x-ms-ratelimit-remaining-subscription-writes: 11999  
x-ms-correlation-request-id   : 00000000-1111-2222-1111-000000000000  
x-ms-routing-request-id       : WESTUS:20141203T213044Z: 00000000-1111-2222-1111-000000000000  
Strict-Transport-Security     : max-age=31536000; includeSubDomains  
Cache-Control                 : no-cache  
Date                          : Wed, 03 Dec 2014 21:30:44 GMT  
Server                        : Microsoft-IIS/8.5  
X-Powered-By                  : ASP.NET  
  
```  
  
  
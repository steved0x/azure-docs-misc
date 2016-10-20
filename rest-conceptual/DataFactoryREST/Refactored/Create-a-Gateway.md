---
title: "Create a Gateway"
ms.custom: na
ms.date: 2016-07-21
ms.prod: azure
ms.reviewer: na
ms.service: data-factory
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: dda9f6cf-1dd8-4e8d-ae9c-9bf40174d22f
caps.latest.revision: 9
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
# Create a Gateway
  The Create or Update Gateway operation creates a new gateway, or updates an existing gateway.  
  
## Request  
 The Create or Update Gateway request may be constructed as follows (HTTPS is recommended):  
  
|**HTTP Verb**|**Request URI**|**HTTP Version**|  
|-|-|-|  
|PUT|https://management.azure.com/subscriptions/<SubscriptionID\>/resourcegroups/<ResourceGroupName\>/providers/Microsoft.DataFactory/datafactories/<DataFactoryName\>/gateways/<GatewayName\>?api-version=<Api-Version>|HTTP/1.1|  
  
### URI Parameters  
  
|**URI Parameter**|**Required**|**Description**|  
|-|-|-|  
|SubscriptionID|Yes|Your Azure subscription ID.|  
|ResourceGroupName|Yes|A unique name for the resource group that hosts your Azure data factory.|  
|DataFactoryName|Yes|Name for the data factory that you want to create your gateway in.|  
|GatewayName|Yes|Name of gateway you want to create|  
|Api-Version|Yes|Specifies the version of the protocol used to make this request.|  
  
### Request Headers  
 The following table describes the request headers.  
  
|Request Header|Required|Description|  
|-|-|-|  
|x-ms-client-request-id|Yes|The operation id for this request.|  
  
### Request Body  
 The format of the request body is as follows.  
  
```  
  
{  
    "name": <name>,  
    "properties": {  
        "description": <description>  
    }  
}  
  
```  
  
 The following table describes the elements of the request body.  
  
|**Element Name**|**Required**|**Description**|  
|-|-|-|  
|name|Yes|Name of the gateway.|  
|description|No|Description of the gateway.|  
  
## Response  
 The response includes an HTTP status code, a set of response headers, and a response body.  
  
### Status Code  
  
-   200 (OK) - if the request completed successfully.  
  
-   202 (Accepted) - if the request was accepted.  
  
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
  
```  
  
{  
    "location": <location>,  
    "name": <name>,  
    "properties": {  
        "key": <key>,  
        "description": <description>,  
        "hostServiceUri": <hostServiceUri>,  
        "dataFactoryName": <dataFactoryName>,  
        "status": <status>,  
        "versionStatus": <versionStatus>,  
        "provisioningState": <provisioningState>,  
        "version": <version>,  
        "createTime": <createTime>,  
        "registerTime": <registerTime>,  
        "lastConnectTime": <lastConnectTime>,  
        "expiryTime": <expiryTime>  
    }  
}  
```  
  
 The following table describes the elements of the response body.  
  
|**Element Name**|**Description**|  
|-|-|  
|name|Name of the gateway.|  
|location|Location of the gateway.|  
|key|Key of the gateway used for registration.|  
|description|Description of the gateway.|  
|hostServiceUri|Uri for the host machine of the gateway|  
|dataFactoryName|Name of the data factory which the gateway belongs to.|  
|status|Status of the gateway. Values can be Online, Offline or NeedRegistration.|  
|versionStatus|Status of the gateway version. Values can be UpToDate, Expiring, Expired, NewVersionAvailable and None.|  
|provisioningState|Specifies the current provisioning state of the linked service. When a linked service is successfully created, the value of the element is **Succeeded**.|  
|version|Version of the gateway|  
|createTime|The time at which the gateway was created.|  
|registerTime|The time at which the gateway was registered.|  
|expiryTime|The time at which the gateway will expire.|  
|lastConnectTime|The time at which the gateway was connection for the last time.|  
  
## Sample Request and Response  
 Example URI:  
  
```  
PUT: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/adf/providers/Microsoft.DataFactory/datafactories/test/gateways/gatewaytest?api-version=2015-10-01  
```  
  
 The request is sent with the following headers.  
  
```  
x-ms-client-request-id: 00000000-0000-0000-0000-000000000000  
```  
  
 And with the following body.  
  
```  
  
{  
    "name": "gatewaytest",  
    "properties": {  
        "description": "test description."  
    }  
}  
  
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
  
 The response includes the following XML body.  
  
```  
  
{  
    "location": "West US",  
    "name": "gatewaytest",  
    "properties": {  
        "key": "ADF#066b1a89-e84f-47a4-a784-a753b2e06623@21a6600e-6a83-4734-9a7a-b2a6b791b129@317515fd-a26a-4a08-a2f5-c13fb49b3851@wu#11gTEsN4o12bfYN26qbjlJMgihOlX7hyYAmrPwtLCRU=",  
        "description": "test description.",  
        "hostServiceUri": null,  
        "dataFactoryName": "test",  
        "status": "NeedRegistration",  
        "versionStatus": "None",  
        "provisioningState": "Succeeded",  
        "version": null,  
        "createTime": "2015-12-18T07:04:13.00664Z",  
        "registerTime": null,  
        "lastConnectTime": null,  
        "expiryTime": null  
    }  
}  
  
```  
  
  
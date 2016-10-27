---
title: "Media Services Operations REST"
ms.custom: ""
ms.date: "2016-03-08"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f7b363f7-4c14-4b4b-ac68-6b8bf23ee3ba
caps.latest.revision: 9
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
# Media Services Operations REST
> [!NOTE]
>  It is now recommended to use  the Azure Resource Manager (ARM) REST API endpoints, as described in [Media Services Management API Reference](../Topic/Media%20Services%20Management%20API%20Reference.md).  
  
 The Service Management API includes Operations on Media Services. This section demonstrates how to create requests and receive responses using Media Services Management REST API.  
  
## Request  
 The REST endpoint only supports HTTPS. The request is made against an URL in the format of https://endpoint/ (optionally with additional URL segments and/or URL query string). A request includes a set of request headers, and optionally a request body (for POST, PUT, GET request).  
  
### Request Headers  
 The `x-ms-version` request header value must be specified in the format YYYY-MM-DD. The current version of Media Services management operations is `2011-10-01`.  
  
```  
Request Headers:  
x-ms-version: 2011-10-01  
```  
  
|Header|Required|Remarks|Valid Values|  
|------------|--------------|-------------|------------------|  
|x-ms-version|Yes|Indicates the API version. Alternatively, request can use api-version.|2011-10-01|  
|Content-Type|No|Required for request that has request body.|application/xml or application/json|  
|Charset|No|Indicates what character sets are acceptable for the response. If omitted, server uses UTF-8.|See HTTP Headers reference for all charsets.|  
|Content-Length|No|The length of the request body in bytes. Required for request that has request body.|N/A|  
  
### Request Body  
 For a POST, PUT request, there is a request body. The request body has to be in the format indicated by the Content-Type header.  
  
## Response  
 A response includes an HTTP status code, a set of response headers, and optionally a response body (for non-204 response).  
  
### Response Headers  
  
|Header|Always Present|Remarks|Possible Values|  
|------------|--------------------|-------------|---------------------|  
|x-ms-request-id|Yes|An id assigned by server for tracking the request.|N/A|  
|WWW-Authenticate|No|The error message about why the authentication failed.|N/A|  
|X-AspNet-Version|Yes|Indicates the version of AspNet.|4.0.30319|  
|Date|Yes|Server time at which the processing the request finished.|See HTTP Headers reference for DateTime format.|  
|Content-Length|No|The length of the response body in bytes. Only present if there is a response body.|N/A|  
|Content-Type|No|The format of the response body according to the client’s `Accept` header (application/xml by default). Only present if there is a response body.|application/xml application/json|  
  
### Response Body  
 Response with non-204 (No Content) status code will have a response body. In this case, the response will have Content-Length and Content-Type header. The format of the body will be either XML or JSON depending on the `Accept` header in the request. If the Accept header is not specified in the request, server returns XML response body.  
  
## In This Section  
 [List Available Regions](../MediaServicesOperations_RESTAPI/list-available-regions.md)  
  
 [List Media Services Accounts](../MediaServicesOperations_RESTAPI/list-media-services-accounts.md)  
  
 [Create Media Services Account](../MediaServicesOperations_RESTAPI/create-media-services-account.md)  
  
 [Delete Media Services Account](../MediaServicesOperations_RESTAPI/delete-media-services-account.md)  
  
 [Get Media Services Account Details](../MediaServicesOperations_RESTAPI/get-media-services-account-details.md)  
  
 [List Storage Accounts](../MediaServicesOperations_RESTAPI/list-storage-accounts--media-services-.md)  
  
 [Update Storage Account Key](../MediaServicesOperations_RESTAPI/update-storage-account-key--media-services-.md)  
  
 [Regenerate Media Services Primary Account Key](../MediaServicesOperations_RESTAPI/regenerate-media-services-primary-account-key.md)  
  
 [Regenerate Media Services Secondary Account Key](../MediaServicesOperations_RESTAPI/regenerate-media-services-secondary-account-key.md)  
  
 [Media Services Management Error Codes](../MediaServicesOperations_RESTAPI/media-services-management-error-codes.md)
---
title: "API Management policies"
ms.custom: na
ms.date: 2016-08-29
ms.prod: azure
ms.reviewer: na
ms.service: api-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 1cc460cb-8e67-41aa-bc76-bbafc1892798
caps.latest.revision: 26
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
# API Management policies
This section provides a reference for the following API Management policies. For information on adding and configuring policies, see [Policies in API Management](https://azure.microsoft.com/documentation/articles/api-management-howto-policies/).  
  
 Policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration. Policies are a collection of Statements that are executed sequentially on the request or response of an API. Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer. Many more policies are available out of the box.  
  
 Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise. Some policies such as the [Control flow](../templates/API-Management-advanced-policies.md#choose) and [Set variable](../templates/API-Management-advanced-policies.md#set-variable) policies are based on policy expressions. For more information, see [Advanced policies](../templates/API-Management-advanced-policies.md#AdvancedPolicies) and [Policy expressions](../templates/API-Management-policy-expressions.md).  
  
##  <a name="ProxyPolicies"></a> Policies  
  
-   [Access restriction policies](../templates/API-Management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   [Check HTTP header](../templates/API-Management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.  
  
    -   [Limit call rate by subscription](../templates/API-Management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.  
  
    -   [Limit call rate by key](../templates/API-Management-access-restriction-policies.md#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.  
  
    -   [Restrict caller IPs](../templates/API-Management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.  
  
    -   [Set usage quota by subscription](../templates/API-Management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.  
  
    -   [Set usage quota by key](../templates/API-Management-access-restriction-policies.md#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.  
  
    -   [Validate JWT](../templates/API-Management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.  
  
-   [Advanced policies](../templates/API-Management-advanced-policies.md#AdvancedPolicies)  
  
    -   [Control flow](../templates/API-Management-advanced-policies.md#choose) - Conditionally applies policy statements based on the evaluation of Boolean expressions.  
  
    -   [Forward request](../templates/API-Management-advanced-policies.md#ForwardRequest) - Forwards the request to the backend service.  
  
    -   [Log to Event Hub](../templates/API-Management-advanced-policies.md#log-to-eventhub) - Sends messages in the specified format to a message target defined by a [Logger](../rest-conceptual/Azure-API-Management-REST-API-Logger-entity.md) entity.  
  
    -   [Retry](../templates/API-Management-advanced-policies.md#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met. Execution will repeat at the specified time intervals and up to the specified retry count.  
  
    -   [Return response](../templates/API-Management-advanced-policies.md#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.  
  
    -   [Send one way request](../templates/API-Management-advanced-policies.md#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.  
  
    -   [Send request](../templates/API-Management-advanced-policies.md#SendRequest) - Sends a request to the specified URL.  
  
    -   [Set variable](../templates/API-Management-advanced-policies.md#set-variable) - Persist a value in a named context variable for later access.  
  
    -   [Set request method](../templates/API-Management-advanced-policies.md#SetRequestMethod) - Allows you to change the HTTP method for a request.  
  
    -   [Set status code](../templates/API-Management-advanced-policies.md#SetStatus) - Changes the HTTP status code to the specified value.  
  
    -   [Trace](../templates/API-Management-advanced-policies.md#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.  
  
    -   [Wait](../templates/API-Management-advanced-policies.md#Wait) - Waits for enclosed [Send request](../templates/API-Management-advanced-policies.md#SendRequest), [Get value from cache](../templates/API-Management-caching-policies.md#GetFromCacheByKey), or [Control flow](../templates/API-Management-advanced-policies.md#choose) policies to complete before proceeding.  
  
-   [Authentication policies](../templates/API-Management-authentication-policies.md#AuthenticationPolicies)  
  
    -   [Authenticate with Basic](../templates/API-Management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.  
  
    -   [Authenticate with client certificate](../templates/API-Management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.  
  
-   [Caching policies](../templates/API-Management-caching-policies.md#CachingPolicies)  
  
    -   [Get from cache](../templates/API-Management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached response when available.  
  
    -   [Store to cache](../templates/API-Management-caching-policies.md#StoreToCache) - Caches response according to the specified cache control configuration.  
  
    -   [Get value from cache](../templates/API-Management-caching-policies.md#GetFromCacheByKey) - Retrieve a cached item by key.  
  
    -   [Store value in cache](../templates/API-Management-caching-policies.md#StoreToCacheByKey) - Store an item in the cache by key.  
  
    -   [Remove value from cache](../templates/API-Management-caching-policies.md#RemoveCacheByKey) - Remove an item in the cache by key.  
  
-   [Cross domain policies](../templates/API-Management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   [Allow cross-domain calls](../templates/API-Management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.  
  
    -   [CORS](../templates/API-Management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.  
  
    -   [JSONP](../templates/API-Management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.  
  
-   [Transformation policies](../templates/API-Management-transformation-policies.md#TransformationPolicies)  
  
    -   [Convert JSON to XML](../templates/API-Management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.  
  
    -   [Convert XML to JSON](../templates/API-Management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.  
  
    -   [Find and replace string in body](../templates/API-Management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.  
  
    -   [Mask URLs in content](../templates/API-Management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.  
  
    -   [Set backend service](../templates/API-Management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.  
  
    -   [Set body](../templates/API-Management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.  
  
    -   [Set HTTP header](../templates/API-Management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.  
  
    -   [Set query string parameter](../templates/API-Management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.  
  
    -   [Rewrite URL](../templates/API-Management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.  
  
    -   [Transform XML using an XSLT](../templates/API-Management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.  
  
## See Also  
 [Policy expressions](../templates/API-Management-policy-expressions.md)
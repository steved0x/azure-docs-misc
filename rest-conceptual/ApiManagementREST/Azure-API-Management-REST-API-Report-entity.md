---
title: "Azure API Management REST API Report entity"
ms.custom: na
ms.date: 2016-08-26
ms.prod: azure
ms.reviewer: na
ms.service: api-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 29839440-57b3-4165-83a8-8cc7f9b24967
caps.latest.revision: 17
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
# Azure API Management REST API Report entity
This topic describes how to retrieve reports using the API Management REST API.  
  
 For more information about working with the REST API, see the [API Management .NET REST API Sample](https://github.com/Azure/api-management-samples/tree/master/restApiDemo) and the [Getting Started with Azure API Management REST API](http://azure.microsoft.com/documentation/videos/getting-started-with-azure-api-management-rest-api/) video.  
  
## In this topic  
  
-   [Prerequisites](../ApiManagementREST/Azure-API-Management-REST-API-Report-entity.md#Prerequisites)  
  
-   [Report entity properties](../ApiManagementREST/Azure-API-Management-REST-API-Report-entity.md#Report)  
  
-   [Get metrics over a period of time](../ApiManagementREST/Azure-API-Management-REST-API-Report-entity.md#ReportByTime)  
  
-   [Get metrics aggregated by geographical region](../ApiManagementREST/Azure-API-Management-REST-API-Report-entity.md#ReportByGeo)  
  
-   [Get metrics aggregated by user](../ApiManagementREST/Azure-API-Management-REST-API-Report-entity.md#ReportByUser)  
  
-   [Get metrics aggregated by product](../ApiManagementREST/Azure-API-Management-REST-API-Report-entity.md#ReportByProduct)  
  
-   [Get metrics aggregated by API](../ApiManagementREST/Azure-API-Management-REST-API-Report-entity.md#ReportByAPI)  
  
-   [Get metrics aggregated by operation](../ApiManagementREST/Azure-API-Management-REST-API-Report-entity.md#ReportByOperation)  
  
-   [Get metrics aggregated by subscription](../ApiManagementREST/Azure-API-Management-REST-API-Report-entity.md#ReportBySubscription)  
  
-   [Get request log entries](../ApiManagementREST/Azure-API-Management-REST-API-Report-entity.md#ReportByRequest)  
  
##  <a name="Prerequisites"></a> Prerequisites  
  
> [!IMPORTANT]
>  Before making any calls into the API Management REST API, please review the [Prerequisites](../ApiManagementREST/API-Management-REST.md#Prerequisites) section of the [API Management REST](../ApiManagementREST/API-Management-REST.md) guide. This specifies the necessary authentication, version parameters, supported media types, and other information required in order to successfully call the API Management REST API.  
  
 Each of the following report types support different `$filter` parameter expression operand combinations which are listed in the **Query Parameters** section for each report type. If a `$filter` parameter expression operand combination is invalid, a `400 Bad Request` response code is returned.  
  
 When specifying id-based operands in `$filter` parameter expressions, make sure to use the actual id rather than resource URL. For example, to filter on `/apis/1234567890` use `apiId eq '1234567890'`.  
  
> [!IMPORTANT]
>  Note that only the `and` operator is supported when combining filter parameters.  
  
##  <a name="Report"></a> Report entity properties  
 The full report entity has the following properties. Each report operation described below returns a subset of the full entity. See the documentation for individual operations for details.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|name|string|Depending on the report endpoint this property specifies product, API, operation, subscription, or developer name.|  
|timestamp|dateTime|Start of reporting interval presented in this entry, in ISO 8601 format: `2014-06-24T16:25:00Z`.|  
|interval|string|Period of time over which the data presented in this entity was aggregated, in ISO 8601 format: `P500DT3H10M15.304S`.|  
|country|string|Country to which this data entity is related.|  
|region|string|Country region to which this entity is related (US only).|  
|zip|string|Zip code to which this entity is related (US only).|  
|userId|string|[User](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#User) identifier.|  
|productId|string|[Product](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Product) identifier.|  
|apiId|string|[API](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#API) identifier.|  
|operationId|string|[Operation](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Operation) identifier.|  
|apiRegion|string|Azure region where the gateway that processed this request is located.|  
|subscriptionId|string|[Subscription](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Subscription) identifier.|  
|callCountSuccess|integer|Number of successful calls.|  
|callCountBlocked|integer|Number of calls blocked due to invalid credentials.|  
|callCountFailed|integer|Number of calls failed due to gateway or backend errors.|  
|callCountOther|integer|Number of calls that didn't fall into any of the previous categories.|  
|callCountTotal|integer|Total number of calls.|  
|bandwidth|number|Total bandwidth consumed.|  
|cacheHitCount|integer|Number of times content was served from cache.|  
|cacheMissCount|integer|Number of times content was obtained from the backend.|  
|apiTimeAvg|double|Average time it took to process a request.|  
|apiTimeMin|double|Minimum time it took to process a request.|  
|apiTimeMax|double|Maximum time it took to process a request.|  
|serviceTimeAvg|double|Average time it took to process a request on the backend.|  
|serviceTimeMin|double|Minimum time it took to process a request on the backend.|  
|serviceTimeMax|double|Maximum time it took to process a request on the backend.|  
  
##  <a name="Request"></a> Request entity properties  
 The full request entity has the following properties. It is used by the [Get request log entries](../ApiManagementREST/Azure-API-Management-REST-API-Report-entity.md#ReportByRequest) operation.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|timestamp|dateTime|The date and time when this request was received by the gateway in ISO 8601 format: `2014-06-24T16:25:00Z`.|  
|method|string|The HTTP method associated with this request.|  
|url|string|The full URL associated with this request.|  
|ipAddress|string|The client IP address associated with this request.|  
|requestSize|integer|The size of this request.|  
|apiId|string|[API](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#API) identifier.|  
|operationId|string|[Operation](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Operation) identifier.|  
|productId|string|[Product](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Product) identifier.|  
|subscriptionId|string|[Subscription](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Subscription) identifier.|  
|userId|string|[User](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#User) identifier.|  
|apiRegion|string|Azure region where the gateway that processed this request is located.|  
|apiTime|double|The total time it took to process this request.|  
|serviceTime|double|The time it took to forward this request to the backend and get the response back.|  
|responseSize|integer|The size of the response returned by the gateway.|  
|cache|string|Specifies if response cache was involved in generating the response. If the value is `none`, the cache was not used. If the value is `hit`, cached response was returned. If the value is `miss`, the cache was used but lookup resulted in a miss and request was fullfilled by the backend.|  
|backendResponseCode|integer|The HTTP status code received by the gateway as a result of forwarding this request to the backend.|  
|responseCode|integer|The HTTP status code returned by the gateway.|  
  
##  <a name="ReportByTime"></a> Get metrics over a period of time  
 This operation returns metrics covering the specified time period.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/reports/byTime|  
  
#### Request Parameters  
 None.  
  
#### Request Headers  
  
|Request Header|Description|  
|--------------------|-----------------|  
|Accept|`Accept` can be set to `text/csv` or `application/json`. If `Accept` is not set the default is `application/json`.|  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|Filter using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported. This parameter is required and must include a `timestamp` for the call to be successful.<br /><br /> timestamp:<br /><br /> - ge,le: The start and end of the reporting period, for example `$filter=timestamp ge datetime'2014-10-07T00:00:00' and timestamp le datetime'2014-10-14T00:00:00'`. If `le` is omitted the current date and time is used for the end of the reporting period. You must specify a starting date and time for `ge`.<br /><br /> apiRegion:<br /><br /> - eq: Azure region where the gateway that processed this request is located.<br /><br /> userId:<br /><br /> - eq: User identifier.<br /><br /> productId:<br /><br /> - eq: Product identifier.<br /><br /> apiId:<br /><br /> - eq: API identifier.<br /><br /> operationId:<br /><br /> - eq: Operation identifier.<br /><br /> subscriptionId:<br /><br /> - eq: Subscription identifier.|  
|interval|string|Period of time over which the data presented in this entity was aggregated, in ISO 8601 format: `P500DT3H10M15.304S`. The minimum `interval` is fifteen minutes, and `interval` must be in even fifteen minute increments; otherwise a `400 Bad Request` error is returned.<br /><br /> This parameter is required.|  
  
 This report supports the following `$filter` parameter expression operand combinations.  
  
-   API  
  
-   API and operation  
  
-   Product  
  
-   Subscription  
  
-   User  
  
-   User and API  
  
-   User and API and operation  
  
-   User and product  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 This operation returns a [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of [Report](../ApiManagementREST/Azure-API-Management-REST-API-Report-entity.md#Report) records in `application/json` format, or the report record details in `text/csv` format.  
  
> [!NOTE]
>  For this report, the following fields are returned.  
>   
>  -   timestamp  
> -   interval  
> -   callCountSuccess  
> -   callCountBlocked  
> -   callCountFailed  
> -   callCountOther  
> -   bandwidth  
> -   cacheHitsCount  
> -   cacheMissCount  
> -   apiTimeAvg  
> -   apiTimeMin  
> -   apiTimeMax  
> -   serviceTimeAvg  
> -   serviceTimeMin  
> -   serviceTimeMax  
>   
>  All other fields in the response contain default values.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="ReportByGeo"></a> Get metrics aggregated by geographical region  
 This operation returns metrics aggregated by geographical region.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/reports/byGeo|  
  
#### Request Parameters  
 None.  
  
#### Request Headers  
  
|Request Header|Description|  
|--------------------|-----------------|  
|Accept|`Accept` can be set to `text/csv` or `application/json`. If `Accept` is not set the default is `application/json`.|  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|Filter using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported. This parameter is required and must include a `timestamp` for the call to be successful.<br /><br /> timestamp:<br /><br /> - ge,le: The start and end of the reporting period, for example `$filter=timestamp ge datetime'2014-10-07T00:00:00' and timestamp le datetime'2014-10-14T00:00:00'`. If `le` is omitted the current date and time is used for the end of the reporting period. You must specify a starting date and time for `ge`.<br /><br /> apiRegion:<br /><br /> - eq: Azure region where the gateway that processed this request is located.<br /><br /> userId:<br /><br /> - eq: User identifier.<br /><br /> productId:<br /><br /> - eq: Product identifier.<br /><br /> apiId:<br /><br /> - eq: API identifier.<br /><br /> operationId:<br /><br /> - eq: Operation identifier.<br /><br /> subscriptionId:<br /><br /> - eq: Subscription identifier.|  
  
 This report supports the following `$filter` parameter expression operand combinations.  
  
-   API  
  
-   API and operation  
  
-   Product  
  
-   Subscription  
  
-   User  
  
-   User and API  
  
-   User and API and operation  
  
-   User and product  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 This operation returns a [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of [Report](../ApiManagementREST/Azure-API-Management-REST-API-Report-entity.md#Report) records in `application/json` format, or the report record details in `text/csv` format.  
  
> [!NOTE]
>  For this report, the following fields are returned.  
>   
>  -   country  
> -   region  
> -   zip  
> -   callCountSuccess  
> -   callCountBlocked  
> -   callCountFailed  
> -   callCountOther  
> -   bandwidth  
> -   cacheHitsCount  
> -   cacheMissCount  
> -   apiTimeAvg  
> -   apiTimeMin  
> -   apiTimeMax  
> -   serviceTimeAvg  
> -   serviceTimeMin  
> -   serviceTimeMax  
>   
>  All other fields in the response contain default values.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="ReportByUser"></a> Get metrics aggregated by user  
 This operation returns metrics aggregated by user.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/reports/byUser|  
  
#### Request Parameters  
 None.  
  
#### Request Headers  
  
|Request Header|Description|  
|--------------------|-----------------|  
|Accept|`Accept` can be set to `text/csv` or `application/json`. If `Accept` is not set the default is `application/json`.|  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|Filter using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported. This parameter is required and must include a `timestamp` for the call to be successful.<br /><br /> timestamp:<br /><br /> - ge,le: The start and end of the reporting period, for example `$filter=timestamp ge datetime'2014-10-07T00:00:00' and timestamp le datetime'2014-10-14T00:00:00'`. If `le` is omitted the current date and time is used for the end of the reporting period. You must specify a starting date and time for `ge`.<br /><br /> userId:<br /><br /> - eq: User identifier.<br /><br /> apiRegion:<br /><br /> - eq: Azure region where the gateway that processed this request is located..<br /><br /> productId:<br /><br /> - eq: Product identifier.<br /><br /> apiId:<br /><br /> - eq: API identifier.<br /><br /> operationId:<br /><br /> - eq: Operation identifier.<br /><br /> subscriptionId:<br /><br /> - eq: Subscription identifier.|  
|$top|string|Number of records to return.|  
|$skip|string|Number of records to skip.|  
|$orderby|string|OData [order by query](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793862) option. The following fields are supported.<br /><br /> - name<br /><br /> - callCountSuccess<br /><br /> - callCountBlocked<br /><br /> - callCountFailed<br /><br /> - callCountOther<br /><br /> - bandwidth<br /><br /> - apiTimeAvg|  
  
 This report supports the following `$filter` parameter expression operand combinations.  
  
-   API  
  
-   API and operation  
  
-   Product  
  
-   Subscription - can be combined with any other filter  
  
-   User - can be combined with any other filter  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 This operation returns a [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of [Report](../ApiManagementREST/Azure-API-Management-REST-API-Report-entity.md#Report) records in `application/json` format, or the report record details in `text/csv` format.  
  
> [!NOTE]
>  For this report, the following fields are returned.  
>   
>  -   name  
> -   userId  
> -   callCountSuccess  
> -   callCountBlocked  
> -   callCountFailed  
> -   callCountOther  
> -   bandwidth  
> -   cacheHitsCount  
> -   cacheMissCount  
> -   apiTimeAvg  
> -   apiTimeMin  
> -   apiTimeMax  
> -   serviceTimeAvg  
> -   serviceTimeMin  
> -   serviceTimeMax  
>   
>  All other fields in the response contain default values.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="ReportByProduct"></a> Get metrics aggregated by product  
 This operation returns metrics aggregated by product.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/reports/byProduct|  
  
#### Request Parameters  
 None.  
  
#### Request Headers  
  
|Request Header|Description|  
|--------------------|-----------------|  
|Accept|`Accept` can be set to `text/csv` or `application/json`. If `Accept` is not set the default is `application/json`.|  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|Filter using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported. This parameter is required and must include a `timestamp` for the call to be successful.<br /><br /> timestamp:<br /><br /> - ge,le: The start and end of the reporting period, for example `$filter=timestamp ge datetime'2014-10-07T00:00:00' and timestamp le datetime'2014-10-14T00:00:00'`. If `le` is omitted the current date and time is used for the end of the reporting period. You must specify a starting date and time for `ge`.<br /><br /> apiRegion:<br /><br /> - eq: Azure region where the gateway that processed this request is located.<br /><br /> userId:<br /><br /> - eq: User identifier.<br /><br /> productId:<br /><br /> - eq: Product identifier.<br /><br /> subscriptionId:<br /><br /> - eq: Subscription identifier.|  
|$top|string|Number of records to return.|  
|$skip|string|Number of records to skip.|  
|$orderby|string|OData order by query option. The following fields are supported.<br /><br /> - name<br /><br /> - callCountSuccess<br /><br /> - callCountBlocked<br /><br /> - callCountFailed<br /><br /> - callCountOther<br /><br /> - bandwidth<br /><br /> - apiTimeAvg|  
  
 This report supports the following `$filter` parameter expression operand combinations.  
  
-   User  
  
-   Subscription - canbe combined with any other filter  
  
-   Product - can be combined with any other filter  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 This operation returns a [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of [Report](../ApiManagementREST/Azure-API-Management-REST-API-Report-entity.md#Report) records in `application/json` format, or the report record details in `text/csv` format.  
  
> [!NOTE]
>  For this report, the following fields are returned.  
>   
>  -   name  
> -   productId  
> -   callCountSuccess  
> -   callCountBlocked  
> -   callCountFailed  
> -   callCountOther  
> -   bandwidth  
> -   cacheHitsCount  
> -   cacheMissCount  
> -   apiTimeAvg  
> -   apiTimeMin  
> -   apiTimeMax  
> -   serviceTimeAvg  
> -   serviceTimeMin  
> -   serviceTimeMax  
>   
>  All other fields in the response contain default values.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="ReportByAPI"></a> Get metrics aggregated by API  
 This operation returns metrics aggregated by API.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/reports/byApi|  
  
#### Request Parameters  
 None.  
  
#### Request Headers  
  
|Request Header|Description|  
|--------------------|-----------------|  
|Accept|`Accept` can be set to `text/csv` or `application/json`. If `Accept` is not set the default is `application/json`.|  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|Filter using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported. This parameter is required and must include a `timestamp` for the call to be successful.<br /><br /> timestamp:<br /><br /> - ge,le: The start and end of the reporting period, for example `$filter=timestamp ge datetime'2014-10-07T00:00:00' and timestamp le datetime'2014-10-14T00:00:00'`. If `le` is omitted the current date and time is used for the end of the reporting period. You must specify a starting date and time for `ge`.<br /><br /> apiRegion:<br /><br /> - eq: Azure region where the gateway that processed this request is located.<br /><br /> userId:<br /><br /> - eq: User identifier.<br /><br /> productId:<br /><br /> - eq: Product identifier.<br /><br /> subscriptionId:<br /><br /> - eq: Subscription identifier.<br /><br /> apiId:<br /><br /> - eq: API identifier.|  
|$top|string|Number of records to return.|  
|$skip|string|Number of records to skip.|  
|$orderby|string|OData order by query option. The following fields are supported.<br /><br /> - name<br /><br /> - callCountSuccess<br /><br /> - callCountBlocked<br /><br /> - callCountFailed<br /><br /> - callCountOther<br /><br /> - bandwidth<br /><br /> - apiTimeAvg|  
  
 This report supports the following `$filter` parameter expression operand combinations.  
  
-   Product  
  
-   User  
  
-   User and product  
  
-   API - can be combined with any other filter  
  
-   Subscription - can be combined with any other filter  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 This operation returns a [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of [Report](../ApiManagementREST/Azure-API-Management-REST-API-Report-entity.md#Report) records in `application/json` format, or the report record details in `text/csv` format.  
  
> [!NOTE]
>  For this report, the following fields are returned.  
>   
>  -   name  
> -   apiId  
> -   callCountSuccess  
> -   callCountBlocked  
> -   callCountFailed  
> -   callCountOther  
> -   bandwidth  
> -   cacheHitsCount  
> -   cacheMissCount  
> -   apiTimeAvg  
> -   apiTimeMin  
> -   apiTimeMax  
> -   serviceTimeAvg  
> -   serviceTimeMin  
> -   serviceTimeMax  
>   
>  All other fields in the response contain default values.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="ReportByOperation"></a> Get metrics aggregated by operation  
 This operation returns metrics aggregated by operation.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/reports/byOperation|  
  
#### Request Parameters  
 None.  
  
#### Request Headers  
  
|Request Header|Description|  
|--------------------|-----------------|  
|Accept|`Accept` can be set to `text/csv` or `application/json`. If `Accept` is not set the default is `application/json`.|  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|Filter using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported. This parameter is required and must include a `timestamp` for the call to be successful.<br /><br /> timestamp:<br /><br /> - ge,le: The start and end of the reporting period, for example `$filter=timestamp ge datetime'2014-10-07T00:00:00' and timestamp le datetime'2014-10-14T00:00:00'`. If `le` is omitted the current date and time is used for the end of the reporting period. You must specify a starting date and time for `ge`.<br /><br /> apiRegion:<br /><br /> - eq: Azure region where the gateway that processed this request is located.<br /><br /> userId:<br /><br /> - eq: User identifier.<br /><br /> productId:<br /><br /> - eq: Product identifier.<br /><br /> apiId:<br /><br /> - eq: API identifier.<br /><br /> subscriptionId:<br /><br /> - eq: Subscription identifier.<br /><br /> operationId:<br /><br /> - eq: Operation identifier.|  
|$top|string|Number of records to return.|  
|$skip|string|Number of records to skip.|  
|$orderby|string|OData order by query option. The following fields are supported.<br /><br /> - name<br /><br /> - callCountSuccess<br /><br /> - callCountBlocked<br /><br /> - callCountFailed<br /><br /> - callCountOther<br /><br /> - bandwidth<br /><br /> - apiTimeAvg|  
  
 This report supports the following `$filter` parameter expression operand combinations.  
  
-   API  
  
-   Product  
  
-   User  
  
-   User and API  
  
-   User and product  
  
-   Subscription - can be combined with any other filter  
  
-   Subscription - can be combined with API and/or operation  
  
-   Operation - may not be used alone, must be combined with API  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 This operation returns a [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of [Report](../ApiManagementREST/Azure-API-Management-REST-API-Report-entity.md#Report) records in `application/json` format, or the report record details in `text/csv` format.  
  
> [!NOTE]
>  For this report, the following fields are returned.  
>   
>  -   name  
> -   operationId  
> -   callCountSuccess  
> -   callCountBlocked  
> -   callCountFailed  
> -   callCountOther  
> -   bandwidth  
> -   cacheHitsCount  
> -   cacheMissCount  
> -   apiTimeAvg  
> -   apiTimeMin  
> -   apiTimeMax  
> -   serviceTimeAvg  
> -   serviceTimeMin  
> -   serviceTimeMax  
>   
>  All other fields in the response contain default values.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="ReportBySubscription"></a> Get metrics aggregated by subscription  
 This operation returns metrics aggregated by subscription.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/reports/bySubscription|  
  
#### Request Parameters  
 None.  
  
#### Request Headers  
  
|Request Header|Description|  
|--------------------|-----------------|  
|Accept|`Accept` can be set to `text/csv` or `application/json`. If `Accept` is not set the default is `application/json`.|  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|Filter using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported. This parameter is required and must include a `timestamp` for the call to be successful.<br /><br /> timestamp:<br /><br /> - ge,le: The start and end of the reporting period, for example `$filter=timestamp ge datetime'2014-10-07T00:00:00' and timestamp le datetime'2014-10-14T00:00:00'`. If `le` is omitted the current date and time is used for the end of the reporting period. You must specify a starting date and time for `ge`.<br /><br /> apiRegion:<br /><br /> - eq: Azure region where the gateway that processed this request is located.<br /><br /> userId:<br /><br /> - eq: User identifier.<br /><br /> productId:<br /><br /> - eq: Product identifier.<br /><br /> subscriptionId:<br /><br /> - eq: Subscription identifier.|  
|$top|string|Number of records to return.|  
|$skip|string|Number of records to skip.|  
|$orderby|string|OData order by query option. The following fields are supported.<br /><br /> - name<br /><br /> - callCountSuccess<br /><br /> - callCountBlocked<br /><br /> - callCountFailed<br /><br /> - callCountOther<br /><br /> - callCountTotal<br /><br /> - bandwidth<br /><br /> - apiTimeAvg|  
  
 This report supports the following `$filter` parameter expression operand combinations.  
  
-   API  
  
-   API and operation  
  
-   User - can be combined with any other filter  
  
-   Product - can be combined with any other filter  
  
-   Subscription - can be combined with any other filter  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 This operation returns a [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of [Report](../ApiManagementREST/Azure-API-Management-REST-API-Report-entity.md#Report) records in `application/json` format, or the report record details in `text/csv` format.  
  
> [!NOTE]
>  For this report, the following fields are returned.  
>   
>  -   name  
> -   userId  
> -   productId  
> -   subscriptionId  
> -   callCountSuccess  
> -   callCountBlocked  
> -   callCountFailed  
> -   callCountOther  
> -   callCountTotal  
> -   bandwidth  
> -   cacheHitsCount  
> -   cacheMissCount  
> -   apiTimeAvg  
> -   apiTimeMin  
> -   apiTimeMax  
> -   serviceTimeAvg  
> -   serviceTimeMin  
> -   serviceTimeMax  
>   
>  All other fields in the response contain default values.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="ReportByRequest"></a> Get request log entries  
 This operation returns request log entries.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/reports/byRequest|  
  
#### Request Parameters  
 None.  
  
#### Request Headers  
  
|Request Header|Description|  
|--------------------|-----------------|  
|Accept|`Accept` can be set to `text/csv` or `application/json`. If `Accept` is not set, the default is `application/json`.|  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|Filter using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported. This parameter is required and must include a `timestamp` for the call to be successful.<br /><br /> timestamp:<br /><br /> - ge,le: The start and end of the reporting period, for example `$filter=timestamp ge datetime'2014-10-07T00:00:00' and timestamp le datetime'2014-10-14T00:00:00'`. If `le` is omitted the current date and time is used for the end of the reporting period. You must specify a starting date and time for `ge`.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 This operation returns a [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of [Request](../ApiManagementREST/Azure-API-Management-REST-API-Report-entity.md#Request) records in `application/json` or `text/csv` formats.  
  
#### Sample response body  
  
```json  
  
{  
"value":   
  [  
        {  
            "apiId": "/apis/1",  
            "operationId": "/apis/1/operations/15",  
            "productId": "/products/1",  
            "userId": "/users/1",  
            "method": "GET",  
            "url": "https://contoso.azure-api.net/weather/exampleApi?parameter=12345",  
            "ipAddress": "52.19.150.51",  
            "backendResponseCode": 200,  
            "responseCode": 200,  
            "responseSize": 6207,  
            "timestamp": "2016-08-26T21:48:10.6363746",  
            "cache": "none",  
            "apiTime": 480.2314,  
            "serviceTime": 459.9143,  
            "apiRegion": "West Europe",  
            "subscriptionId": "/subscriptions/33",  
            "requestSize": 0  
        },  
            "apiId": "/apis/2",  
            "operationId": "/apis/2/operations/10",  
            "productId": "/products/2",  
            "userId": "/users/2",  
            "method": "GET",  
            "url": "https://contoso.azure-api.net/weather/anotherExampleApi?parameter=6789",  
            "ipAddress": "100.15.65.51",  
            "backendResponseCode": 200,  
            "responseCode": 200,  
            "responseSize": 7405,  
            "timestamp": "2016-08-26T21:53:15.6378946",  
            "cache": "none",  
            "apiTime": 315.5657,  
            "serviceTime": 212.8273,  
            "apiRegion": "West US",  
            "subscriptionId": "/subscriptions/55",  
            "requestSize": 0  
        }                        
    ],  
  "count": 2  
}  
  
```  
  
#### 400 Bad Request  
 Request validation failed. The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.
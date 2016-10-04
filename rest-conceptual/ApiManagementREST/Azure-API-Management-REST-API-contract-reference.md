---
title: "Azure API Management REST API contract reference"
ms.custom: na
ms.date: 2016-05-09
ms.prod: azure
ms.reviewer: na
ms.service: api-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: bed50f05-276a-4828-b43c-33dbbe2a30bc
caps.latest.revision: 44
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
# Azure API Management REST API contract reference
This topic describes the entity and type representations for common items in Azure API Management.  
  
-   [API](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#API)  
  
-   [Authorization Server](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#AuthorizationServer)  
  
-   [Authorization Server authentication settings](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#AuthenticationSettings)  
  
-   [Backend](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Backend)  
  
-   [Certificate](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Certificate)  
  
-   [Group](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Group)  
  
-   [Logger](#Logger)  
  
-   [Operation](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Operation)  
  
-   [Operation-summary](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#OperationSummaryProperties)  
  
-   [Product](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Product)  
  
-   [Property](#Property)  
  
-   [Report](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Report)  
  
-   [Subscription](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Subscription)  
  
-   [User](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#User)  
  
-   [HTTP Request](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#HTTPRequest)  
  
-   [HTTP Response](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#HTTPResponse)  
  
-   [Parameter](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Parameter)  
  
-   [Representation](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Representation)  
  
-   [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error)  
  
-   [Error body](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error-body)  
  
-   [Error detail](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#ErrorDetail)  
  
-   [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection)  
  
-   [Policy](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Policy)  
  
 For more information about working with the REST API, see the [API Management .NET REST API Sample](https://github.com/Azure/api-management-samples/tree/master/restApiDemo) and the [Getting Started with Azure API Management REST API](http://azure.microsoft.com/documentation/videos/getting-started-with-azure-api-management-rest-api/) video.  
  
##  <a name="API"></a> API  
 The `API` entity has the following properties.  
  
|Property|Type|Description|Remarks|  
|--------------|----------|-----------------|-------------|  
|id|string|Resource identifier. Uniquely identifies the API within the current API Management service instance. The value is a valid relative URL in the format of `/apis/{id}` where `{id}` is an API identifier. This property is read-only.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|name|string|Name of the API. Must not be empty. Maximum length is 100 characters.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|description|string|Description of the API. Must not be empty. May include HTML formatting tags. Maximum length is 1000 characters.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|serviceUrl|string|Absolute URL of the backend service implementing this API.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|path|string|Relative URL uniquely identifying this API and all of its resource paths within the API Management service instance. It is appended to the API endpoint base URL specified during the service instance creation to form a public URL for this API.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|protocols|array of string|Describes on which protocols the operations in this API can be invoked. Allowed values are `http`, `https`, or both `http` and `https`.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|operations|[Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of [Operation](#Operation).|Collection of operations included in this API. Present only if the `import` query parameter is set to `true`.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|subscriptionKeyParameterNames|object|Optional property that can be used to specify custom names for query and/or header parameters containing the subscription key. When this property is present it must contain at least one of the two following properties.<br /><br /> `{   "subscriptionKeyParameterNames":   {     "query": “customQueryParameterName",     "header": “customHeaderParameterName"   } }`|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
  
> [!NOTE]
>  For more information about `API` entity operations, see [API](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md).  
  
##  <a name="AuthorizationServer"></a> Authorization Server  
 The `authorization server` entity has the following properties.  
  
|Property|Type|Description|Remarks|  
|--------------|----------|-----------------|-------------|  
|id|string|Resource identifier. Uniquely identifies the authorization server within the current API Management service instance. The value is a valid relative URL in the format of `/authorizationServers/{authsid}` where `{authsid}` is an authorization server identifier. This property is read-only.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|name|string|Name of the authorization server. Maximum length is 100 characters.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|description|string|Description of the authorization server. Can contain HTML formatting tags.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|clientRegistrationEndpoint|string|Optional reference to a page where client or app registration for this authorization server is performed. Contains absolute URL to entity being referenced.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|authorizationEndpoint|string|[OAuth authorization endpoint](http://tools.ietf.org/html/rfc6749#section-3.2). Contains absolute URI to entity being referenced.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|authorizationMethods|array|HTTP verbs supported by the authorization endpoint. `GET` must be always present. `POST` is optional.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|clientAuthenticationMethod|array|Method of authentication supported by the token endpoint of this authorization server. Possible values are `Basic` and/or `Body`. When `Body` is specified, client credentials and other parameters are passed within the request body in the `application/x-www-form-urlencoded` format.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|tokenBodyParameters|array|Additional parameters required by the token endpoint of this authorization server represented as an array of JSON objects with `name` and `value` string properties, i.e. `{"name" : "name value", "value": "a value"}`|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|tokenEndpoint|string|[OAuth token endpoint](http://tools.ietf.org/html/rfc6749#section-3.1). Contains absolute URI to entity being referenced.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|supportState|boolean|If `true`, authorization server will include state parameter from the authorization request to its response. Client may use state parameter to raise protocol security.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|defaultScope|string|[Access token scope](http://tools.ietf.org/html/rfc6749#section-3.3) that is going to be requested by default. Can be overridden at the API level. Should be provided in the form of a string containing space-delimited values.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|grantTypes|array|[Authorization](http://tools.ietf.org/html/rfc6749#section-4) grant types supported by this authorization server. Possible values are: `authorizationCode`, `implicit`, `resourceOwnerPassword`, and `clientCredentials`.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|bearerTokenSendingMethods|array|Specifies the mechanism by which access token is passed to the API. Possible values include: `auhtorizationHeader` or `query`.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|clientId|string|Client or app id registered with this authorization server.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|clientSecret|string|Client or app secret registered with this authorization server.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|resourceOwnerUsername|string|Can be optionally specified when resource owner password grant type is supported by this authorization server. Default resource owner username.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|resourceOwnerPassword|string|Can be optionally specified when resource owner password grant type is supported by this authorization server. Default resource owner password.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
  
> [!NOTE]
>  For more information about `authorization server` entity operations, see [Authorization Server](../ApiManagementREST/Azure-API-Management-REST-API-Authorization-Server-entity.md).  
  
##  <a name="AuthenticationSettings"></a> Authorization Server authentication settings  
 This section description the `oAuth2AuthenticationSettings` representation.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|authorizationServerId|string|OAuth authorization server identifier. Corresponds to the id of one of the [Authorization Server](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#AuthorizationServer) entities in the current service instance.|  
|scope|string|Operations scope. This property is optional. If present, it overrides the default scope from the authorization server.|  
  
##  <a name="Backend"></a> Backend  
 The `backend` entity has the following properties.  
  
|Property|Type|Description|Remarks|  
|--------------|----------|-----------------|-------------|  
|id|string|Resource identifier. Uniquely identifies the backend within the current API Management service instance. The value is a valid relative URL in the format of `/backends/{backendId}` where `{backendId}` is a backend identifier. This property is read-only.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|host|string|Host attribute of the backend. Host is a pure hostname without a port or suffix, for example `backend.contoso.com`. Must not be empty. Maximum length is 255 characters.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|skipCertificateChainValidation|boolean|Flag indicating whether SSL certificate chain validation should be skipped when using self-signed certificates for this backend host.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
  
> [!NOTE]
>  For more information about `backend` entity operations, see [Backend](../ApiManagementREST/Azure-API-Management-REST-API-Backend-entity.md).  
  
##  <a name="Certificate"></a> Certificate  
 The `certificate` entity has the following properties.  
  
|Property|Type|Description|Remarks|  
|--------------|----------|-----------------|-------------|  
|id|string|Resource identifier. Uniquely identifies the certificate within the current API Management service instance. The value is a valid relative URL in the format of `/certificates/{id}` where `{id}` is a certificate identifier. This property is read-only.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|subject|string|Subject attribute of the certificate.|This property is used only the following operations.<br /><br /> - [Get a list of all certificates](../ApiManagementREST/Azure-API-Management-REST-API-Certificate-entity.md#List)<br /><br /> - [Get a certificate](../ApiManagementREST/Azure-API-Management-REST-API-Certificate-entity.md#Get)|  
|thumbprint|string|Thumbprint of the certificate.|This property is used only the following operations.<br /><br /> - [Get a list of all certificates](../ApiManagementREST/Azure-API-Management-REST-API-Certificate-entity.md#List)<br /><br /> - [Get a certificate](../ApiManagementREST/Azure-API-Management-REST-API-Certificate-entity.md#Get)|  
|expirationDate|dateTime|Expiration date of the certificate, in ISO 8601 format. Example: `2014-06-24T16:25:00Z`.|This property is used only the following operations.<br /><br /> - [Get a list of all certificates](../ApiManagementREST/Azure-API-Management-REST-API-Certificate-entity.md#List)<br /><br /> - [Get a certificate](../ApiManagementREST/Azure-API-Management-REST-API-Certificate-entity.md#Get)|  
|data|string|Base 64 encoded certificate using the `application/x-pkcs12` representation.|This property is used only when adding or updating a certificate. For more information, see [Add or update a certificate](../ApiManagementREST/Azure-API-Management-REST-API-Certificate-entity.md#Add).|  
|password|string|Password for the certificate.|This property is only used when adding or updating a certificate. For more information, see [Add or update a certificate](../ApiManagementREST/Azure-API-Management-REST-API-Certificate-entity.md#Add).|  
  
> [!NOTE]
>  For more information about `certificate` entity operations, see [Certificate](../ApiManagementREST/Azure-API-Management-REST-API-Certificate-entity.md).  
  
##  <a name="Group"></a> Group  
 The `group` entity has the following properties.  
  
|Property|Type|Description|Remarks|  
|--------------|----------|-----------------|-------------|  
|id|string|Resource identifier. Uniquely identifies the group within the current API Management service instance. The value is a valid relative URL in the format of `/groups/{gid}` where `{gid}` is a group identifier. This property is read-only.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|name|string|Name of the group. Maximum length is 100 characters.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|description|string|Description of the group. Can contain HTML formatting tags. Maximum length is 1000 characters.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|builtIn|boolean|`true` if the group is one of the three system groups (Administrators, Developers, or Guests); otherwise `false`. This property is read-only.|This property is set automatically and is not used in the following operations.<br /><br /> - [Create a new group](../ApiManagementREST/Azure-API-Management-REST-API-Group-entity.md#CreateGroup)<br /><br /> - [Update an existing group](../ApiManagementREST/Azure-API-Management-REST-API-Group-entity.md#UpdateGroup)|  
|type|string|The type of group, which is one of the following values: `system`, `custom`, or `external`. This property is read-only.|This property is set automatically and is not used in the following operations.<br /><br /> - [Create a new group](../ApiManagementREST/Azure-API-Management-REST-API-Group-entity.md#CreateGroup)<br /><br /> - [Update an existing group](../ApiManagementREST/Azure-API-Management-REST-API-Group-entity.md#UpdateGroup)|  
|externalId|string|For external groups, this property contains the id of the group from the external identity provider, e.g. Azure Active Directory; otherwise the value is `null`. This property is read-only.|This property is set automatically and is not used in the following operations.<br /><br /> - [Create a new group](../ApiManagementREST/Azure-API-Management-REST-API-Group-entity.md#CreateGroup)<br /><br /> - [Update an existing group](../ApiManagementREST/Azure-API-Management-REST-API-Group-entity.md#UpdateGroup)|  
  
> [!NOTE]
>  For more information about `group` entity operations, see [Group](../ApiManagementREST/Azure-API-Management-REST-API-Group-entity.md).  
  
##  <a name="Logger"></a> Logger  
 The logger entity has the following properties.  
  
|Property|Type|Description|Remarks|  
|--------------|----------|-----------------|-------------|  
|id|string|Resource identifier. Uniquely identifies the logger within the current API Management service instance. The value is a valid relative URL in the format of `/loggers/{loggerId}` where `{loggerId}` is a logger identifier. This property is read-only.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|type|string|The type of logger. The value must be set to `AzureEventHub`.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|description|string|Description of the logger.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|credentials|string dictionary|The name and **SendRule** connection string of the event hub.<br /><br /> `"credentials" : {     "name" : "Event hub name from Azure classic portal",     "connectionString" : "Endpoint=endpoint and key from Azure classic portal"     }`|For security purposes, this property is not returned in the response body for the following operations.<br /><br /> - [List loggers](../ApiManagementREST/Azure-API-Management-REST-API-Logger-entity.md#List)<br /><br /> - [Get a specific logger](../ApiManagementREST/Azure-API-Management-REST-API-Logger-entity.md#GET)|  
  
> [!NOTE]
>  Only `id`, `type`, and `description` are returned for operations that return a logger entity. The `credentials` are not returned and are used only when creating or updating a logger entity.  
  
##  <a name="Operation"></a> Operation  
 The `operation` entity has the following properties.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|id|string|Resource identifier. Uniquely identifies the operation within the current API Management service instance. The value is a valid relative URL in the format of `/apis/{aid}/operations/{id}` where `{aid}` is an API identifier and `{id}` is an operation identifier. This property is read-only.|  
|name|string|Name of the operation. Must not be empty. Maximum length is 100 characters.|  
|method|string|Operation HTTP method.|  
|urlTemplate|string|Relative URL template identifying the target resource for this operation. May include parameters. Example: `/customers/{cid}/orders/{oid}/?date={date}`|  
|templateParameters|array of [Parameter](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Parameter)|Array of URL template parameters.|  
|description|string|Description of the operation. Must not be empty. May include HTML formatting tags. Maximum length is 1000 characters.|  
|request|[HTTP Request](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#HTTPRequest)|An entity containing request details.|  
|responses|array of [HTTP Response](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#HTTPResponse)|Array of operation [HTTP Response](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#HTTPResponse) entities.|  
  
> [!NOTE]
>  For more information about `operation` entity operations, see the operation methods in the [API](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md) documentation.  
  
##  <a name="OperationSummaryProperties"></a> Operation-summary  
 The `operation-summary` entity has the following properties.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|id|string|Resource identifier. Uniquely identifies the operation within the current API Management service instance. The value is a valid relative URL in the format of `/apis/{aid}/operations/{id}` where `{aid}` is an API identifier and `{id}` is an operation identifier. This property is read-only.|  
|name|string|Name of the operation. Must not be empty. Maximum length is 100 characters.|  
|method|string|Operation HTTP method.|  
|urlTemplate|string|Relative URL template identifying the target resource for this operation. May include parameters. Example: `/customers/{cid}/orders/{oid}/?date={date}`|  
|description|string|Description of the operation. Must not be empty. May include HTML formatting tags. Maximum length is 1000 characters.|  
  
> [!NOTE]
>  For more information about `operation-summary` entity operations, see the operation methods in the [API](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md) documentation.  
  
##  <a name="Product"></a> Product  
 The `product` entity has the following properties.  
  
|Property|Type|Description|Remarks|  
|--------------|----------|-----------------|-------------|  
|id|string|Resource identifier. Uniquely identifies the product within the current API Management service instance. The value is a valid relative URL in the format of `/products/{pid}` where `{pid}` is a product identifier. This property is read-only.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|name|string|Name of the product. Must not be empty. Maximum length is 100 characters.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|description|string|Description of the product. Must not be empty. May include HTML formatting tags. Maximum length is 1000 characters.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|terms|string|Product terms of use. Developers trying to subscribe to the product will be presented and required to accept these terms before they can complete the subscription process.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|subscriptionRequired|boolean|Specifies whether a product subscription is required for accessing APIs included in this product. If `true`, the product is referred to as **protected** and a valid subscription key is required for a request to an API included in the product to succeed. If `false`, the product is referred to as **open** and requests to an API included in the product can be made without a subscription key. If this property is omitted when creating a new product the default is `true`.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|approvalRequired|boolean|Specifies whether subscription approval is required. If `false`, new subscriptions will be approved automatically enabling developers to call the product’s APIs immediately after subscribing. If `true`, administrators must manually approve the subscription before the developer can any of the product’s APIs.<br /><br /> Can be present only if the `subscriptionRequired` property is present with a value of `true`.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|subscriptionsLimit|number|Specifies the number of subscriptions a user can have to this product at the same time. Set to `null` or omit to allow unlimited per user subscriptions.<br /><br /> Can be present only if the `subscriptionRequired` property is present with a value of `true`.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|state|string|Specifies whether the product is published or not. Published products are discoverable by developers on the developer portal. Non-published products are visible only to administrators.<br /><br /> The allowable values for product state are `published` and `notPublished`.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|groups|array|An array of [Group](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Group) entities that have visibility to the product.|This property is optional and is only included in responses when the request has an `expandGroups` query parameter with a value of `true`.|  
  
> [!NOTE]
>  For more information about `product` entity operations, see [Product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md).  
  
##  <a name="Property"></a> Property  
 The `property` entity has the following properties.  
  
|Property|Type|Description|Remarks|  
|--------------|----------|-----------------|-------------|  
|id|string|Resource identifier. Uniquely identifies the property within the current API Management service instance. The value is a valid relative URL in the format of `/properties/{propId}` where `{propId}` is a property identifier. This property is read-only.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|name|string|Name of the property. Maximum length is 100 characters. It may contain only letters, digits, period, dash, and underscore characters.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|value|string|Value of the property. Can contain policy expressions. Maximum length is 1000 characters. It may not be empty or consist only of whitespace.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|tags|array of string|Optional tags that when provided can be used to filter the property list.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|secret|boolean|Determines whether the value is a secret and should be encrypted or not.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
  
##  <a name="Report"></a> Report  
 The `report` entity has the following properties.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|name|string|Depending on the report endpoint this property specifies product, API, operation, or developer name.|  
|timestamp|dateTime|Start of reporting interval presented in this entry, in ISO 8601 format: `2014-06-24T16:25:00Z`.|  
|interval|string|Period of time over which the data presented in this entity was aggregated, in ISO 8601 format: `P500DT3H10M15.304S`.|  
|country|string|Country to which this data entity is related.|  
|region|string|Country region to which this entity is related (US only).|  
|zip|string|Zip code to which this entity is related (US only).|  
|userId|string|[User](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#User) identifier.|  
|productId|string|[Product](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Product) identifier.|  
|apiId|string|[API](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#API) identifier.|  
|operationId|string|[Operation](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Operation) identifier.|  
|apiRegion|string|API region identifier.|  
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
  
> [!NOTE]
>  For more information about `report` entity operations, see [Report](../ApiManagementREST/Azure-API-Management-REST-API-Report-entity.md).  
  
##  <a name="Subscription"></a> Subscription  
 The `subscription` entity has the following properties.  
  
|Property|Type|Description|Remarks|  
|--------------|----------|-----------------|-------------|  
|id|string|Resource identifier. Uniquely identifies the subscription within the current API Management service instance. The value is a valid relative URL in the format of `/subscriptions/{sid}` where `{sid}` is a subscription identifier. This property is read-only.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|userId|string|The user resource identifier of the subscription owner. The value is a valid relative URL in the format of `/users/{uid}` where `{uid}` is a user identifier.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|productId|string|The product resource identifier of the subscribed product. The value is a valid relative URL in the format of `/products/{pid}` where `{pid}` is a product identifier.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|name|string|The name of the subscription, or `null` if the subscription has no name.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|state|string|The state of the subscription. Possible states are:<br /><br /> - `active` – the subscription is active.<br /><br /> - `suspended` – the subscription is blocked, and the subscriber cannot call any APIs of the product.<br /><br /> - `submitted` – the subscription request has been made by the developer, but has not yet been approved or rejected.<br /><br /> - `rejected` – the subscription request has been denied by an administrator.<br /><br /> - `cancelled` – the subscription has been cancelled by the developer or administrator.<br /><br /> - `expired` – the subscription reached its expiration date and was deactivated.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|createdDate|dateTime|Subscription created date, in ISO 8601 format: `2014-06-24T16:25:00Z`.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|startDate|dateTime|Subscription activation date, in ISO 8601 format: `2014-06-24T16:25:00Z`.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|expirationDate|dateTime|Subscription expiration date, in ISO 8601 format: `2014-06-24T16:25:00Z`.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|endDate|dateTime|The date the subscription was cancelled, in ISO 8601 format: `2014-06-24T16:25:00Z`.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|notificationDate|dateTime|The notification date for an upcoming expiration, in ISO 8601 format: `2014-06-24T16:25:00Z`.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|primaryKey|string|The primary subscription key. Maximum length is 256 characters.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|secondaryKey|string|The secondary subscription key. Maximum length is 256 characters.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|stateComment|string|Optional subscription comment added by an administrator.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
  
> [!NOTE]
>  For more information about `subscription` entity operations, see [Subscription](../ApiManagementREST/Azure-API-Management-REST-API-Subscription-entity.md).  
  
##  <a name="User"></a> User  
 The `user` entity has the following properties.  
  
|Property|Type|Description|Remarks|  
|--------------|----------|-----------------|-------------|  
|id|string|Resource identifier. Uniquely identifies the user within the current API Management service instance. The value is a valid relative URL in the format of `/users/{uid}` where `{uid}` is a user identifier. This property is read-only.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|firstName|string|First name. Must not be empty. Maximum length is 100 characters.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|lastName|string|Last name. Must not be empty. Maximum length is 100 characters.|This property is passed as a path parameter and is not present as part of the request body when creating or updating this entity.|  
|password|string|User password.|For security purposes, this property is not returned in the response body for the following operations.<br /><br /> - [List registered users](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#List)<br /><br /> - [Get a specific user](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#GetUser)|  
|email|string|Email address. Must not be empty and must be unique within the service instance. Maximum length is 254 characters.|For security purposes, this property is not returned in the response body for the following operations.<br /><br /> - [List registered users](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#List)<br /><br /> - [Get a specific user](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#GetUser)|  
|state|string|Specifies whether the user is active or not. Blocked users are unable to sign into the developer portal or call any APIs of subscribed products.<br /><br /> The allowable values for user state are `active` and `blocked`.|For security purposes, this property is not returned in the response body for the following operations.<br /><br /> - [List registered users](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#List)<br /><br /> - [Get a specific user](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#GetUser)|  
|registrationDate|dateTime|User registration date, in ISO 8601 format: `2014-06-24T16:25:00Z`|For security purposes, this property is not returned in the response body for the following operations.<br /><br /> - [List registered users](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#List)<br /><br /> - [Get a specific user](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#GetUser)|  
|note|string|Optional note about a user set by the administrator.|For security purposes, this property is not returned in the response body for the following operations.<br /><br /> - [List registered users](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#List)<br /><br /> - [Get a specific user](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md#GetUser)|  
|groups|boolean|An array of [Group](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Group) entities to which the user belongs.|This property is optional and is only included in responses when the request has an `expandGroups` query parameter with a value of `true`.|  
  
> [!NOTE]
>  For more information about `user` entity operations, see [User](../ApiManagementREST/Azure-API-Management-REST-API-User-entity.md).  
  
##  <a name="HTTPRequest"></a> HTTP Request  
 This section describes the `request` representation.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|description|string|Operation request description.|  
|queryParameters|array of [Parameter](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Parameter)|Collection of operation request query parameters.|  
|headers|array of [Parameter](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Parameter)|Collection of operation request headers.|  
|representations|array of [Representation](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Representation)|Collection of operation request representations.|  
  
##  <a name="HTTPResponse"></a> HTTP Response  
 This section describes the `response` representation.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|statusCode|positive integer|Operation response status code.|  
|description|string|Operation response description.|  
|representations|array of [Representation](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Representation)|Collection of operation response representations.|  
  
##  <a name="Parameter"></a> Parameter  
 This section describes the `parameter` representation.  
  
|Property|Description|Type|  
|--------------|-----------------|----------|  
|name|string|Parameter name.|  
|description|string|Parameter description.|  
|type|string|Parameter type.|  
|defaultValue|string|Default parameter value.|  
|required|boolean|Specifies whether parameter is required or not.|  
|values|array of string|Parameter values.|  
  
##  <a name="Representation"></a> Representation  
 This section describes a `representation`.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|contentType|string|Specifies a registered or custom content type for this representation, e.g. `application/xml`.|  
|sample|string|An example of the representation.|  
  
##  <a name="error"></a> Error  
 This section describes the `error` representation.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|error|[Error body](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error-body)|The error body containing the details of the error.|  
  
##  <a name="error-body"></a> Error body  
 This section describes the `error-body` representation.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|code|string|Service-defined error code. This code serves as a sub-status for the HTTP error code specified in the response.|  
|message|string|Description of the error.|  
|details|[Error detail](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#ErrorDetail)|In case of validation errors this field contains a list of invalid fields sent in the request.|  
  
##  <a name="ErrorDetail"></a> Error detail  
 This section describes the `error-detail` representation.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|code|string|Property level error code.|  
|message|string|Human readable representation of the `property-level` error.|  
|target|string|Optional. Property name.|  
  
##  <a name="collection"></a> Collection  
 This section describes the `collection` representation.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|nextLink|string|The absolute url to the remaining items in the collection.|  
|count|long|The total number of elements in the collection.|  
|value|array|Contains a collection of items included in this response.|  
  
##  <a name="Policy"></a> Policy  
 This section describes the `application/vnd.ms-azure-apim.policy+xml` representation. This representation contains the policy definitions for the specified entity, and each representation is different depending on the specific policy. In the following example, a usage policy for a product is specified which limits calls to a rate of 10 calls per minute, with a total of 200 calls per week.  
  
```xml  
<policies>  
    <inbound>  
        <rate-limit calls="10" renewal-period="60">  
        </rate-limit>  
        <quota calls="200" renewal-period="604800">  
        </quota>  
        <base />  
  
</inbound>  
<outbound>  
  
    <base />  
  
    </outbound>  
</policies>  
```  
  
 For a list of all API Management policies and their representations, see [API Management policy reference](http://go.microsoft.com/fwlink/?LinkID=398186).
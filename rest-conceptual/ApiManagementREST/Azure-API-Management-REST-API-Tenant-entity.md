---
title: "Azure API Management REST API Tenant entity"
ms.custom: na
ms.date: 2016-09-22
ms.prod: azure
ms.reviewer: na
ms.service: api-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 25747017-34cf-4821-ae42-8b67863afca9
caps.latest.revision: 14
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
# Azure API Management REST API Tenant entity
This topic describes how to manage properties and configuration that apply to the entire API Management service instance using the API Management REST API.  
  
 For more information about working with the REST API, see the [API Management .NET REST API Sample](https://github.com/Azure/api-management-samples/tree/master/restApiDemo) and the [Getting Started with Azure API Management REST API](http://azure.microsoft.com/documentation/videos/getting-started-with-azure-api-management-rest-api/) video.  
  
## In this topic  
  
-   [Prerequisites](../ApiManagementREST/Azure-API-Management-REST-API-Tenant-entity.md#Prerequisites)  
  
-   [Get global policy configuration for a tenant](../ApiManagementREST/Azure-API-Management-REST-API-Tenant-entity.md#GetPolicy)  
  
-   [Check a tenant for attached global policy configuration](../ApiManagementREST/Azure-API-Management-REST-API-Tenant-entity.md#HEAD)  
  
-   [Set global policy configuration for a tenant](../ApiManagementREST/Azure-API-Management-REST-API-Tenant-entity.md#SetPolicy)  
  
-   [Remove global policy configuration from a tenant](../ApiManagementREST/Azure-API-Management-REST-API-Tenant-entity.md#RemovePolicy)  
  
-   [Get tenant Git access information](#GetGit)  
  
-   [Get the metadata for Git access configuration](#GetMetadata)  
  
-   [Enable or disable Git access](#EnableGit)  
  
-   [Regenerate Git configuration primary key](#RegeneratePrimaryKey)  
  
-   [Regenerate Git configuration secondary key](#RegenerateSecondaryKey)  
  
-   [Get a list of all async operation results](#ListOperations)  
  
-   [Get an async operation result](#GetOperation)  
  
-   [Commit configuration snapshot](#CommitSnapshot)  
  
-   [Deploy Git changes to configuration database](#DeployChanges)  
  
-   [Validate Git changes](#ValidateChanges)  
  
-   [Get the status of the latest synchronization](#GetSyncStatus)  
  
##  <a name="Prerequisites"></a> Prerequisites  
  
> [!IMPORTANT]
>  Before making any calls into the API Management REST API, please review the [Prerequisites](../ApiManagementREST/API-Management-REST.md#Prerequisites) section of the [API Management REST](../ApiManagementREST/API-Management-REST.md) guide. This specifies the necessary authentication, version parameters, supported media types, and other information required in order to successfully call the API Management REST API.  
  
##  <a name="GetPolicy"></a> Get global policy configuration for a tenant  
 This operation returns the global policy configuration for the specified tenant.  
  
> [!NOTE]
>  To work with policies defined at product, API, or operation scope, see the policy operations in the [Product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md) and [API](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md) entity documentation.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/tenant/policy|  
  
#### Request Parameters  
 None.  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The response headers contain the following metatada.  
  
|Headers|  
|-------------|  
|ETag|string|Current entity state version.|  
  
 The response body contains a [Policy](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Policy) response type. The media type for this response is `application/vnd.ms-azure-apim.policy+xml`.  
  
##### Sample response body  
  
```xml  
<policies>  
	<inbound>  
	</inbound>  
	<backend>  
		<forward-request follow-redirects="true" />  
	</backend>  
	<outbound>  
	</outbound>  
</policies>  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 There is no policy configuration attached.  
  
##  <a name="HEAD"></a> Check a tenant for attached global policy configuration  
 This operation determines if a global policy configuration is attached to the tenant.  
  
> [!NOTE]
>  To work with policies defined at product, API, or operation scope, see the policy operations in the [Product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md) and [API](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md) entity documentation.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|HEAD|/tenant/policy|  
  
#### Request Parameters  
 None.  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 Policy configuration is attached to the tenant.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not found  
 There is no policy configuration attached.  
  
##  <a name="SetPolicy"></a> Set global policy configuration for a tenant  
 This operation sets the global policy configuration for a tenant.  
  
> [!NOTE]
>  To work with policies defined at product, API, or operation scope, see the policy operations in the [Product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md) and [API](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md) entity documentation.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PUT|/tenant/policy|  
  
#### Request Parameters  
 None.  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the product. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
|Content-Type|Possible values are `application/vnd.ms-azure-apim.policy+xml` and `application/vnd.ms-azure-apim.policy.raw+xml`.<br /><br /> When using `application/vnd.ms-azure-apim.policy+xml`, expressions contained within the policy must be XML-escaped.<br /><br /> When using `application/vnd.ms-azure-apim.policy.raw+xml` no escaping is necessary.|  
  
#### Request Body  
 The request body is the desired [Policy](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Policy) representation.  
  
```xml  
<policies>  
	<inbound>  
	</inbound>  
	<backend>  
		<forward-request follow-redirects="true" />  
	</backend>  
	<outbound>  
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
  
#### 412 Precondition Failed  
 Returned if the product resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="RemovePolicy"></a> Remove global policy configuration from a tenant  
 This operation removes the global policy configuration for the specified product.  
  
> [!NOTE]
>  To work with policies defined at product, API, or operation scope, see the policy operations in the [Product](../ApiManagementREST/Azure-API-Management-REST-API-Product-Entity.md) and [API](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md) entity documentation.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|DELETE|/tenant/policy|  
  
#### Request parameters  
 None.  
  
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
  
##  <a name="GetGit"></a> Get tenant Git access information  
 This operation returns the Git access configuration for the tenant.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/tenant/access/git|  
  
#### Request Parameters  
 None.  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The response headers contain the following metatada.  
  
|Headers|  
|-------------|  
|ETag|string|Current entity state version.|  
  
 The response body contains the following information.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|primaryKey|string|The primary access key.|  
|secondaryKey|string|The secondary access key.|  
|enabled|boolean|Determines whether Git access is enabled or disabled.|  
  
##### Sample response body  
  
```json  
{  
  "id": "56d49ec51b72ff123b030004",  
  "primaryKey": "MhOHj7XFJiTBoRyFDlJ7CGR63EMwYASEt4rJh5CyNXVrcA3VA9AYkFbrLpi463E3VHXhQFd0wWn4Qi4RrT9TRg==",  
  "secondaryKey": "hKM8tb+0bdq0lCEZAgtYuiWl6Z400APzIuZt0REftPEyGmFu6yaKCBap9QGOey6+GKHxXHalSBkt0F0XcOR17g==",  
  "enabled": false  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="GetMetadata"></a> Get the metadata for Git access configuration  
 This operation retrieves the metadata for the Git access configuration.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|HEAD|/tenant/access/git|  
  
#### Request Parameters  
 None.  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The operation was successful.  
  
|Headers|  
|-------------|  
|ETag|string|Current entity state version|  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="EnableGit"></a> Enable or disable Git access  
 This operation updates the details of a subscription.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PATCH|/tenant/access/git|  
  
#### Request parameters  
 None.  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the Git access configuration. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
#### Request Body  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|enabled|boolean|Determines whether Git access is enabled or disabled.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The Git configuration status was successfully updated.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="RegeneratePrimaryKey"></a> Regenerate Git configuration primary key  
 This operation regenerates the primary key for Git configuration access.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|POST|/tenant/access/git/regeneratePrimaryKey|  
  
#### Request Parameters  
 None.  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The primary key was successfully regenerated.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="RegenerateSecondaryKey"></a> Regenerate Git configuration secondary key  
 This operation regenerates the secondary key for Git configuration access.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|POST|/tenant/access/git/regenerateSecondaryKey|  
  
#### Request Parameters  
 None.  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The secondary key was successfully regenerated.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="ListOperations"></a> Get a list of all async operation results  
 This operation returns a list of all the finished and in-progress asynchronous operation results in the specified service instance.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/tenant/configuration/operationResults|  
  
#### Request Parameters  
 None.  
  
#### Request Headers  
 None.  
  
#### Request Body  
 None.  
  
### Responses  
  
#### 200 OK  
 A [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of [operation results](#OperationResultsType) for the specified API Management service instance.  
  
##### Sample response body  
  
```json  
{  
  "value": [  
    {  
      "id": "56d0c47675a58d07740f7196",  
      "status": "Succeeded",  
      "started": "2016-02-26T21:32:38.803",  
      "updated": "2016-02-26T21:32:57.613",  
      "resultInfo": "Current configuration was successfully saved to master as commit 21529f869027474fec3f0939a9e2c588bd9c8e82.",  
      "error": null  
    },  
    {  
      "id": "56cf7db875a58d07740f707b",  
      "status": "Succeeded",  
      "started": "2016-02-25T22:18:32.807",  
      "updated": "2016-02-25T22:19:32.12",  
      "resultInfo": "Current configuration was successfully saved to master as commit d91ad6c9cbae4051629768634b8c5a19f815a8be.",  
      "error": null  
    }  
  ],  
  "count": 2,  
  "nextLink": null  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="GetOperation"></a> Get an async operation result  
 This operation returns the status of the specified asynchronous operation.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/tenant/configuration/operationResults/{operationId}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|operationId|string|Operation identifier.|  
  
### Responses  
 This operation has the following responses.  
  
####  <a name="OperationResultsType"></a> 200 OK or 202 Accepted  
 `202 Accepted` is returned while the operation is in flight. `200 OK` is returned upon operation completion.  
  
 The response headers contain the following metadata about the entity.  
  
|Headers|  
|-------------|  
|ETag|string|Current entity state version. Should be treated as opaque and used to make conditional HTTP requests.|  
  
 The response body contains the following information about the operation.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|id|string|The Id of the operation.|  
|status|string|The status of the operation. Can have one of the following values: `Started`, `In progress`, `Succeeded`, `Failed`.|  
|started|dateTime|The date/time the operation started, in ISO 8601 format: `2014-06-24T16:25:00Z`.|  
|updated|dateTime|The date/time of the latest operation update, in ISO 8601 format: `2014-06-24T16:25:00Z`.|  
|resultInfo|string|A description of the result of the operation.|  
|error|string|If there was an error, contains a description of the error.|  
  
##### Sample response body  
  
```json  
{  
  "id": "56d0c47675a58d07740f7196",  
  "status": "Succeeded",  
  "started": "2016-02-26T21:32:38.803",   
  "updated": "2016-02-26T21:32:57.613",  
  "resultInfo": "Current configuration was successfully saved to master as commit 21529f869027474fec3f0939a9e2c588bd9c8e82.",  
  "error": null  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified operation result does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="CommitSnapshot"></a> Commit configuration snapshot  
 This operation creates a commit with the current configuration snapshot to the specified branch in the repository.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|POST|/tenant/configuration/save|  
  
#### Request parameters  
 None.  
  
#### Request Body  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|branch|string|Name of the Git branch in which to commit the current configuration snapshot.|  
|force|boolean|If `true`, the current configuration database is committed to the Git repository, even if the Git repository has newer changes that would be overwritten.|  
  
### Responses  
 This operation has the following responses.  
  
#### 202 Request Accepted  
 The save request was accepted.  
  
 The response headers contain a `Location` header that contains a URL you can use to check on the status of the operation. This URL maps to the [Get an async operation result](#GetOperation) operation and contains the `operationId` of the operation. Call this operation to retrieve the status of the operation and the results of the operation once it has completed.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="DeployChanges"></a> Deploy Git changes to configuration database  
 This operation applies changes from the specified Git branch to the configuration database.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|POST|/tenant/configuration/deploy|  
  
#### Request parameters  
 None.  
  
#### Request Body  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|branch|string|Name of the Git branch from which the configuration is to be deployed to the configuration database.|  
|force|boolean|Enforce deleting subscriptions to products that are deleted in this update.|  
  
### Responses  
 This operation has the following responses.  
  
#### 202 Request Accepted  
 The save request was accepted.  
  
 The response headers contain a `Location` header that contains a URL you can use to check on the status of the operation. This URL maps to the [Get an async operation result](#GetOperation) operation.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="ValidateChanges"></a> Validate Git changes  
 This operation validates the changes in the specified Git branch.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|POST|/tenant/configuration/validate|  
  
#### Request parameters  
 None.  
  
#### Request Body  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|branch|string|Name of the Git branch from which the configuration is to be deployed to the configuration database.|  
|force|boolean|Enforce deleting subscriptions to products that are deleted in this update.|  
  
### Responses  
 This operation has the following responses.  
  
#### 202 Request Accepted  
 The save request was accepted.  
  
 The response headers contain a `Location` header that contains a URL you can use to check on the status of the operation. This URL maps to the [Get an async operation result](#GetOperation) operation and contains the `operationId` of the operation. Call this operation to retrieve the status of the operation and the results of the validation once it has completed.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="GetSyncStatus"></a> Get the status of the latest synchronization  
 This operation returns the status of the most recent synchronization between the configuration database and the Git repository.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/tenant/configuration/syncState|  
  
#### Request Parameters  
 None.  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The response body contains the following information.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|branch|string|Name of the Git branch.|  
|commitId|string|The latest commit Id.|  
|isExport|boolean|Indicates if the latest synchronization was a Save (true) or Deploy (false) operation.|  
|isSynced|boolean|Indicates if the latest synchronization was later than the configuration change.|  
|isGitEnabled|boolean|Indicates whether Git configuration access is enabled.|  
|SyncDate|dateTime|The date/time of the latest synchronization, in ISO 8601 format: `2014-06-24T16:25:00Z`.|  
|ConfigurationChangeDate|dateTime|The date/time of the latest configuration change, in ISO 8601 format: `2014-06-24T16:25:00Z`.|  
  
##### Sample response body  
  
```json  
{  
  "branch": "master",  
  "commitId": "21529f869027474fec3f0939a9e2c588bd9c8e82",  
  "isExport": true,  
  "isSynced": true,  
  "isGitEnabled": true,  
  "syncDate": "2016-02-26T21:32:57.2508897Z",  
  "configurationChangeDate": "2016-02-26T21:32:29.3747952Z"  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.
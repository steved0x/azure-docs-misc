---
title: "Azure API Management REST API Certificate entity"
ms.custom: na
ms.date: 2016-05-09
ms.prod: azure
ms.reviewer: na
ms.service: api-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 8471692d-79e7-4cbd-b602-9f9ed4e586c4
caps.latest.revision: 13
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
# Azure API Management REST API Certificate entity
This topic describes how to manage certificates and their operations using the API Management REST API.  
  
 For more information about working with certificates in the publisher portal, see [How to secure back-end services using mutual certificate authentication in Azure API Management](http://go.microsoft.com/fwlink/?LinkId=511599).  
  
 For more information about working with the REST API, see the [API Management .NET REST API Sample](https://github.com/Azure/api-management-samples/tree/master/restApiDemo) and the [Getting Started with Azure API Management REST API](http://azure.microsoft.com/documentation/videos/getting-started-with-azure-api-management-rest-api/) video.  
  
## In this topic  
  
-   [Prerequisites](../ApiManagementREST/Azure-API-Management-REST-API-Certificate-entity.md#Prerequisites)  
  
-   [Get a list of all certificates](../ApiManagementREST/Azure-API-Management-REST-API-Certificate-entity.md#List)  
  
-   [Get a certificate](../ApiManagementREST/Azure-API-Management-REST-API-Certificate-entity.md#Get)  
  
-   [Get the metadata for a certificate](../ApiManagementREST/Azure-API-Management-REST-API-Certificate-entity.md#GetMetadata)  
  
-   [Add or update a certificate](../ApiManagementREST/Azure-API-Management-REST-API-Certificate-entity.md#Add)  
  
-   [Remove a certificate](../ApiManagementREST/Azure-API-Management-REST-API-Certificate-entity.md#Remove)  
  
##  <a name="Prerequisites"></a> Prerequisites  
  
> [!IMPORTANT]
>  Before making any calls into the API Management REST API, please review the [Prerequisites](../ApiManagementREST/API-Management-REST.md#Prerequisites) section of the [API Management REST](../ApiManagementREST/API-Management-REST.md) guide. This specifies the necessary authentication, version parameters, supported media types, and other information required in order to successfully call the API Management REST API.  
  
##  <a name="List"></a> Get a list of all certificates  
 This operation returns a collection of all certificates in the specified service instance.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/certificates|  
  
#### Request Parameters  
 None.  
  
#### Request Headers  
 None.  
  
#### Request Body  
 None.  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|You can filter the results using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported<br /><br /> id:<br /><br /> - ge, le, eq, ne, gt, lt:  substringof, startswith, endswith<br /><br /> subject:<br /><br /> - ge, le, eq, ne, gt, lt: substringof, startswith, endswith<br /><br /> thumbprint:<br /><br /> - ge, le, eq, ne, gt, lt: substringof, startswith, endswith<br /><br /> expirationDate:<br /><br /> - ge, le, eq, ne, gt, lt: N/A|  
|$top|string|The number of entities to return.|  
|$skip|string|The number of entities to skip.|  
  
### Responses  
  
#### 200 OK  
 A [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of the [Certificate](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Certificate) entities for the specified API Management service instance.  
  
##### Sample response body  
  
```json  
{  
  "value": [  
    {  
      "id": "/certificates/544fe9abc3b8f30fb490d90f",  
      "subject": "CN=myapi.cloudapp.net",  
      "thumbprint": "446581AC8386C0F79FE0C5C866431E45FCA5545E",  
      "expirationDate": "2016-08-21T21:10:42"  
    }  
  ],  
  "count": 1,  
  "nextLink": null  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="Get"></a> Get a certificate  
 This operation returns the details of the certificate specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/certificates/{cid}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|cid|string|Certificate identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The response headers contain the following metatada about the certificate.  
  
|Headers|||  
|-------------|-|-|  
|ETag|string|Current entity state version. Should be treated as opaque and used to make conditional HTTP requests.|  
  
 The response body contains the specified [Certificate](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Certificate) entity.  
  
##### Sample response body  
  
```json  
{  
  "id": "/certificates/544fe9abc3b8f30fb490d90f",  
  "subject": "CN=myapi.cloudapp.net",  
  "thumbprint": "446581AC8386C0F79FE0C5C866431E45FCA5545E",  
  "expirationDate": "2016-08-21T21:10:42"  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified certificate does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="GetMetadata"></a> Get the metadata for a certificate  
 This operation returns the metadata for the certificate specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|HEAD|/certificates/{cid}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|cid|string|Certificate identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The operation was successful.  
  
|Headers|||  
|-------------|-|-|  
|ETag|string|Current entity state version. Should be treated as opaque and used to make conditional HTTP requests.|  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not found  
 The specified certificate does not exist.  
  
##  <a name="Add"></a> Add or update a certificate  
 This operation adds a new certificate to or updates an existing certificate of the specified API Management service instance.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PUT|/certificates/{cid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|cid|string|Certificate identifier. Must be unique in the current API Management service instance. Maximum length is 256 characters.|  
  
#### Request Headers  
  
|Request Header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the certificate. Required only if updating an existing certificate. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
#### Request body  
 The request body is the following two properties from a [Certificate](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Certificate) entity.  
  
```json  
{  
    data = "Base 64 encoded certificate using the application/x-pkcs12 representation",  
    password="..."  
}  
```  
  
> [!NOTE]
>  Certificates must be in the `.pfx` format. Self-signed certificates are allowed.  
  
 The following code example shows how to specify a certificate as part of the request body.  
  
```c#  
public async Task UploadAsync(string filePath, string password, string certificateId, string sharedAccessSignature)  
{  
    const string apiVersion = "2014-02-14-preview"; // or other supported api-version  
    const string serviceName = "myservice";  
    var httpClient = new HttpClient();  
    string url = string.Concat("https://",  
        serviceName,  
        ".management.-azure-api.net/certificates/",  
        certificateId,  
        "?api-version=",  
        apiVersion,  
        "&password=",  
        password);  
  
    var request = new HttpRequestMessage(HttpMethod.Put, url);  
    request.Headers.Authorization = new AuthenticationHeaderValue("SharedAccessSignature", sharedAccessSignature);  
  
    // Create the body of the request in the following format  
    //{  
    //    data: "<Base64-encoded certificate>",  
    //    password: "<password here>"  
    //}  
  
    // Load the certificate and encode it to Base64.  
    var bytes = File.ReadAllBytes(filePath);  
    var encodedBytes = Convert.ToBase64String(bytes);  
  
    // Create the JSON body for the request.  
    var body = new JObject();  
    body.Add(new JProperty("data", encodedBytes));  
    body.Add(new JProperty("password", password));  
    request.Content = new StringContent(body.ToString());  
  
    // Make the request.  
    HttpResponseMessage response = await httpClient.SendAsync(request);  
  
    // Throw an exception if the call is not successful.  
    response.EnsureSuccessStatusCode();  
}  
```  
  
### Responses  
 This operation has the following responses.  
  
#### 201 Created  
 The new certificate was successfully added.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 409 Conflict  
 Certificate with the same identifier already exists.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="Remove"></a> Remove a certificate  
 This operation deletes the specified certificate.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|DELETE|/certificates/{cid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|cid|string|Certificate identifier.|  
  
#### Request Headers  
  
|Request Header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the certificate to remove. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The certificate was successfully deleted.  
  
#### 400 Bad Request  
 Certificate cannot be deleted since it is being used by one or more policies.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.
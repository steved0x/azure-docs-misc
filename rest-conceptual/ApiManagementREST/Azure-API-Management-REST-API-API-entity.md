---
title: "Azure API Management REST API API entity"
ms.custom: na
ms.date: 2016-09-22
ms.prod: azure
ms.reviewer: na
ms.service: api-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: f6edf95f-f1ba-439b-9010-c4a96ec14d48
caps.latest.revision: 28
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
# Azure API Management REST API API entity
This topic describes how to manage APIs and their operations using the API Management REST API.  
  
 For more information about working with APIs and operations in the publisher portal, see [How to create APIs, operations, and products in Azure API Management](http://go.microsoft.com/fwlink/?LinkId=510414).  
  
 For more information about working with the REST API, see the [API Management .NET REST API Sample](https://github.com/Azure/api-management-samples/tree/master/restApiDemo) and the [Getting Started with Azure API Management REST API](http://azure.microsoft.com/documentation/videos/getting-started-with-azure-api-management-rest-api/) video.  
  
## In this topic  
  
-   [Prerequisites](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#Prerequisites)  
  
-   [Get a list of all APIs](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#ListAPIs)  
  
-   [Get a specific API](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#GetAPI)  
  
-   [Get the metadata for a specific API](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#GetAPIMetadata)  
  
-   [Create or import a new API](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#CreateAPI)  
  
-   [Update an API via import](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#ImportExisting)  
  
-   [Update an API](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#UpdateAPI)  
  
-   [Delete an API](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#DeleteAPI)  
  
-   [Get a list of all operations for a specific API](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#ListOperations)  
  
-   [Get a specific operation](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#GetOperation)  
  
-   [Get the metadata for a specific operation](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#GetOperationMetadata)  
  
-   [Create a new operation](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#CreateOperation)  
  
-   [Update an operation](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#UpdateOperation)  
  
-   [Delete an operation](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#DeleteOperation)  
  
-   [Get policy for an operation](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#GetOperationPolicy)  
  
-   [Check for policy on an operation](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#CheckOperationPolicy)  
  
-   [Set policy for an operation](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#SetOperationPolicy)  
  
-   [Remove policy configuration from an operation](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#RemoveOperationPolicy)  
  
-   [Get policy for an API](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#GetAPIPolicy)  
  
-   [Check for policy on an API](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#CheckAPIPolicy)  
  
-   [Set policy on an API](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#SetAPIPolicy)  
  
-   [Remove policy configuration from an API](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#RemoveAPIPolicy)  
  
##  <a name="Prerequisites"></a> Prerequisites  
  
> [!IMPORTANT]
>  Before making any calls into the API Management REST API, please review the [Prerequisites](../ApiManagementREST/API-Management-REST.md#Prerequisites) section of the [API Management REST](../ApiManagementREST/API-Management-REST.md) guide. This specifies the necessary authentication, version parameters, supported media types, and other information required in order to successfully call the API Management REST API.  
  
##  <a name="ListAPIs"></a> Get a list of all APIs  
 This operation returns a collection of all APIs in the specified service instance.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/apis|  
  
#### Request Parameters  
 None.  
  
#### Request Headers  
 None.  
  
#### Request Body  
 None.  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|You can filter the results using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported<br /><br /> id:<br /><br /> - ge, le, eq, ne, gt, lt: substringof, startswith, endswith<br /><br /> name:<br /><br /> - ge, le, eq, ne, gt, lt: substringof, startswith, endswith<br /><br /> description:<br /><br /> - ge, le, eq, ne, gt, lt: substringof, startswith, endswith<br /><br /> serviceUrl:<br /><br /> - ge, le, eq, ne, gt, lt: substringof, startswith, endswith<br /><br /> path:<br /><br /> - ge, le, eq, ne, gt, lt: substringof, startswith, endswith|  
|$top|string|The number of entities to return.|  
|$skip|string|The number of entities to skip.|  
  
### Responses  
  
#### 200 OK  
 A [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of the [API](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#API) entities for the specified API Management service instance.  
  
##### Sample response body  
  
```json  
{  
  "value": [  
    {  
      "id": "/apis/54ff046ff0be6b0c94ccfb2f",  
      "name": "Basic Calculator",  
      "description": "Arithmetics is just a call away!",  
      "serviceUrl": "http://calcapi.cloudapp.net/api",  
      "path": "calc",  
      "protocols": [  
        "https"  
      ]  
    },  
    {  
      "id": "/apis/5480c157f0be6b10ac965a76",  
      "name": "Contoso API",  
      "description": null,  
      "serviceUrl": "http://api.contoso.com",  
      "path": "contosoapi",  
      "protocols": [  
        "https"  
      ]  
    },  
    {  
      "id": "/apis/53c765632095310385040001",  
      "name": "Echo API",  
      "description": null,  
      "serviceUrl": "http://echoapi.cloudapp.net/api",  
      "path": "echo",  
      "protocols": [  
        "https"  
      ]  
    },  
    {  
      "id": "/apis/54d913208ad1c9037c46876a",  
      "name": "Salesforce REST API",  
      "description": "OAuth demo service.",  
      "serviceUrl": "https://na17.salesforce.com/services/data/v20.0",  
      "path": "salesforce",  
      "protocols": [  
        "https"  
      ]  
    }  
  ],  
  "count": 4,  
  "nextLink": null  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="GetAPI"></a> Get a specific API  
 This operation returns the details of the API specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/apis/{aid}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|aid|string|API identifier.|  
  
#### Request Headers  
  
|Request Header|Description|  
|--------------------|-----------------|  
|Accept|If the `export` query parameter described in the following section is set to `true`, then the `Accept` header can be set to `application/vnd.sun.wadl+xml`, `application/vnd.swagger.doc+json`, or `application/json`; otherwise it must be either omitted or set to `application/json`.|  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|export|boolean|The `export` query parameters can have one of the following values.<br /><br /> -                             `true` - The response contains full set of API metadata and includes API entity with an embedded array of operation entities. The following media types can be specified in the `Accept` request header: `application/vnd.sun.wadl+xml`, `application/vnd.swagger.doc+json`, or `application/json`.<br /><br /> -                              `false` - The response includes only the API entity in `application/json` format. If the `export` query parameter is not present the default value is `false`.|  
  
#### Request Body  
 None.  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The response headers contain the following metatada about the API.  
  
|Headers|||  
|-------------|-|-|  
|ETag|string|Current entity state version. Should be treated as opaque and used to make conditional HTTP requests.|  
  
 The response body contains the specified [API](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#API) entity.  
  
##### Sample response body with export=false  
  
```json  
{  
  "id": "/apis/53c765632095310385040001",  
  "name": "Echo API",  
  "description": null,  
  "serviceUrl": "http://echoapi.cloudapp.net/api",  
  "path": "echo",  
  "protocols": [  
    "https"  
  ],  
  "authenticationSettings": {  
    "oAuth2": null  
  },  
  "subscriptionKeyParameterNames": {  
    "header": "Ocp-Apim-Subscription-Key",  
    "query": "subscription-key"  
  }  
}  
```  
  
##### Sample response body with export=true in application/json  
  
```json  
{  
  "id": "/apis/53c765632095310385040001",  
  "name": "Echo API",  
  "description": null,  
  "serviceUrl": "http://echoapi.cloudapp.net/api",  
  "path": "echo",  
  "protocols": [  
    "https"  
  ],  
  "operations": {  
    "value": [  
      {  
        "id": "/apis/53c765632095310385040001/operations/53c765632095310385080005",  
        "name": "DELETE Resource",  
        "method": "DELETE",  
        "urlTemplate": "/resource",  
        "templateParameters": [],  
        "description": "A demonstration of a DELETE call which traditionally deletes the resource. It is based on the same \"echo\" backend as in all other operations so nothing is actually deleted.",  
        "request": {  
          "description": null,  
          "queryParameters": [],  
          "headers": [],  
          "representations": []  
        },  
        "responses": [  
          {  
            "statusCode": 200,  
            "description": null,  
            "representations": []  
          }  
        ]  
      },  
      {  
        "id": "/apis/53c765632095310385040001/operations/53c765632095310385080001",  
        "name": "GET Resource",  
        "method": "GET",  
        "urlTemplate": "/resource",  
        "templateParameters": [],  
        "description": "A demonstration of a GET call on a sample resource. It is handled by an \"echo\" backend which returns a response equal to the request (the supplied headers and body are being returned as received).",  
        "request": {  
          "description": null,  
          "queryParameters": [  
            {  
              "name": "param1",  
              "description": "A sample parameter that is required and has a default value of \"sample\".",  
              "type": "string",  
              "defaultValue": "sample",  
              "required": false,  
              "values": [  
                "sample"  
              ]  
            },  
            {  
              "name": "param2",  
              "description": "Another sample parameter, set to not required.",  
              "type": "number",  
              "defaultValue": null,  
              "required": false,  
              "values": []  
            }  
          ],  
          "headers": [],  
          "representations": []  
        },  
        "responses": [  
          {  
            "statusCode": 200,  
            "description": "Returned in all cases.",  
            "representations": []  
          }  
        ]  
      },  
      {  
        "id": "/apis/53c765632095310385040001/operations/53c765632095310385080002",  
        "name": "GET Resource (cached)",  
        "method": "GET",  
        "urlTemplate": "/resource-cached",  
        "templateParameters": [],  
        "description": "A demonstration of a GET call with caching enabled on the same \"echo\" backend as above. Cache TTL is set to 1 hour. When you make thefirst request the headers you supplied will be cached. Subsequent calls will return the same headers as the first time even if you change them in your request.",  
        "request": {  
          "description": null,  
          "queryParameters": [  
            {  
              "name": "param1",  
              "description": "A sample parameter that is required and has a defa  
ult value of \"sample\".",  
              "type": "string",  
              "defaultValue": "sample",  
              "required": false,  
              "values": [  
                "sample"  
              ]  
            },  
            {  
              "name": "param2",  
              "description": "Another sample parameter, set to not required.",  
              "type": "string",  
              "defaultValue": null,  
              "required": false,  
              "values": []  
            }  
          ],  
          "headers": [],  
          "representations": []  
        },  
        "responses": [  
          {  
            "statusCode": 200,  
            "description": null,  
            "representations": []  
          }  
        ]  
      },  
      {  
        "id": "/apis/53c765632095310385040001/operations/53c765632095310385080006",  
        "name": "HEAD Resource",  
        "method": "HEAD",  
        "urlTemplate": "/resource",  
        "templateParameters": [],  
        "description": "The HEAD operation returns only headers. In this demonstration a policy is used to set additional headers when the response is returned and to enable JSONP.",  
        "request": {  
          "description": null,  
          "queryParameters": [],  
          "headers": [],  
          "representations": []  
        },  
        "responses": [  
          {  
            "statusCode": 200,  
            "description": null,  
            "representations": []  
          }  
        ]  
      },  
      {  
        "id": "/apis/53c765632095310385040001/operations/53c765632095310385080004",  
        "name": "POST Resource",  
        "method": "POST",  
        "urlTemplate": "/resource",  
        "templateParameters": [],  
        "description": "A demonstration of a POST call based on the echo backend above. The request body is expected to contain JSON-formatted data (see example below). A policy is used to automatically transform any request sent in JSON directly to XML. In a real-world scenario this could be used to enable modern clients to speak to a legacy backend.",  
        "request": {  
          "description": null,  
          "queryParameters": [],  
          "headers": [],  
          "representations": [  
            {  
              "contentType": "application/json",  
              "sample": "{\r\n\t\t\t\"vehicleType\": \"train\",\r\n\t\t\t\"maxSp  
eed\": 125,\r\n\t\t\t\"avgSpeed\": 90,\r\n\t\t\t\"speedUnit\": \"mph\"\r\n\t\t}"  
  
            }  
          ]  
        },  
        "responses": [  
          {  
            "statusCode": 200,  
            "description": null,  
            "representations": []  
          }  
        ]  
      },  
      {  
        "id": "/apis/53c765632095310385040001/operations/53c765632095310385080003",  
        "name": "PUT Resource",  
        "method": "PUT",  
        "urlTemplate": "/resource",  
        "templateParameters": [],  
        "description": "A demonstration of a PUT call handled by the same \"echo\" backend as above. You can now specify a request body in addition to headers and it will be returned as well.",  
        "request": {  
          "description": null,  
          "queryParameters": [],  
          "headers": [],  
          "representations": []  
        },  
        "responses": [  
          {  
            "statusCode": 200,  
            "description": null,  
            "representations": []  
          }  
        ]  
      }  
    ],  
    "count": 6,  
    "nextLink": null  
  },  
  "authenticationSettings": {  
    "oAuth2": null  
  },  
  "subscriptionKeyParameterNames": {  
    "header": "Ocp-Apim-Subscription-Key",  
    "query": "subscription-key"  
  }  
}  
```  
  
##### Sample response body with export=true in application/vnd.sun.wadl+xml  
  
```xml  
<application xmlns="http://wadl.dev.java.net/2009/02" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://wadl.dev.java.net/2009/02 http://www.w3.org/Submission/wadl/wadl.xsd">  
    <doc title="Echo API">Echoes back response headers and body.</doc>  
    <resources base="http://echoapi.cloudapp.net/api">  
        <resource path="/resource">  
            <doc title="DELETE Resource">A demonstration of a DELETE call which traditionally deletes the resource. It is based on the same "echo" backend as in all other operations so nothing is actually deleted.  
            </doc>  
            <method name="DELETE">  
                <request>  
                    <doc>A demonstration of a DELETE call which traditionally deletes the resource. It is based on the same "echo" backend as in all other operations so nothing is actually deleted.  
                    </doc>  
                </request>  
                <response status="200"/>  
            </method>  
        </resource>  
        <resource path="/resource">  
            <doc title="GET Resource">A demonstration of a GET call on a sample resource. It is handled by an "echo" backend which returns a response equal to the request (the supplied headers and body are being returned as received).  
            </doc>  
            <method name="GET">  
                <request>  
                    <doc>A demonstration of a GET call on a sample resource. It is handled by an "echo" backend which returns a response equal to the request (the supplied headers and body are being returned as received).  
                    </doc>  
                    <param default="sample" name="param1" style="query" type="xs:string">  
                        <doc>A sample parameter that is required and has a default value of "sample".</doc>  
                        <option value="sample"/>  
                    </param>  
                    <param name="param2" style="query" type="xs:number">  
                        <doc>Another sample parameter, set to not required.</doc>  
                    </param>  
                </request>  
                <response status="200">  
                    <doc>Returned in all cases.</doc>  
                </response>  
            </method>  
        </resource>  
        <resource path="/resource-cached">  
            <doc title="GET Resource (cached)">A demonstration of a GET call with caching enabled on the same "echo" backend as above. Cache TTL is set to 1 hour. When you make the first request the headers you supplied will be cached. Subsequent calls will return the same headers as the first time even if you change them in your request.  
            </doc>  
            <method name="GET">  
                <request>  
                    <doc>A demonstration of a GET call with caching enabled on the same "echo" backend as above. Cache TTL is set to 1 hour. When you make the first request the headers you supplied will be cached. Subsequent calls will return the same headers as the first time even if you change them in your request.  
                    </doc>  
                    <param default="sample" name="param1" style="query" type="xs:string">  
                        <doc>A sample parameter that is required and has a default value of "sample".</doc>  
                        <option value="sample"/>  
                    </param>  
                    <param name="param2" style="query" type="xs:string">  
                        <doc>Another sample parameter, set to not required.</doc>  
                    </param>  
                </request>  
                <response status="200"/>  
            </method>  
        </resource>  
        <resource path="/resource">  
            <doc title="HEAD Resource">The HEAD operation returns only headers. In this demonstration a policy is used to set additional headers when the response is returned and to enable JSONP.  
            </doc>  
            <method name="HEAD">  
                <request>  
                    <doc>The HEAD operation returns only headers. In this demonstration a policy is used to set additional headers when the response is returned and to enable JSONP.  
                    </doc>  
                </request>  
                <response status="200"/>  
            </method>  
        </resource>  
        <resource path="/resource">  
            <doc title="POST Resource">A demonstration of a POST call based on the echo backend above. The request body is expected to contain JSON-formatted data (see example below). A policy is used to automatically transform any request sent in JSON directly to XML. In a real-world scenario this could be used to enable modern clients to speak to a legacy backend.  
            </doc>  
            <method name="POST">  
                <request>  
                    <doc>A demonstration of a POST call based on the echo backend above. The request body is expected to contain JSON-formatted data (see example below). A policy is used to automatically transform any request sent in JSON directly to XML. In a real-world scenario this could be used to enable modern clients to speak to a legacy backend.  
                    </doc>  
                    <representation mediaType="application/json">  
                        <doc>{ "vehicleType": "train", "maxSpeed": 125, "avgSpeed": 90, "speedUnit": "mph" }</doc>  
                    </representation>  
                </request>  
                <response status="200"/>  
            </method>  
        </resource>  
        <resource path="/resource">  
            <doc title="PUT Resource">A demonstration of a PUT call handled by the same "echo" backend as above. You can now specify a request body in addition to headers and it will be returned as well.  
            </doc>  
            <method name="PUT">  
                <request>  
                    <doc>A demonstration of a PUT call handled by the same "echo" backend as above. You can now specify a request body in addition to headers and it will be returned as well.  
                    </doc>  
                </request>  
                <response status="200"/>  
            </method>  
        </resource>  
    </resources>  
</application>  
```  
  
##### Sample response body with export=true in application/vnd.swagger.doc+json  
  
```json  
{  
  "swaggerVersion": "1.2",  
  "basePath": "http://echoapi.cloudapp.net/api",  
  "apis": [  
    {  
      "path": "/resource",  
      "operations": [  
        {  
          "method": "DELETE",  
          "parameters": [],  
          "nickname": "DELETE Resource",  
          "summary": "A demonstration of a DELETE call which traditionally deletes the resource. It is based on the same \"echo\" backend as in all other operations so nothing is actually deleted.",  
          "errorResponses": [  
            {  
              "code": 200  
            }  
          ]  
        }  
      ]  
    },  
    {  
      "path": "/resource",  
      "operations": [  
        {  
          "method": "GET",  
          "parameters": [  
            {  
              "name": "param1",  
              "paramType": "query",  
              "dataType": "string",  
              "description": "A sample parameter that is required and has a default value of \"sample\".",  
              "defaultValue": "sample",  
              "allowableValues": {  
                "valueType": "LIST",  
                "values": [  
                  "sample"  
                ]  
              }  
            },  
            {  
              "name": "param2",  
              "paramType": "query",  
              "dataType": "number",  
              "description": "Another sample parameter, set to not required."  
            }  
          ],  
          "nickname": "GET Resource",  
          "summary": "A demonstration of a GET call on a sample resource. It is handled by an \"echo\" backend which returns a response equal to the request (the supplied headers and body are being returned as received).",  
          "errorResponses": [  
            {  
              "code": 200,  
              "reason": "Returned in all cases."  
            }  
          ]  
        }  
      ]  
    },  
    {  
      "path": "/resource-cached",  
      "operations": [  
        {  
          "method": "GET",  
          "parameters": [  
            {  
              "name": "param1",  
              "paramType": "query",  
              "dataType": "string",  
              "description": "A sample parameter that is required and has a default value of \"sample\".",  
              "defaultValue": "sample",  
              "allowableValues": {  
                "valueType": "LIST",  
                "values": [  
                  "sample"  
                ]  
              }  
            },  
            {  
              "name": "param2",  
              "paramType": "query",  
              "dataType": "string",  
              "description": "Another sample parameter, set to not required."  
            }  
          ],  
          "nickname": "GET Resource (cached)",  
          "summary": "A demonstration of a GET call with caching enabled on the same \"echo\" backend as above. Cache TTL is set to 1 hour. When you make the first request the headers you supplied will be cached. Subsequent calls will return the same headers as the first time even if you change them in your request.",  
          "errorResponses": [  
            {  
              "code": 200  
            }  
          ]  
        }  
      ]  
    },  
    {  
      "path": "/resource",  
      "operations": [  
        {  
          "method": "HEAD",  
          "parameters": [],  
          "nickname": "HEAD Resource",  
          "summary": "The HEAD operation returns only headers. In this demonstration a policy is used to set additional headers when the response is returned and to enable JSONP.",  
          "errorResponses": [  
            {  
              "code": 200  
            }  
          ]  
        }  
      ]  
    },  
    {  
      "path": "/resource",  
      "operations": [  
        {  
          "method": "POST",  
          "parameters": [],  
          "nickname": "POST Resource",  
          "summary": "A demonstration of a POST call based on the echo backend above. The request body is expected to contain JSON-formatted data (see example below). A policy is used to automatically transform any request sent in JSON directly to XML. In a real-world scenario this could be used to enable modern clients to speak to a legacy backend.",  
          "errorResponses": [  
            {  
              "code": 200  
            }  
          ]  
        }  
      ]  
    },  
    {  
      "path": "/resource",  
      "operations": [  
        {  
          "method": "PUT",  
          "parameters": [],  
          "nickname": "PUT Resource",  
          "summary": "A demonstration of a PUT call handled by the same \"echo\" backend as above. You can now specify a request body in addition to headers and it will be returned as well.",  
          "errorResponses": [  
            {  
              "code": 200  
            }  
          ]  
        }  
      ]  
    }  
  ],  
  "models": {},  
  "info": {  
    "title": "Echo API",  
    "description": "Echoes back response headers and body."  
  }  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified API does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="GetAPIMetadata"></a> Get the metadata for a specific API  
 This operation returns the metadata for the API specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|HEAD|/apis/{aid}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|aid|string|API identifier.|  
  
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
 The specified API does not exist.  
  
##  <a name="CreateAPI"></a> Create or import a new API  
 This operation creates or a new API directly or by importing an API description in one of the supported formats.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PUT|/apis/{aid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|aid|string|API identifier. Must be unique in the current API Management service instance. Maximum length is 256 characters.|  
  
####  <a name="CreateAPIRequestHeaders"></a> Request Headers  
  
|Request Header|Description|  
|--------------------|-----------------|  
|Content-Type|If the `import` query parameter described in the following section is set to `true`, then the `Content-Type` request header can be set to one of the following values.<br /><br /> - `application/vnd.sun.wadl+xml`<br /><br /> -                                     `application/vnd.swagger.doc+json`<br /><br /> -                                     `application/json`<br /><br /> These media types are used when the API metadata is provided in the body of the request.<br /><br /> -                                     `application/vnd.swagger.link+json`<br /><br /> - `application/vnd.sun.wadl.link+json`<br /><br /> These media types are used when the API metadata is provided via a link in the body of the request in the following format. <br />`{`<br />`"link" : http://contoso.com/myapi/metadata`<br />`}`<br /><br /> If the `import` query parameter is set to `false` the `Content-Type` request header should be set to `application/json` or omitted.<br /><br /> For more information about the `import` query parameter, see the `import` query parameter in the following [Query Parameters](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#ImportQueryParameters) section.|  
  
####  <a name="ImportQueryParameters"></a> Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|import|boolean|The `import` query parameter is optional and can have one of the following values. If the `import` query parameter is missing the default value is `false`.<br /><br /> -                             `true` - The request body must contain either API metadata or a link to API metadata.<br /><br /> -                             `false` – The request must contain the body specified in the following **Request body** section.<br /><br /> For information on the supported media types for these requests, see the `Content-Type` header documentation in the previous [Request Headers](../ApiManagementREST/Azure-API-Management-REST-API-API-entity.md#CreateAPIRequestHeaders) section.|  
|path|string|This parameter must be present only if the `import` parameter is set to `true`.<br /><br /> Relative URL uniquely identifying this API and all of it resource paths within the API Management service instance. It is appended to the API endpoint base URL specified during the service instance creation to form a public URL for this API.|  
  
#### Request body  
 The request body contains a [API](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#API) entity. For a complete list of eligible properties for this operation, see the [API](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#API) properties in the [Contract reference](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md).  
  
### Responses  
 This operation has the following responses.  
  
#### 201 Created  
 API was successfully created.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 409 Conflict  
 API with the same identifier already exists.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="ImportExisting"></a> Update an API via import  
 This operation updates an API by importing an API description in one of the supported formats.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PUT|/apis/{aid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|aid|string|API identifier.|  
  
#### Request Headers  
  
|Request Header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the API to update. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
|Content-Type|If the `import` query parameter described in the following section is set to `true`, then the `Content-Type` request header can be set to one of the following values.<br /><br /> -                                     `application/vnd.sun.wadl+xml`<br /><br /> -                                     `application/vnd.swagger.doc+json`<br /><br /> -                                     `application/json`<br /><br /> These media types are used when the API metadata is provided in the body of the request.<br /><br /> -                                     `application/vnd.swagger.link+json`<br /><br /> -                                     `application/vnd.sun.wadl.link+json`<br /><br /> These media types are used when the API metadata is provided via a link in the body of the request in the following format. <br />`{`<br />`"link" : http://contoso.com/myapi/metadata`<br />`}`|  
  
#### Request body  
 The request body contains a [API](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#API) entity. For a complete list of eligible properties for this operation, see the [API](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#API) properties in the [Contract reference](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md).  
  
> [!NOTE]
>  This request body representation is used only when `Content-Type` is set to `application/json`.  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The API was successfully imported.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the resource doesn't pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="UpdateAPI"></a> Update an API  
 This operation updates the details of the API specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PATCH|/apis/{aid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|aid|string|API identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the API to update. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
#### Request Body  
 The request body contains a [API](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#API) entity. For a complete list of eligible properties for this operation, see the [API](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#API) properties in the [Contract reference](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md).  
  
 Only [API](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#API) properties being updated may be specified in the request body.  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The API settings were successfully updated.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified API doesn’t exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="DeleteAPI"></a> Delete an API  
 This operation deletes the specified API.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|DELETE|/apis/{aid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|aid|string|API identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the API to delete. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The API was successfully deleted.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the product resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="ListOperations"></a> Get a list of all operations for a specific API  
 This operation returns a collection of the operations for the specified API.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/apis/{aid}/operations|  
  
#### Request Parameters  
 None.  
  
#### Request Headers  
 None.  
  
#### Request Body  
 None.  
  
#### Query Parameters  
  
|Query Parameter|Type|Description|  
|---------------------|----------|-----------------|  
|$filter|string|You can filter the results using OData filter expression [syntax](http://docs.oasis-open.org/odata/odata/v4.0/os/part2-url-conventions/odata-v4.0-os-part2-url-conventions.html#_Toc372793792). The following fields and operators are supported<br /><br /> name:<br /><br /> - ge, le, eq, ne, gt, lt: substringof, startswith, endswith<br /><br /> method:<br /><br /> - ge, le, eq, ne, gt, lt: substringof, startswith, endswith<br /><br /> description:<br /><br /> - ge, le, eq, ne, gt, lt: substringof, startswith, endswith<br /><br /> urlTemplate:<br /><br /> - ge, le, eq, ne, gt, lt: substringof, startswith, endswith|  
|$top|string|The number of entities to return.|  
|$skip|string|The number of entities to skip.|  
  
### Responses  
  
#### 200 OK  
 A [Collection](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#collection) of the [Operation-summary](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#OperationSummaryProperties) entities for the specified API.  
  
##### Sample response body  
  
```json  
{  
  "value": [  
    {  
      "id": "/apis/53ee171a9d3ea90381040001/operations/53ee171a9d3ea90381080005",  
      "name": "DELETE Resource",  
      "method": "DELETE",  
      "urlTemplate": "/resource",  
      "description": "A demonstration of a DELETE call which traditionally deletes the resource. It is based on the same \"echo\" backend as in all other operations so nothing is actually deleted."  
    },  
    {  
      "id": "/apis/53ee171a9d3ea90381040001/operations/53ee171a9d3ea90381080001",  
      "name": "GET Resource",  
      "method": "GET",  
      "urlTemplate": "/resource",  
      "description": "A demonstration of a GET call on a sample resource. It is handled by an \"echo\" backend which returns a response equal to the request (the supplied headers and body are being returned as received)."  
    },  
    {  
      "id": "/apis/53ee171a9d3ea90381040001/operations/53ee171a9d3ea90381080002",  
      "name": "GET Resource (cached)",  
      "method": "GET",  
      "urlTemplate": "/resource-cached",  
      "description": "A demonstration of a GET call with caching enabled on the same \"echo\" backend as above. Cache TTL is set to 1 hour. When you make the first request the headers you supplied will be cached. Subsequent calls will return the same headers as the first time even if you change them in your request."  
    },  
    {  
      "id": "/apis/53ee171a9d3ea90381040001/operations/53ee171a9d3ea90381080006",  
      "name": "HEAD Resource",  
      "method": "HEAD",  
      "urlTemplate": "/resource",  
      "description": "The HEAD operation returns only headers. In this demonstration a policy is used to set additional headers when the response is returned and to enable JSONP."  
    },  
    {  
      "id": "/apis/53ee171a9d3ea90381040001/operations/53ee171a9d3ea90381080004",  
      "name": "POST Resource",  
      "method": "POST",  
      "urlTemplate": "/resource",  
      "description": "A demonstration of a POST call based on the echo backend above. The request body is expected to contain JSON-formatted data (see example below). A policy is used to automatically transform any request sent in JSON directly to XML. In a real-world scenario this could be used to enable modern clients to speak to a legacy backend."  
    },  
    {  
      "id": "/apis/53ee171a9d3ea90381040001/operations/53ee171a9d3ea90381080003",  
      "name": "PUT Resource",  
      "method": "PUT",  
      "urlTemplate": "/resource",  
      "description": "A demonstration of a PUT call handled by the same \"echo\" backend as above. You can now specify a request body in addition to headers and it will be returned as well."  
    }  
  ],  
  "count": 6,  
  "nextLink": null  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="GetOperation"></a> Get a specific operation  
 This operation returns the details of the API specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/apis/{aid}/operations/{oid}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|aid|string|API identifier.|  
|oid|string|Operation identifier.|  
  
#### Request Body  
 None.  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The response headers contain the following metatada about the API.  
  
|Headers|||  
|-------------|-|-|  
|ETag|string|Current entity state version. Should be treated as opaque and used to make conditional HTTP requests.|  
  
 The response body contains the specified [Operation](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Operation) entity.  
  
##### Sample response body  
  
```json  
{  
  "id": "/apis/53ee1e1bb84c1a0d304496ce/operations/53ee1e1cb84c1a0cc462557f",  
  "name": "Add two integers",  
  "method": "GET",  
  "urlTemplate": "/add",  
  "templateParameters": [],  
  "description": "Produce sum of two numbers.",  
  "request": {  
    "description": null,  
    "queryParameters": [  
      {  
        "name": "a",  
        "description": "First operand. Default value is <code>51</code>.",  
        "type": "integer",  
        "defaultValue": "51",  
        "required": true,  
        "values": [  
          "51"  
        ]  
      },  
      {  
        "name": "b",  
        "description": "Second operand. Default value is <code>49</code>.",  
        "type": "integer",  
        "defaultValue": "49",  
        "required": true,  
        "values": [  
          "49"  
        ]  
      }  
    ],  
    "headers": [],  
    "representations": []  
  },  
  "responses": [  
    {  
      "statusCode": 200,  
      "description": null,  
      "representations": [  
        {  
          "contentType": "application/xml",  
          "sample": "<result>\n   <value>100</value>\n   <broughtToYouBy>Azure API Management - http://api.azure.com/</broughtToYouBy>\n</result>"  
        },  
        {  
          "contentType": "application/json",  
          "sample": "{\n   \"result\":\n    {\n        \"value\":\"100\",\n        \"broughtToYouBy\":\"Azure API Management - http://api.azure.com/ \"\n    }\n}"  
        }  
      ]  
    }  
  ]  
}  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified operation does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="GetOperationMetadata"></a> Get the metadata for a specific operation  
 This operation returns the details of the API specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|HEAD|/apis/{aid}/operations/{oid}|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|aid|string|API identifier.|  
|oid|string|Operation identifier.|  
  
#### Request Body  
 None.  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The response headers contain the following metatada about the API.  
  
|Headers|||  
|-------------|-|-|  
|ETag|string|Current entity state version. Should be treated as opaque and used to make conditional HTTP requests.|  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified operation does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="CreateOperation"></a> Create a new operation  
 This operation creates a new operation.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PUT|/apis/{aid}/operations/{oid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|aid|string|API identifier.|  
|oid|string|Operation identifier. Must be unique in the current API Management service instance. Maximum length is 256 characters.|  
  
#### Request body  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|name|string|Name of the operation. Must not be empty. Maximum length is 100 characters.|  
|method|string|Operation HTTP method.|  
|urlTemplate|string|Operation URI template. Contains relative URI to entity being referenced.|  
|description|string|Description of the API. Must not be empty. May include HTML formatting tags. Maximum length is 1000 characters.|  
|request|string|Operation request.|  
|responses|string|Array of operation responses.|  
  
### Responses  
 This operation has the following responses.  
  
#### 201 Created  
 Operation was successfully created.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified API doesn’t exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 409 Conflict  
 Operation with the same identifier already exists.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="UpdateOperation"></a> Update an operation  
 This operation updates the details of the operation specified by its identifier.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PATCH|/apis/{aid}/operations/{oid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|aid|string|API identifier.|  
|oid|string|Operation identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the operation to update. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
#### Request Body  
 Only operation properties being updated may be specified in the request body.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|name|string|Name of the API. Must not be empty. Maximum length is 100 characters.|  
|method|string|Operation HTTP method.|  
|urlTemplate|string|Operation URI template. Contains relative URI to entity being referenced.|  
|description|string|Description of the API. Must not be empty. May include HTML formatting tags. Maximum length is 1000 characters.|  
|request|string|Operation request.|  
|responses|string|Array of operation responses.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The operation was successfully updated.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified API or operation doesn’t exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the operation resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="DeleteOperation"></a> Delete an operation  
 This operation deletes the specified operation.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|DELETE|/apis/{aid}/operations/{oid}|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|aid|string|API identifier.|  
|oid|string|Operation identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the operation to delete. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The operation was successfully deleted.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The API or operation does not exist.  
  
#### 412 Precondition Failed  
 Returned if the resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="GetOperationPolicy"></a> Get policy for an operation  
 This operation returns the policy configuration for the specified operation.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/apis/{aid}/operations/{oid}/policy|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|aid|string|API identifier.|  
|oid|string|Operation identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The response headers contain the following metatada about the operation.  
  
|Headers|||  
|-------------|-|-|  
|ETag|string|Current entity state version.|  
  
 The response body contains a [Policy](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Policy) response type. The media type for this response is `application/vnd.ms-azure-apim.policy+xml`.  
  
##### Sample response body  
  
```xml  
<policies>  
  <inbound>  
    <base/>  
    <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">  
      <vary-by-header>Accept</vary-by-header>  
      <vary-by-header>Accept-Charset</vary-by-header>  
    </cache-lookup>  
    <rewrite-uri template="/resource"/>  
  </inbound>  
  <outbound>  
    <base/>  
    <cache-store caching-mode="cache-on" duration="3600"/>  
  </outbound>  
</policies>  
  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified operation does not exist or there is no policy attached.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="CheckOperationPolicy"></a> Check for policy on an operation  
 This operation determines if policy configuration is attached to the specified operation.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|HEAD|/apis/{aid}/operations/{oid}/policy|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|aid|string|API identifier.|  
|oid|string|Operation identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 Policy configuration is attached to the specified operation.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not found  
 The specified operation does not exist or there is no policy configuration attached.  
  
##  <a name="SetOperationPolicy"></a> Set policy for an operation  
 This operation sets the policy configuration for the specified operation.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PUT|/apis/{aid}/operations/{oid}/policy|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|aid|string|API identifier.|  
|oid|string|Operation identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the operation to update. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
|Content-Type|Possible values are `application/vnd.ms-azure-apim.policy+xml` and `application/vnd.ms-azure-apim.policy.raw+xml`.<br /><br /> When using `application/vnd.ms-azure-apim.policy+xml`, expressions contained within the policy must be XML-escaped.<br /><br /> When using `application/vnd.ms-azure-apim.policy.raw+xml` no escaping is necessary.|  
  
#### Request Body  
 The request body is the desired [Policy](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Policy) representation.  
  
##### Sample request body  
  
```xml  
<policies>  
  <inbound>  
    <base/>  
    <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">  
      <vary-by-header>Accept</vary-by-header>  
      <vary-by-header>Accept-Charset</vary-by-header>  
    </cache-lookup>  
    <rewrite-uri template="/resource"/>  
  </inbound>  
  <outbound>  
    <base/>  
    <cache-store caching-mode="cache-on" duration="3600"/>  
  </outbound>  
</policies>  
  
```  
  
### Responses  
 This operation has the following responses.  
  
#### 201 Created  
 The policy configuration was successfully attached to the operation.  
  
#### 204 No Content  
 The existing policy configuration was successfully replaced.  
  
#### 400 Bad Request  
 Request validation failed. The typical cause is that the API or operation doesn't exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the policy resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="RemoveOperationPolicy"></a> Remove policy configuration from an operation  
 This operation removes the policy configuration for the specified operation.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|DELETE|/apis/{aid}/operations/{oid}/policy|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|aid|string|API identifier.|  
|oid|string|Operation identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the operation. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The policy configuration was successfully removed from the operation.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified operation does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="GetAPIPolicy"></a> Get policy for an API  
 This operation returns the policy configuration for the specified API.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|GET|/apis/{aid}/policy|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|aid|string|API identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 The response headers contain the following metatada about the API.  
  
|Headers|||  
|-------------|-|-|  
|ETag|string|Current entity state version.|  
  
 The response body contains a [Policy](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Policy) response type. The media type for this response is `application/vnd.ms-azure-apim.policy+xml`.  
  
##### Sample response body  
  
```xml  
<policies>  
  <inbound>  
    <base/>  
  </inbound>  
  <outbound>  
    <base/>  
    <xml-to-json apply="content-type-xml" consider-accept-header="true" kind="direct"/>  
  </outbound>  
</policies>  
```  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified API does not exist or there is no policy attached.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="CheckAPIPolicy"></a> Check for policy on an API  
 This operation determines if policy configuration is attached to the specified API.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|HEAD|/apis/{aid}/policy|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|aid|string|API identifier.|  
  
### Responses  
 This operation has the following responses.  
  
#### 200 OK  
 Policy configuration is attached to the specified API.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not found  
 The specified API does not exist or there is no policy configuration attached.  
  
##  <a name="SetAPIPolicy"></a> Set policy on an API  
 This operation sets the policy configuration for the specified API.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|PUT|/apis/{aid}/policy|  
  
#### Request Parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|aid|string|API identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the API to update. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
|Content-Type|Possible values are `application/vnd.ms-azure-apim.policy+xml` and `application/vnd.ms-azure-apim.policy.raw+xml`.<br /><br /> When using `application/vnd.ms-azure-apim.policy+xml`, expressions contained within the policy must be XML-escaped.<br /><br /> When using `application/vnd.ms-azure-apim.policy.raw+xml` no escaping is necessary.|  
  
#### Request Body  
 The request body is the desired [Policy](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#Policy) representation.  
  
##### Sample request body  
  
```xml  
<policies>  
  <inbound>  
    <base/>  
  </inbound>  
  <outbound>  
    <base/>  
    <xml-to-json apply="content-type-xml" consider-accept-header="true" kind="direct"/>  
  </outbound>  
</policies>  
```  
  
### Responses  
 This operation has the following responses.  
  
#### 201 Created  
 The policy configuration was successfully attached to the operation.  
  
#### 204 No Content  
 The existing policy configuration was successfully replaced with the new policy.  
  
#### 400 Bad Request  
 Request validation failed. The typical cause is that the API doesn't exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified API does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the policy resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
##  <a name="RemoveAPIPolicy"></a> Remove policy configuration from an API  
 This operation removes the policy configuration from the specified API.  
  
### Request  
  
|HTTP Method|Relative Request URI|  
|-----------------|--------------------------|  
|DELETE|/apis/{aid}/policy|  
  
#### Request parameters  
  
|Request Parameter|Type|Description|  
|-----------------------|----------|-----------------|  
|aid|string|API identifier.|  
  
#### Request Headers  
  
|Request header|Description|  
|--------------------|-----------------|  
|If-Match|The entity state version of the API. This header is required. A value of `"*"` can be used for `If-Match` to unconditionally apply the operation.|  
  
### Responses  
 This operation has the following responses.  
  
#### 204 No Content  
 The policy configuration was successfully removed from the API.  
  
#### 400 Bad Request  
 Request validation failed.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 404 Not Found  
 The specified API does not exist.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.  
  
#### 412 Precondition Failed  
 Returned if the resource doesn’t pass the condition specified by the `If-Match` header.  
  
 The response body contains an [Error](../ApiManagementREST/Azure-API-Management-REST-API-contract-reference.md#error) response representation.
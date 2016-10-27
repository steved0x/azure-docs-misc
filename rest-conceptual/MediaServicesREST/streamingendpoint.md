---
title: "StreamingEndpoint"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d42211cd-8a20-4566-97ec-9885a00732e7
caps.latest.revision: 35
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
# StreamingEndpoint
> [!IMPORTANT]
>  Starting with Media Services 2.7, the `Origin` entity was renamed to `StreamingEndpoint`.  
  
 The `StreamingEndpoint` entity represents a streaming service that can deliver content directly to a client player application, or to a Content Delivery Network (CDN) for further distribution. Starting with version 2.9, Microsoft Azure Media Services provides the Azure CDN integration (for more information, see the `CdnEnabled` property documented below). The outbound stream from a StreamingEndpoint service can be a live stream, or a video on demand Asset in your Media Services account. In adndition, you can control the capacity of the StreamingEndpoint service to handle growing bandwidth needs by adjusting scale units (also known as streaming units). It is recommended to allocate one or more scale units for applications in production environment. Scale units provide you with both dedicated egress capacity that can be purchased in increments of 200 Mbps and additional functionality which currently includes use [dynamic packaging](http://msdn.microsoft.com/en-us/8d3069a3-4d1d-4a7c-946c-1df63e54cfeb). For more information, see [How to Scale a Media Service](http://www.windowsazure.com/manage/services/media-services/how-to-scale-a-media-service/).  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://msdn.microsoft.com/en-us/42ae6204-93bc-4797-bf40-1c68512cfb73).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
 This topic gives an overview of the `StreamingEndpoint` entity and also demonstrates how to execute various operations with the Media Services REST API.  
  
-   [Create StreamingEndpoint](#create_streaming_endpoints)  
  
     Also shows how to create an Origin (which was the name of the entity before the 2.7 release).  
  
-   [Start StreamingEndpoint](#start_create_streaming_endpoints)  
  
-   [Stop StreamingEndpoints](#stop_create_streaming_endpoints)  
  
-   [Scale StreamingEndpoints](#scale_create_streaming_endpoints)  
  
-   [List StreamingEndpoints](#list_create_streaming_endpoints)  
  
-   [Update StreamingEndpoints](#update_create_streaming_endpoints)  
  
-   [Delete StreamingEndpoints](#delete_create_streaming_endpoints)  
  
## StreamingEndpoint Entity  
 The `StreamingEndpoint` entity contains the following properties.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`Id`<br /><br /> Read-only. Set by Media Services.|Edm.String|The StreamingEndpoint ID, assigned upon creation. The format is: nb:oid:UUID:\<GUID>.|  
|`Name`|Edm.String|Friendly name for the StreamingEndpoint service.<br /><br /> - Must be unique within your Media Services account.<br /><br /> - Maximum length = 32 characters.<br /><br /> - Cannot contain spaces.<br /><br /> - Hyphens and alphanumeric characters only.<br /><br /> - Cannot begin or end with a hyphen.|  
|`Description`|Edm.String|Description of the StreamingEndpoint. The maximum length is 256 characters.|  
|`Created`<br /><br /> Read-only. Set by Media Services.|Edm.DateTime|Created by the Microsoft Azure Media Services Live Streaming Preview service.|  
|`State`<br /><br /> Read-only. Set by Media Services.|Edm.Int32|Values for the property include:<br /><br /> - Stopped. The initial state of a StreamingEndpoint after creation.<br /><br /> - Starting. The StreamingEndpoint is transitioning to the running state.<br /><br /> - Running. The StreamingEndpoint is able to stream content to clients.<br /><br /> - Scaling. The streaming units (ScaleUnits) are being increased or decreased.<br /><br /> - Stopping. The StreamingEndpoint is transitioning to the stopped state.|  
|`HostName`<br /><br /> Read-only. Set by Media Services.|Edm.String|Default streaming endpoint hostname.|  
|`LastModified`<br /><br /> Read-only. Set by Media Services.|Edm.DateTime|Last update time for this entity.|  
|`ScaleUnits`<br /><br /> Read-only.<br /><br /> If `ScaleUnits` is set to 0, the content will be streamed from the [shared pool](#SharedPool).|Edm.Int32|The number of streaming units allocated for the StreamingEndpoint deployment. When the StreamingEndpoint is in the `Running` state, the streaming units on the StreamingEndpoint can be scaled up by calling the `Scale` operation.<br /><br /> Note that the following StreamingEndpoint’s properties can only be configured with 1 or more streaming units: `AccessControl`, `CustomHostNames`, `CacheControl`, `CrossSiteAccessPolicies`.|  
|`CdnEnabled`<br /><br /> This property was added in Media Services 2.9.|`Edm.Boolean`|Indicates whether or not the Azure CDN integration for this StreamingEndpoint is enabled (disabled by default.)<br /><br /> To set the `CdnEnabled` to true, the StreamingEndpoint must have at least one streaming unit (`ScaleUnits`) and be in the stopped state. If later you want to set `ScaleUnits` to 0, you must first set the CdnEnabled to false.<br /><br /> It could take up to 90 min for the Azure CDN integration to get enabled. Use the [Operation](../MediaServicesREST/operation.md) REST API to check the status. Once it is enabled, the following configurations get disabled: `CustomHostNames` and `AccessControl`.<br /><br /> **Note**: Not all data centers support the Azure CDN integration. To check whether or not your data center has the Azure CDN integration available do the following:<br /><br /> - Try to set the `CdnEnabled` to true.<br /><br /> - Check the returned result for an `HTTP Error Code 412` (PreconditionFailed) with a message of  "Streaming endpoint CdnEnabled property cannot be set to true as CDN capability is not available in the current region."<br /><br /> If you get this error, the data center does not support it. You should try another data center.|  
|`CustomHostNames`<br /><br /> Optional.|Collection(Edm.String)|Used to configure a streaming endpoint to accept traffic directed to a custom host name. This allows for easier traffic management configuration through a Global Traffic Manager (GTM) and also for branded domain names to be used as the streaming endpoint name.<br /><br /> The ownership of the domain name must be confirmed by Azure Media Services. Azure Media Services verifies the domain name ownership by requiring a `CName` record containing the Azure Media Services account ID as a component to be added to the domain in use. As an example, for “sports.contoso.com” to be used as a custom host name for the Streaming Endpoint, a record for “\<accountId>.contoso.com” must be configured to point to one of Media Services verification host names. The verification host name is composed of verifydns.\<mediaservices-dns-zone>. The following table contains the expected DNS zones to be used in the verify record for different Azure regions.<br /><br /> North America, Europe, Singapore, Hong Kong, Japan:<br /><br /> - mediaservices.windows.net<br /><br /> - verifydns.mediaservices.windows.net<br /><br /> China:<br /><br /> - mediaservices.chinacloudapi.cn<br /><br /> - verifydns.mediaservices.chinacloudapi.cn<br /><br /> For example, a `CName` record that maps “945a4c4e-28ea-45cd-8ccb-a519f6b700ad.contoso.com” to “verifydns.mediaservices.windows.net” proves that the Azure Media Services ID 945a4c4e-28ea-45cd-8ccb-a519f6b700ad has the ownership of the contoso.com domain, thus enabling any name under contoso.com to be used as a custom host name for a streaming endpoint under that account.<br /><br /> To find the Media Service ID value, go to the [Azure classic portal](https://manage.windowsazure.com) and select your Media Service account. The MEDIA SERVICE ID appears on the right of the DASHBOARD page.<br /><br /> **Warning**: If there is an attempt to set a custom host name without a proper verification of the `CName` record, the DNS response will fail and then be cached for some time. Once a proper record is in place it might take a while until the cached response is revalidated. Depending on the DNS provider for the custom domain, it could take anywhere from a few minutes to an hour to revalidate the record.<br /><br /> In addition to the `CName` that maps `<accountId>.<parent domain>` to `verifydns.<mediaservices-dns-zone>`, you must create another `CName` that maps the custom host name (for example, `sports.contoso.com`) to your Media Services StreamingEndpont’s host name (for example, `amstest.streaming.mediaservices.windows.net`).<br /><br /> **Note**: Streaming endpoints located in the same data center, cannot share the same custom host name.|  
|`AccessControl`|[StreamingEndpointAccessControl ComplexType](#StreamingEndpointAccessControl)|Used to configure the following security settings for this streaming endpoint: Akamai signature header authentication keys and IP addresses that are allowed to connect to this endpoint.|  
|`CacheControl`|[StreamingEndpointCacheControl](#StreamingEndpointCacheControl)|Used to configure asset cache lifetime for assets served through this streaming endpoint.|  
|`CrossSiteAccessPolicies`|[CrossSiteAccessPolicies](../MediaServicesREST/crosssiteaccesspolicies.md)|Used to specify cross site access policies for various clients. For more information, see [Cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html) and [Making a Service Available Across Domain Boundaries](http://msdn.microsoft.com/library/cc197955\(v=vs.95\).aspx).|  
  
###  <a name="StreamingEndpointCacheControl"></a> StreamingEndpointCacheControl  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`MaxAge`<br /><br /> Optional.|Edm.Int64|Overrides the default max-age HTTP cache control header set by the streaming endpoint on media fragments and on-demand manifests. The value is set in seconds.|  
  
###  <a name="StreamingEndpointAccessControl "></a> StreamingEndpointAccessControl ComplexType  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Akamai`|[AkamaiAccessControl](#AkamaiAccessControl)|Akamai access control.|  
|`IP`|[IPAccessControl](#IPAccessControl)|IP access control.|  
  
###  <a name="AkamaiAccessControl"></a> AkamaiAccessControl  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|AkamaiSignatureHeaderAuthenticationKeyList|[AkamaiSignatureHeaderAuthenticationKey ComplexType](#AkamaiSignatureHeaderAuthenticationKey)|Contains information about Akamai Signature Header Authentication keys.|  
  
###  <a name="IPAccessControl"></a> IPAccessControl  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|Allow|[IPRange ComplexType](#IPRange)|Defines the IP addresses that can connect to a streaming endpoint.<br /><br /> **Note**: Setting this value to null allows all IP source addresses to connect. Setting it to an empty string (“”) allows no one to connect.|  
  
###  <a name="AkamaiSignatureHeaderAuthenticationKey"></a> AkamaiSignatureHeaderAuthenticationKey ComplexType  
 This type describes Akamai G20 authentication settings. Akamai Authentication is a keyed-hash message authentication scheme. The authentication key is a secret shared by the Akamai CDN and the Azure Media Origin Streaming Service. Azure Media Services only supports version 3, which uses HMAC-MD5.  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Identifier`|Edm.String|The identifier for the authentication key.  This is the nonce provided by Akamai.|  
|`Expiration`|Edm.DateTime|DateTime value that specifies when the Akamai authentication expires|  
|`Base64Key`|Edm.String|Base64-encoded authentication key that will be used by the CDN.  The authentication key provided by Akamai is an ASCII encoded string, and must be converted to bytes and then base64 encoded.|  
  
 The following C# example shows how to convert Akamai authentication key to base64:  
  
```  
string akamaiKey = "01234567890123456789012345678901";  
string base64Key = Convert.ToBase64String(System.Text.Encoding.ASCII.GetBytes(akamaiKey);  
  
```  
  
###  <a name="IPRange"></a> IPRange ComplexType  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Name`|Edm.String|A friendly name for this IP Range.|  
|`Address`|Edm.String|The base IP address for the subnet representation (for example:192.168.0.1).|  
|`SubnetPrefixLength`|Edm.Int32|The number of significant bits for the subnet mask (for example, in the following IP address 192.168.0.1/24, 24 represents the number of significant bits).|  
  
##  <a name="create_streaming_endpoints"></a> Create StreamingEndpoint  
 Create a new StreamingEndpoint service.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/api/StreamingEndpoint|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab.  
  
 Make sure to use valid redirected host URI and authorization bearer token values. For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
POST https://testrest.cloudapp.net/api/StreamingEndpoints HTTP/1.1  
Content-Type: application/json;odata=minimalmetadata  
Accept: application/json;odata=minimalmetadata  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
x-ms-version: 2.11  
Authorization: Bearer <token value>  
  
```  
  
 Request body:  
  
```  
{    
   "Id":null,  
   "Name":"teststreamingendpoint001",  
   "Description":"",  
   "Created":"0001-01-01T00:00:00",  
   "LastModified":"0001-01-01T00:00:00",  
   "State":null,  
   "HostName":null,  
   "ScaleUnits":1,  
   "CustomHostNames":[    
  
   ],  
   "AccessControl":{    
      "Akamai":{    
         "AkamaiSignatureHeaderAuthenticationKeyList":[    
            {    
               "Identifier":"My key",  
               "Expiration":"2015-08-08T21:45:34.463Z",  
               "Base64Key":"/31iWKdqNC7YUnj8zQ3XHA=="  
            }  
         ]  
      },  
      "IP":{    
         "Allow":[    
            {    
               "Name":"Allow all",  
               "Address":"0.0.0.0",  
               "SubnetPrefixLength":0  
            }  
         ]  
      }  
   },  
   "CacheControl":{    
      "MaxAge":"1800"  
   },  
   "CrossSiteAccessPolicies":{    
      "ClientAccessPolicy":"<access-policy><cross-domain-access><policy><allow-from http-request-headers='*'><domain uri='http://*' /></allow-from><grant-to><resource path='/' include-subpaths='false' /></grant-to></policy></cross-domain-access></access-policy>",  
      "CrossDomainPolicy":"<?xml version='1.0'?><!DOCTYPE cross-domain-policy SYSTEM 'http://www.macromedia.com/xml/dtds/cross-domain-policy.dtd'><cross-domain-policy><allow-access-from domain='*' /></cross-domain-policy>"  
   }  
}  
  
```  
  
 If successful, a **202 Accepted** status code is returned along with a representation of the created entity in the response body.  
  
```  
HTTP/1.1 202 Accepted  
Cache-Control: no-cache  
Content-Length: 1185  
Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8  
Location: https://testrest.cloudapp.net/api/StreamingEndpoints('nb%3Aoid%3AUUID%3Ad2742eb8-ce32-44b8-aae8-83f21364c291')  
Server: Microsoft-IIS/8.5  
request-id: 917c74d3-ebc7-48b6-8484-a103054a9e34  
x-ms-request-id: 917c74d3-ebc7-48b6-8484-a103054a9e34  
operation-id: nb:opid:UUID:ec2e517c-9b33-4af5-baca-e6136acfb40f  
X-Content-Type-Options: nosniff  
DataServiceVersion: 3.0;  
X-Powered-By: ASP.NET  
Date: Sun, 10 Aug 2014 00:31:28 GMT  
  
{    
   "odata.metadata":"https://testrest.cloudapp.net/api/$metadata#StreamingEndpoints/@Element",  
   "Id":"nb:oid:UUID:d2742eb8-ce32-44b8-aae8-83f21364c291",  
   "Name":"teststreamingendpoint001",  
   "Description":"",  
   "Created":"2014-08-10T00:31:28.6760592Z",  
   "LastModified":"2014-08-10T00:31:28.6760592Z",  
   "State":"Stopped",  
   "HostName":null,  
   "ScaleUnits":1,  
   "CustomHostNames":[    
  
   ],  
   "AccessControl":{    
      "Akamai":{    
         "AkamaiSignatureHeaderAuthenticationKeyList":[    
            {    
               "Identifier":"My key",  
               "Expiration":"2015-08-08T21:45:34.463Z",  
               "Base64Key":"/31iWKdqNC7YUnj8zQ3XHA=="  
            }  
         ]  
      },  
      "IP":{    
         "Allow":[    
            {    
               "Name":"Allow all",  
               "Address":"0.0.0.0",  
               "SubnetPrefixLength":0  
            }  
         ]  
      }  
   },  
   "CacheControl":{    
      "MaxAge":"1800"  
   },  
   "CrossSiteAccessPolicies":{    
      "ClientAccessPolicy":"<access-policy><cross-domain-access><policy><allow-from http-request-headers='*'><domain uri='http://*' /></allow-from><grant-to><resource path='/' include-subpaths='false' /></grant-to></policy></cross-domain-access></access-policy>",  
      "CrossDomainPolicy":"<?xml version='1.0'?><!DOCTYPE cross-domain-policy SYSTEM 'http://www.macromedia.com/xml/dtds/cross-domain-policy.dtd'><cross-domain-policy><allow-access-from domain='*' /></cross-domain-policy>"  
   }  
}  
  
```  
  
 The **202 Accepted** status code indicates an asynchronous operation, in which case the operation-id header value is also provided for use in polling and tracking the status of long-running operations, such as starting or stopping a StreamingEndpoint. Pass the operation-id header value into the Operation Entity to retrieve the status. For more information, see [Manually Polling Long-Running Operations](http://msdn.microsoft.com/en-us/3f8c9717-b557-47b8-bbef-18f867e98019).  
  
##  <a name="start_create_streaming_endpoints"></a> Start StreamingEndpoint  
 Start the specified StreamingEndpoint. A StreamingEndpoint can only be started when it is in the **Stopped** state. If the streaming unit count is 0, points the DNS name to the shared pool.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/api/StreamingEndpoints(‘*StreamingEndpointId*')/Start|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab.  
  
 Make sure to use valid redirected host URI and authorization bearer token values. For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
 Request headers:  
  
```  
POST https://testrest.cloudapp.net/api/StreamingEndpoints('nb%3Aoid%3AUUID%3A32ad7fa6-f780-4345-bbc6-45a79a914427')/Start HTTP/1.1  
Content-Type: application/json;odata=minimalmetadata  
Accept: application/json;odata=minimalmetadata  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
x-ms-version: 2.9  
Authorization: Bearer <token value>  
  
```  
  
 If successful, a **202 Accepted** status code is returned. The **202 Accepted** status code indicates an asynchronous operation, in which case the operation-id header value is also provided for use in polling and tracking the status of long-running operations, such as starting or stopping a StreamingEndpoint. Pass the operation-id header value into the Operation Entity to retrieve the status. For more information, see [Manually Polling Long-Running Operations](http://msdn.microsoft.com/en-us/3f8c9717-b557-47b8-bbef-18f867e98019).  
  
##  <a name="stop_create_streaming_endpoints"></a> Stop StreamingEndpoints  
 Stop the specified StreamingEndpoint. A StreamingEndpoint can be stopped only when it is in the **Running** state.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/api/StreamingEndpoints(‘*StreamingEndpointId*')/Stop|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab.  
  
 Make sure to use valid redirected host URI and authorization bearer token values. For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
POST https://testrest.cloudapp.net/api/StreamingEndpoints('nb%3Aoid%3AUUID%3A32ad7fa6-f780-4345-bbc6-45a79a914427')/Start HTTP/1.1  
Content-Type: application/json;odata=minimalmetadata  
Accept: application/json;odata=minimalmetadata  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
x-ms-version: 2.11  
Authorization: Bearer <token value>  
  
```  
  
 If successful, a **202 Accepted** status code is returned. The **202 Accepted** status code indicates an asynchronous operation, in which case the operation-id header value is also provided for use in polling and tracking the status of long-running operations, such as starting or stopping a StreamingEndpoint. Pass the operation-id header value into the Operation Entity to retrieve the status. For more information, see [Manually Polling Long-Running Operations](http://msdn.microsoft.com/en-us/3f8c9717-b557-47b8-bbef-18f867e98019).  
  
##  <a name="scale_create_streaming_endpoints"></a> Scale StreamingEndpoints  
 Dynamically updates the streaming unit capacity while in the running state.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/api/StreamingEndpoints(‘*StreamingEndpointId*')/Scale|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab.  
  
 Make sure to use valid redirected host URI and authorization bearer token values. For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
POST https://testrest.cloudapp.net/api/StreamingEndpoints('nb%3Aoid%3AUUID%3A32ad7fa6-f780-4345-bbc6-45a79a914427')/Scale HTTP/1.1  
Content-Type: application/json;odata=minimalmetadata  
Accept: application/json;odata=minimalmetadata  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
x-ms-version: 2.11  
Authorization: Bearer <token value>  
  
```  
  
 Request body:  
  
```  
{"scaleUnits" : 2}  
```  
  
 If successful, a **202 Accepted** status code is returned. The **202 Accepted** status code indicates an asynchronous operation, in which case the operation-id header value is also provided for use in polling and tracking the status of long-running operations, such as starting or stopping a StreamingEndpoint. Pass the operation-id header value into the Operation Entity to retrieve the status. For more information, see [Manually Polling Long-Running Operations](http://msdn.microsoft.com/en-us/3f8c9717-b557-47b8-bbef-18f867e98019).  
  
##  <a name="list_create_streaming_endpoints"></a> List StreamingEndpoints  
 StreamingEndpoints are retrieved using a GET HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|Get all StreamingEndpoints:<br /><br /> https://media.windows.net/api/StreamingEndpoints<br /><br /> Get the specified StreamingEndpoint.<br /><br /> https://media.windows.net/api/StreamingEndpoints(‘*StreamingEndpointId*’)|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab.  
  
 Make sure to use valid redirected host URI and authorization bearer token values. For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
GET https://testrest.cloudapp.net/api/StreamingEndpoints HTTP/1.1  
Content-Type: application/json;odata=minimalmetadata  
Accept: application/json;odata=minimalmetadata  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
x-ms-version: 2.11  
Authorization: Bearer <token value>  
  
```  
  
 If successful, this operation returns a **200 OK** status code and a list of all of the StreamingEndpoints created in your Media Services account.  
  
##  <a name="update_create_streaming_endpoints"></a> Update StreamingEndpoints  
 Update a StreamingEndpoint with new property values. This is an asynchronous operation if the StreamingEndpoint is running and the settings are changed.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|PATCH/PUT/MERGE<br /><br /> For more information about these operations, see [PATCH/PUT/MERGE](http://msdn.microsoft.com/library/dd541276.aspx).|https://media.windows.net/api/StreamingEndpoints(‘*StreamingEndpointId*’)|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. The example updates the **MaxAge** value.  
  
 Make sure to use valid redirected host URI and authorization bearer token values. For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
PATCH https://testrest.cloudapp.net/api/StreamingEndpoints('nb%3Aoid%3AUUID%3A32ad7fa6-f780-4345-bbc6-45a79a914427') HTTP/1.1  
Content-Type: application/json;odata=minimalmetadata  
Accept: application/json;odata=minimalmetadata  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
x-ms-version: 2.11  
Authorization: Bearer <token value>  
  
```  
  
 Request body:  
  
```  
{"CacheControl":{"MaxAge":"2000"}}  
```  
  
 If the update completes synchronously, it returns a **204 No Content** status code; otherwise it returns a **202 Accepted** status code. The **202 Accepted** status code indicates an asynchronous operation, in which case the operation-id header value is also provided for use in polling and tracking the status of long-running operations, such as starting or stopping a StreamingEndpoint. Pass the operation-id header value into the Operation Entity to retrieve the status. For more information, see [Manually Polling Long-Running Operations](http://msdn.microsoft.com/en-us/3f8c9717-b557-47b8-bbef-18f867e98019).  
  
##  <a name="delete_create_streaming_endpoints"></a> Delete StreamingEndpoints  
 Delete a StreamingEndpoint. A StreamingEndpoint can be deleted only when it is in the **Stopped** state.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|DELETE|https://media.windows.net/api/StreamingEndpoints(‘*StreamingEndpointId*’)|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab.  
  
 Make sure to use valid redirected host URI and authorization bearer token values. For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
DELETE https://testrest.cloudapp.net/api/StreamingEndpoints('nb%3Aoid%3AUUID%3A32ad7fa6-f780-4345-bbc6-45a79a914427') HTTP/1.1  
Content-Type: application/json;odata=minimalmetadata  
Accept: application/json;odata=minimalmetadata  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
x-ms-version: 2.11  
Authorization: Bearer <token value>  
  
```  
  
 If successful, a **202 Accepted** status code is returned. The **202 Accepted** status code indicates an asynchronous operation, in which case the operation-id header value is also provided for use in polling and tracking the status of long-running operations, such as starting or stopping a StreamingEndpoint. Pass the operation-id header value into the Operation Entity to retrieve the status. For more information, see [Manually Polling Long-Running Operations](http://msdn.microsoft.com/en-us/3f8c9717-b557-47b8-bbef-18f867e98019).  
  
##  <a name="SharedPool"></a> Streaming from a Dedicated or Shared Pool  
 There are two states possible when working with StreamingEndpoints: *dedicated* or *shared*. If you consent to use *streaming units*, your StreamingEndpoint performance is governed by a Service Level Agreement (SLA). This state is referred to as “dedicated,” for using dedicated streaming units. If you do not contract to use streaming units, you are using computing resources from a *shared pool*. The shared pool can be used for testing or prototyping, but no SLA governs the performance.  
  
 By default, when you create a Microsoft Azure Media Services account, one StreamingEndpoint is created with no streaming units. The StreamingEndpoint has the name “Default,” and it cannot be deleted. The state of the StreamingEndpoint is **Started**. After some time, the state changes to `Running`.  
  
 If the streaming unit count is set to 0, and the StreamingEndpoint entity is in the **Running** state, the streaming will continue from shared pool. To stop streaming at a later point in time, call the Stop operation on the StreamingEndpoints entity. The table summarizes the behavior:  
  
|State|Streaming Units|Description|Available Actions|  
|-----------|---------------------|-----------------|-----------------------|  
|Stopped|0|Not streaming.|Start|  
|Running|0|Streaming from the shared pool.|Stop, Scale|  
|Stopped|>0|Not streaming.|Start, Scale|  
|Running|>0|Streaming from dedicated.|Stop, Scale|  
  
## See Also  
 [Channel](../MediaServicesREST/channel.md)   
 [Program](../MediaServicesREST/program.md)   
 [Operation](../MediaServicesREST/operation.md)
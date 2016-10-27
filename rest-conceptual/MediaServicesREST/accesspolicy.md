---
title: "AccessPolicy"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 9deaec39-9330-47c7-a452-f56dcd89b59b
caps.latest.revision: 40
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
# AccessPolicy
An AccessPolicy defines the permissions and duration of access to an Asset.  
  
 This topic gives an overview of the `AccessPolicy` entity and also demonstrates how to execute various operations with the Media Services REST API.  
  
-   [AccessPolicy Entity Properties](../MediaServicesREST/accesspolicy.md#accesspolicy_properties)  
  
-   [Create an AccessPolicy](../MediaServicesREST/accesspolicy.md#create_an_accesspolicy)  
  
-   [List AccessPolicies](../MediaServicesREST/accesspolicy.md#list_accesspolicies)  
  
-   [Delete an AccessPolicy](../MediaServicesREST/accesspolicy.md#delete_an_accesspolicy)  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://msdn.microsoft.com/en-us/42ae6204-93bc-4797-bf40-1c68512cfb73).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
##  <a name="accesspolicy_properties"></a> AccessPolicy Entity Properties  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`Id`<br /><br /> Read-only. Set by Media Services at creation time.|Edm.String|Unique identifier.|  
|`Created`<br /><br /> Read-only. Set by Media Services at creation time.|Edm.DateTime|Represents the number of milliseconds since midnight Jan 1, 1970.|  
|`LastModified`<br /><br /> Read-only. Set by Media Services.|Edm.DateTime|This value is updated by Media Services after any property changes are made. It represents the number of milliseconds since midnight Jan 1, 1970.|  
|`Name`<br /><br /> Required.|Edm.String|Friendly name for your AccessPolicy.|  
|`DurationInMinutes`<br /><br /> Required.|Edm.Double|Duration that the AccessPolicy is valid for.|  
|`Permissions`<br /><br /> Optional.|Edm.Int32|This value specifies the access rights the client has when interacting with the Asset. Valid values are:<br /><br /> -   None = 0<br />-   Read = 1<br />-   Write = 2<br />-   Delete = 4<br />-   List = 8<br /><br /> The default value is 0.<br /><br /> Note that the List permission should not be used when creating OnDemandOrigin locators.|  
  
##  <a name="create_an_accesspolicy"></a> Create an AccessPolicy  
 AccessPolicies can be created with a POST HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/API/AccessPolicies|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
POST https://media.windows.net/API/AccessPolicies HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d  
Host: media.windows.net  
Content-Length: 67  
Expect: 100-continue  
  
{"Name": "NewUploadPolicy", "DurationInMinutes" : "100", "Permissions" : 2 }  
```  
  
##  <a name="list_accesspolicies"></a> List AccessPolicies  
 AccessPolicies can be retrieved using a GET HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/AccessPolicies|HTTP/1.1|  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/AccessPolicies('*accesspolicyid*')|HTTP/1.1|  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/Assets('*assetid*')/AccessPolicies|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
GET https://media.windows.net/API/AccessPolicies('nb:pid:UUID:ad05d8fa-06a2-4e2f-8fb4-fac57875135a') HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fnimbusvoddev.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334276569&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Cax61TKgo%2fLo5k6AWA%2brOLdAbMMd4poqvpVqiRPdTXk%3d  
Host: media.windows.net  
  
```  
  
##  <a name="delete_an_accesspolicy"></a> Delete an AccessPolicy  
 AccessPolicies can be deleted using a DELETE HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|DELETE|https://media.windows.net/API/AccessPolicies('*accesspolicyid*')|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
DELETE https://media.windows.net/API/AccessPolicies('nb:pid:UUID:ad05d8fa-06a2-4e2f-8fb4-fac57875135a') HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337156939&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=IMU5VFP%2bhekKwnUJR13b%2fBMsrZF1h72pZdMlqZ8Txf8%3d  
Host: media.windows.net  
Content-Length: 0  
  
```  
  
## See Also  
 [ContentKey](../MediaServicesREST/contentkey.md)   
 [Asset](../MediaServicesREST/asset.md)   
 [AssetFile](../MediaServicesREST/assetfile.md)   
 [Job](../MediaServicesREST/job.md)   
 [JobTemplate](../MediaServicesREST/jobtemplate.md)   
 [Locator](../MediaServicesREST/locator.md)   
 [MediaProcessor](../MediaServicesREST/mediaprocessor.md)   
 [Task](../MediaServicesREST/task.md)   
 [TaskTemplate](../MediaServicesREST/tasktemplate.md)   
 [Quotas and Limitations](http://msdn.microsoft.com/en-us/82f7e538-6bdf-4883-aa50-24574cc4996e)
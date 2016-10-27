---
title: "NotificationEndPoint"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 10bb13e6-eb2f-427a-a110-c6d4ed194818
caps.latest.revision: 22
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
# NotificationEndPoint
The endpoint to which the notifications about the job state are sent.  
  
 This type was added in Media Services version 2.1.  
  
> [!NOTE]
>  Azure queue notification may have some delay.  
  
 This topic gives an overview of the `NotificationEndPoint` entity and also demonstrates how to execute various operations with the Media Services REST API.  
  
1.  [Create a NotificationEndPoint](#Create_NotificationEndPoint)  
  
2.  [Update a NotificationEndPoint](#Update_NotificationEndPoint)  
  
3.  [Get a NotificationEndPoint](#Get_NotificationEndPoint)  
  
4.  [Delete a NotificationEndPoint](#Delete_NotificationEndPoint)  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://msdn.microsoft.com/en-us/42ae6204-93bc-4797-bf40-1c68512cfb73).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
##  <a name="job_entity_properties"></a> NotificationEndPoint Entity Properties  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|Id<br /><br /> Read-only. Set by Media Services at creation time.|Edm.String|Unique identifier. Format: nb:ncid:UUID:\<GUID>.|  
|Name<br /><br /> Required.|Edm.String|Display name of the notification endpoint.|  
|Created<br /><br /> Read-only. Set by Media Services at creation time.|Edm.DateTime|This value is set by Media Services at creation time.|  
|EndpointType<br /><br /> Required. Cannot be updated after the entity has been created.|Edm.Int32|Type of notification endpoint.<br /><br /> The only valid value is: AzureQueue = 1.|  
|EndpointAddress<br /><br /> Required. Cannot be updated after the entity has been created.|Edm.String|The `EndpointAddress` is the name of `AzureQueue` to use. The naming rules of azure queue are enforced. For more information, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/windowsazure/dd179349.aspx).|  
|CredentialType|Edm.Int32|Set the Credential type for notification endpoint .|  
|EncryptedEndPointCredential|Edm.String|The encrypted endPoint credential.|  
|ProtectionKeyId|Edm.String|The Protection Key Id.|  
|ProtectionKeyType|Edm.Int32|The protection key type.|  
  
##  <a name="Create_NotificationEndPoint "></a> Create a NotificationEndPoint  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 NotificationEndPoint can be creating using HTTP POST request.  
  
```  
POST https://media.windows.net/API/NotificationEndPoints HTTP/1.1  
User-Agent: Microsoft ADO.NET Data Services  
DataServiceVersion: 1.0  
MaxDataServiceVersion: 3.0  
Accept: application/atom+xml,application/xml  
Accept-Charset: UTF-8  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d   
x-ms-version: 2.11  
Content-Type: application/atom+xml  
Host: media.windows.net  
Content-Length: 533  
Expect: 100-continue  
  
<?xml version="1.0" encoding="utf-8"?><entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"><id /><title /><updated>2013-04-21T21:44:14Z</updated><author><name /></author><content type="application/xml"><m:properties><d:EndPointAddress>endpointpueu1</d:EndPointAddress><d:EndPointType m:type="Edm.Int32">1</d:EndPointType><d:Id m:null="true" /><d:Name>EndPointName1</d:Name></m:properties></content></entry>  
  
```  
  
 The following is the response for NotificationEndPoint creation:  
  
```  
HTTP/1.1 201 Created  
Cache-Control: no-cache  
Content-Length: 1113  
Content-Type: application/atom+xml;type=entry;charset=utf-8  
Location: https://media.windows.net/api/NotificationEndPoints('nb%3Anepid%3AUUID%3A1b373460-1fc4-4e80-aad6-b2b0cdb9e674')  
Server: Microsoft-IIS/7.5  
request-id: 9da4221a-7284-4767-905b-4a6823ae2f6f  
x-ms-request-id: 9da4221a-7284-4767-905b-4a6823ae2f6f  
X-Content-Type-Options: nosniff  
DataServiceVersion: 1.0;  
X-Powered-By: ASP.NET  
Date: Sun, 21 Apr 2013 21:44:17 GMT  
  
<?xml version="1.0" encoding="utf-8"?><entry xml:base="https://media.windows.net/api/" xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"><id>https://media.windows.net/api/NotificationEndPoints('nb%3Anepid%3AUUID%3A1b373460-1fc4-4e80-aad6-b2b0cdb9e674')</id><category term="Microsoft.Cloud.Media.Vod.Rest.Data.Models.NotificationEndPoint" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" /><link rel="edit" title="NotificationEndPoint" href="NotificationEndPoints('nb%3Anepid%3AUUID%3A1b373460-1fc4-4e80-aad6-b2b0cdb9e674')" /><title /><updated>2013-04-21T21:44:17Z</updated><author><name /></author><content type="application/xml"><m:properties><d:Id>nb:nepid:UUID:1b373460-1fc4-4e80-aad6-b2b0cdb9e674</d:Id><d:Name>EndPointName1</d:Name><d:Created m:type="Edm.DateTime">2013-04-21T21:44:16.4802609Z</d:Created><d:EndPointAddress>endpointpueu1</d:EndPointAddress><d:EndPointType m:type="Edm.Int32">1</d:EndPointType></m:properties></content></entry>  
  
```  
  
##  <a name="Update_NotificationEndPoint "></a> Update a NotificationEndPoint  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 NotificationEndPoint can be updated using HTTP POST request.  
  
```  
MERGE https://media.windows.net/API/NotificationEndPoints('nb%3Anepid%3AUUID%3A64bb03ea-bb6a-4d3c-b6e9-4a0f3e346638') HTTP/1.1  
User-Agent: Microsoft ADO.NET Data Services  
DataServiceVersion: 1.0  
MaxDataServiceVersion: 3.0  
Accept: application/atom+xml,application/xml  
Accept-Charset: UTF-8  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d   
x-ms-version: 2.11  
Content-Type: application/atom+xml  
Host: media.windows.net  
Content-Length: 690  
Expect: 100-continue  
  
<?xml version="1.0" encoding="utf-8"?><entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"><id>https://media.windows.net/API/NotificationEndPoints('nb%3Anepid%3AUUID%3A64bb03ea-bb6a-4d3c-b6e9-4a0f3e346638')</id><title /><updated>2013-04-21T21:56:15Z</updated><author><name /></author><content type="application/xml"><m:properties><d:EndPointAddress>endpointqueue2</d:EndPointAddress><d:EndPointType m:type="Edm.Int32">1</d:EndPointType><d:Id>nb:nepid:UUID:64bb03ea-bb6a-4d3c-b6e9-4a0f3e346638</d:Id><d:Name>NewEndPoint1</d:Name></m:properties></content></entry>  
  
```  
  
 The following is the response for NotificationEndPoint update:  
  
```  
HTTP/1.1 204 No Content  
Cache-Control: no-cache  
Server: Microsoft-IIS/7.5  
request-id: 6e1533d9-1efc-4c45-b299-8060d2355e48  
x-ms-request-id: 6e1533d9-1efc-4c45-b299-8060d2355e48  
X-Content-Type-Options: nosniff  
DataServiceVersion: 1.0;  
X-Powered-By: ASP.NET  
Date: Sun, 21 Apr 2013 21:56:16 GMT  
  
```  
  
##  <a name="Get_NotificationEndPoint "></a> Get a NotificationEndPoint  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 The following request gets a specified notification point. To get all the notification points call `NotificationEndPoints` without a parameter: `GET https://media.windows.net/api/NotificationEndPoints`.  
  
```  
GET https://media.windows.net/api/NotificationEndPoints('nb%3Anepid%3AUUID%3A6286704e-e69f-454e-80e0-7fda53ce7dba') HTTP/1.1  
DataServiceVersion: 1.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/atom+xml,application/xml  
Accept-Charset: UTF-8  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d   
x-ms-version: 2.11  
Host: media.windows.net  
  
```  
  
```  
HTTP/1.1 200 OK  
Cache-Control: no-cache  
Content-Length: 1167  
Content-Type: application/atom+xml;type=entry;charset=utf-8  
Server: Microsoft-IIS/7.5  
request-id: aa32c140-8e59-4043-bbe8-c2221ca61a5f  
x-ms-request-id: aa32c140-8e59-4043-bbe8-c2221ca61a5f  
X-Content-Type-Options: nosniff  
DataServiceVersion: 1.0;  
X-Powered-By: ASP.NET  
Date: Fri, 02 Aug 2013 06:25:33 GMT  
  
<?xml version="1.0" encoding="utf-8"?><entry xml:base="https://media.windows.net/api/" xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"><id>https://media.windows.net/api/NotificationEndPoints('nb%3Anepid%3AUUID%3A6286704e-e69f-454e-80e0-7fda53ce7dba')</id><category term="Microsoft.Cloud.Media.Vod.Rest.Data.Models.NotificationEndPoint" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" /><link rel="edit" title="NotificationEndPoint" href="NotificationEndPoints('nb%3Anepid%3AUUID%3A6286704e-e69f-454e-80e0-7fda53ce7dba')" /><title /><updated>2013-08-02T06:25:33Z</updated><author><name /></author><content type="application/xml"><m:properties><d:Id>nb:nepid:UUID:6286704e-e69f-454e-80e0-7fda53ce7dba</d:Id><d:Name>62abde48-420f-4f76-9ca4-9ba1d8852f38</d:Name><d:Created m:type="Edm.DateTime">2013-08-02T06:25:02.48</d:Created><d:EndPointAddress>b71b6ac6-e598-4fdf-b5cb-e8494cb955ef</d:EndPointAddress><d:EndPointType m:type="Edm.Int32">1</d:EndPointType></m:properties></content></entry>  
```  
  
##  <a name="Delete_NotificationEndPoint "></a> Delete a NotificationEndPoint  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 NotificationEndPoint can be deleted using HTTP POST request.  
  
```  
DELETE https://media.windows.net/API/NotificationEndPoints('nb%3Anepid%3AUUID%3A64bb03ea-bb6a-4d3c-b6e9-4a0f3e346638') HTTP/1.1  
User-Agent: Microsoft ADO.NET Data Services  
DataServiceVersion: 1.0  
MaxDataServiceVersion: 3.0  
Accept: application/atom+xml,application/xml  
Accept-Charset: UTF-8  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d   
x-ms-version: 2.11  
Host: media.windows.net  
Content-Length: 0  
  
```  
  
 The following is the response for NotificationEndPoint deletion:  
  
```  
HTTP/1.1 204 No Content  
Cache-Control: no-cache  
Server: Microsoft-IIS/7.5  
request-id: f838c56f-d9f6-4e6f-8e0a-945d10a7a48c  
x-ms-request-id: f838c56f-d9f6-4e6f-8e0a-945d10a7a48c  
X-Content-Type-Options: nosniff  
DataServiceVersion: 1.0;  
X-Powered-By: ASP.NET  
Date: Sun, 21 Apr 2013 21:56:17 GMT  
  
```
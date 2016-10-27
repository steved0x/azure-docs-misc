---
title: "IngestManifestAsset"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 49628d78-b064-472e-ad50-7d47d3a59bc1
caps.latest.revision: 20
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
# IngestManifestAsset
IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting. Microsoft Azure Media Services watches internally for the file upload based on IngestManifestFiles associated to the IngestManifestAsset. Once they are uploaded, the asset is completed. For more information on bulk ingesting, see [Ingesting Assets in Bulk with the REST API](http://msdn.microsoft.com/en-us/3caa81ea-c840-4265-b8fa-f958cdde12b6).  
  
 This topic gives an overview of the `IngestManifestAsset` entity and also demonstrates how to execute various operations with the Media Services REST API.  
  
-   [IngestManifestAsset Entity Properties](../MediaServicesREST/ingestmanifestasset.md#ingestmanifestasset_entity_properties)  
  
-   [Create an IngestManifestAsset](../MediaServicesREST/ingestmanifestasset.md#create_an_ingestmanifestasset)  
  
-   [List an IngestManifestAsset](../MediaServicesREST/ingestmanifestasset.md#list_an_ingestmanifestasset)  
  
-   [Delete an IngestManifestAsset](../MediaServicesREST/ingestmanifestasset.md#delete_an_ingestmanifestasset)  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://msdn.microsoft.com/en-us/42ae6204-93bc-4797-bf40-1c68512cfb73).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
##  <a name="ingestmanifestasset_entity_properties"></a> IngestManifestAsset Entity Properties  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`Id`<br /><br /> Read-only. Set by Media Services at creation time.|Edm.String|Unique identifier.|  
|`Created`<br /><br /> Read-only. Set by Media Services at creation time.|Edm.DateTime|Represents the number of milliseconds since midnight Jan 1, 1970.|  
|`LastModified`<br /><br /> Read-only. Set by Media Services.|Edm.DateTime|This value is updated by Media Services after any property changes are made. It represents the number of milliseconds since midnight Jan 1, 1970.|  
|`ParentIngestManifestId`<br /><br /> Required.|Edm.String|IngestManifest that will contain this IngestManifestAsset.|  
|`IngestManifestFiles`<br /><br /> Read-only.|[IngestManifestFile](../MediaServicesREST/ingestmanifestfile.md) entity set|Navigation property that can be used to access the collection of IngestManifestFiles that make up the IngestManifestAsset. Individual IngestManifestFiles can be referenced using the IngestManifestFile Id.|  
|`Asset`<br /><br /> Required.|[Asset](../MediaServicesREST/asset.md) entity|Navigation property that can be used to reference the Asset associated to this IngestManifestAsset.|  
  
##  <a name="create_an_ingestmanifestasset"></a> Create an IngestManifestAsset  
 IngestManifestAssets can be created using an HTTP POST request. IngestManifestAssets must associate with a parent IngestManifest Id and an asset Id in the request body.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/API/IngestManifestAssets|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
POST https://media.windows.net /API/IngestManifestAssets HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d  
Host: media.windows.net  
Content-Length: 152  
Expect: 100-continue  
{ "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "Asset" : { "Id" : "nb:cid:UUID:b757929a-5a57-430b-b33e-c05c6cbef02e"}}  
```  
  
##  <a name="list_an_ingestmanifestasset"></a> List an IngestManifestAsset  
 IngestManifestAssets can be retrieved using an HTTP GET request. You can request a specific IngestManifestAsset by its Id or request all IngestManifestAssets.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/IngestManifestAssets|HTTP/1.1|  
|GET|https://media.windows.net/API/IngestManifestAssets(‘IngestManifestAsset Id’)|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
GET https://media.windows.net /API/IngestManifestAssets('nb:maid:UUID:6422b0a7-15f1-3442-b800-dac3195df54f') HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d  
Host: media.windows.net  
  
```  
  
##  <a name="delete_an_ingestmanifestasset"></a> Delete an IngestManifestAsset  
 IngestManifestAssets can be deleted by referencing the IngestManifestAsset Id value with an HTTP DELETE request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|DELETE|https://media.windows.net/API/IngestManifestAssets(‘IngestManifestAsset Id’)|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
DELETE https://media.windows.net /API/IngestManifestAssets('nb:maid:UUID:9c6e7256-fefd-c541-aa69-fd04cf1cc1a6') HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d  
Host: media.windows.net  
Content-Length: 0  
```  
  
## See Also  
 [Asset](../MediaServicesREST/asset.md)   
 [AssetFile](../MediaServicesREST/assetfile.md)   
 [IngestManifest](../MediaServicesREST/ingestmanifest.md)   
 [IngestManifestFile](../MediaServicesREST/ingestmanifestfile.md)   
 [IngestManifestStatistics](../MediaServicesREST/ingestmanifeststatistics.md)   
 [Quotas and Limitations](http://msdn.microsoft.com/en-us/82f7e538-6bdf-4883-aa50-24574cc4996e)
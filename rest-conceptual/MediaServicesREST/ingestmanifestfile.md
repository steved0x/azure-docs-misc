---
title: "IngestManifestFile"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 80888b04-d045-495b-a931-ed10092e1319
caps.latest.revision: 23
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
# IngestManifestFile
An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting. For more information on bulk ingesting, see [Ingesting Assets in Bulk with the REST API](http://msdn.microsoft.com/en-us/3caa81ea-c840-4265-b8fa-f958cdde12b6). An IngestManifestFile is always associated with an IngestManifest and an IngestManifestAsset.  
  
 This topic gives an overview of the `IngestManifestFile` entity and also demonstrates how to execute various operations with the Media Services REST API.  
  
-   [IngestManifestFile Entity Properties](../MediaServicesREST/ingestmanifestfile.md#ingestmanifestfile_entity_properties)  
  
-   [Create an IngestManifestFile](../MediaServicesREST/ingestmanifestfile.md#create_an_ingestmanifestfile)  
  
-   [List an IngestManifestFile](../MediaServicesREST/ingestmanifestfile.md#list_an_ingestmanifestfile)  
  
-   [Delete an IngestManifestFile](../MediaServicesREST/ingestmanifestfile.md#delete_an_ingestmanifestfile)  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://msdn.microsoft.com/en-us/42ae6204-93bc-4797-bf40-1c68512cfb73).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
##  <a name="ingestmanifestfile_entity_properties"></a> IngestManifestFile Entity Properties  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`Id`<br /><br /> Read-only. Set by Media Services at creation time.|Edm.String|Unique identifier.|  
|`Created`<br /><br /> Read-only. Set by Media Services at creation time.|Edm.DateTime|Represents the number of milliseconds since midnight Jan 1, 1970.|  
|`LastModified`<br /><br /> Read-only. Set by Media Services.|Edm.DateTime|This value is updated by Media Services after any property changes are made. It represents the number of milliseconds since midnight Jan 1, 1970.|  
|`Name`<br /><br /> Required.|Edm.String|Actual filename that will be uploaded to the blob container referenced by the IngestManifest’s **BlobStorageUriForUpload** property. Media Services watches for the file upload in that container by name.<br /><br /> The file name must not be empty or white spaces. Unique within the IngestManifest. Maximum length is 4000.|  
|`State`<br /><br /> Read-only. Set by Media Services.|Edm.Int32|The current state of the IngestManifestFile. This value can be one of the following:<br /><br /> -   **Pending** = 0: The file has not yet been uploaded in order to complete the asset creation. Media Services is waiting on the file upload.<br />-   **Finished** = 1: The file upload was detected and the associated asset has been updated.<br />-   **Error** = 2: An error occurred processing this file. See the **ErrorDetails** property for error information.|  
|`ParentIngestManifestId`<br /><br /> Required.|Edm.String|IngestManifest Id of the manifest that contains this file.|  
|`ParentIngestManifestAssetId`<br /><br /> Required.|Edm.String|IngestManifestAsset Id of the IngestManifestAsset that this file is associated with.|  
|`ErrorDetail`<br /><br /> Read-only. Set by Media Services.|Edm.String|Details of an errors encountered processing this file.|  
|`MimeType`<br /><br /> Optional.|Edm.String|Media Services does not inspect any blob that you uploaded, so you must manually set the mime type. For example, "text/plain" or "video/x-ms-wmv" are valid values to use.|  
|`IsPrimary`<br /><br /> Optional.|Edm.Boolean|Determines if this IngestManifestFile is the primary file in a multi-file Asset.|  
|`EncryptionVersion`<br /><br /> Optional.|Edm.String|Current supported version for StorageEncryption, CommonEncryption, and EnvelopeEncryption is "1.0".|  
|`EncryptionScheme`<br /><br /> Optional.|Edm.String|The encryption scheme used for this file. The valid values are: "StorageEncryption", "CommonEncryption", or "EnvelopeEncryption".|  
|`IsEncrypted`<br /><br /> Optional.|Edm.Boolean|This value should be set to **true** if this file is stored encrypted.|  
|`EncryptionKeyId`<br /><br /> Optional.|Edm.String|Encrypted ContentKey Id.|  
|`InitializationVector`<br /><br /> Optional.|Edm.String|The initialization vector used for storage encryption.|  
  
##  <a name="create_an_ingestmanifestfile"></a> Create an IngestManifestFile  
 IngestManifestFiles can be created by using an HTTP POST request. You must pass a request body that contains the name of the **Name** of the new IngestManifestFile along with the **ParentIngestManifestId** and the **ParentIngestManifestAssetId**.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/API/IngestManifestFiles|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
POST https://media.windows.net/API/IngestManifestFiles HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d  
Host: media.windows.net  
Content-Length: 200  
Expect: 100-continue  
  
{ "Name" : "REST_Example_File.wmv", "ParentIngestManifestId" : "nb:mid:UUID:bfe2d76c-17bd-884a-b9be-21bdfda65984", "ParentIngestManifestAssetId" : "nb:maid:UUID:9c6e7256-fefd-c541-aa69-fd04cf1cc1a6" }  
  
```  
  
##  <a name="list_an_ingestmanifestfile"></a> List an IngestManifestFile  
 IngestManifestFiles can be retrieved using an HTTP GET request. You can request an IngestManifestFile by its Id or request all IngestManifestFiles by omitting the Id.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/IngestManifestFiles|HTTP/1.1|  
|GET|https://media.windows.net/API/IngestManifestFiles(‘IngestManifestFile Id’)|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
GET https://media.windows.net/API/IngestManifestFiles('nb:mfid:UUID:030ef5ef-c5b3-2c4a-86da-217d4d2170de') HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d  
Host: media.windows.net  
  
```  
  
##  <a name="delete_an_ingestmanifestfile"></a> Delete an IngestManifestFile  
 IngestManifestFiles can be deleted by referencing the IngestManifestFile Id value with an HTTP DELETE request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|DELETE|https://media.windows.net/API/IngestManifestFiles(‘IngestManifestFile Id’)|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
DELETE https://media.windows.net/API/IngestManifestFiles('nb:mfid:UUID:030ef5ef-c5b3-2c4a-86da-217d4d2170de') HTTP/1.1  
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
 [AssetFile](../MediaServicesREST/assetfile.md)   
 [IngestManifest](../MediaServicesREST/ingestmanifest.md)   
 [IngestManifestAsset](../MediaServicesREST/ingestmanifestasset.md)   
 [IngestManifestStatistics](../MediaServicesREST/ingestmanifeststatistics.md)   
 [Quotas and Limitations](http://msdn.microsoft.com/en-us/82f7e538-6bdf-4883-aa50-24574cc4996e)
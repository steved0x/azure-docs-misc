---
title: "AssetFile"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 1bdb8930-3ff2-450a-8871-27003c42ee14
caps.latest.revision: 44
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
# AssetFile
The `AssetFile` entity represents an actual video or audio file that is stored in a blob container. An asset file is always associated with an asset, and an asset may contain one or many files. The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.  
  
 This topic gives an overview of the `AssetFile` entity and also demonstrates how to execute various operations with the Media Services REST API.  
  
-   [AssetFile Entity Properties](../MediaServicesREST/assetfile.md#file_entity_properties)  
  
-   [Create an AssetFile](../MediaServicesREST/assetfile.md#create_a_file)  
  
-   [List AssetFiles](../MediaServicesREST/assetfile.md#list_files)  
  
-   [Update an AssetFile](../MediaServicesREST/assetfile.md#Update_a_file)  
  
-   [Delete an AssetFile](../MediaServicesREST/assetfile.md#delete_a_file)  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://msdn.microsoft.com/en-us/42ae6204-93bc-4797-bf40-1c68512cfb73).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
##  <a name="file_entity_properties"></a> AssetFile Entity Properties  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`Id`<br /><br /> Read-only. Set by Media Services at creation time.|Edm.String|Unique identifier.|  
|`Name`<br /><br /> Required.|Edm.String|Friendly name for your AssetFile. The default value is the filename you used during your file upload. Maximum length is 260. **Note:**  Media Services uses the value of the `Name` property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed. The value of the Name property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]". Also, there can only be one ‘.’ for the file name extension.|  
|`ContentFileSize`<br /><br /> Optional.|Edm.Int64|AssetFile size (in bytes) of the content.|  
|`ParentAssetId`<br /><br /> Required. Cannot be updated after the entity has been created.|Edm.String|Asset Id of the Asset that this file is associated with.|  
|`EncryptionVersion`<br /><br /> Optional.|Edm.String|Current supported version for both StorageEncryption and CommonEncryption is "1.0"|  
|`EncryptionScheme`<br /><br /> Optional.|Edm.String|The encryption scheme used for this file. The valid values are: "StorageEncryption" or "CommonEncryption".|  
|`IsEncrypted`<br /><br /> Optional.|Edm.Boolean|This value should be set to `true` if this file is stored encrypted.|  
|`EncryptionKeyId`<br /><br /> Optional.|Edm.String|Encrypted ContentKey Id.|  
|`InitializationVector`<br /><br /> Optional.|Edm.String|The initialization vector used for storage encryption.|  
|`IsPrimary`<br /><br /> Optional.|Edm.Boolean|Determines if this file is the primary file in a multi-file Asset.|  
|`LastModified`<br /><br /> Read-only. Set by Media Services at creation time.|Edm.DateTime|This value is updated by Media Services after any property changes are made. It represents the number of milliseconds since midnight Jan 1, 1970.|  
|`Created`<br /><br /> Read-only. Set by Media Services at creation time.|Edm.DateTime|Represents the number of milliseconds since midnight Jan 1, 1970.|  
|`MimeType`<br /><br /> Optional.|Edm.String|Media Services does not inspect any blob that you uploaded, so you must manually set the mime type. For example, "text/plain" or "video/x-ms-wmv" are valid values to use. Maximum length is 4000.|  
|`ContentChecksum`<br /><br /> Optional.|Edm.String|A hexadecimal number representing a MD5 (RFC 1321) message digest value.  This value is set by the client or client library to serve as a validation of the successful upload of the content. Maximum length is 4000.|  
  
##  <a name="create_a_file"></a> Create an AssetFile  
 The CreateFileInfos function is used to create a new AssetFile entity. For more information, see [REST API Functions](../MediaServicesREST/rest-api-functions.md).  
  
##  <a name="list_files"></a> List AssetFiles  
 AssetFiles are retrieved using a GET HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/Files|HTTP/1.1|  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/Files('*fileid*')|HTTP/1.1|  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/Assets('*assetid*')/Files|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
GET https://media.windows.net/API/Files('nb:cid:UUID:d0214595-fff0-164e-9c67-d576eba09605') HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337178759&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=cKlWvRDsu0bQwDkc1A4sMM5OQOGBEk8OWcuaj9zDkp0%3d  
Host: media.windows.net  
```  
  
##  <a name="Update_a_file"></a> Update an AssetFile  
 AssetFiles are updated using the MERGE HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|MERGE|https://media.windows.net/API/Files('*fileid*')|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
MERGE https://media.windows.net/API/Files('nb:cid:UUID:2710e174-3165-a34c-96ad-618714b0d504') HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337085302&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JFb4PJuWttPAft4dq9HaGl8Zw6hDN6mADhG3NaRi8Co%3d  
Host: media.windows.net  
Content-Length: 27  
Expect: 100-continue  
  
{"MimeType" : "video/mp4" }  
```  
  
##  <a name="delete_a_file"></a> Delete an AssetFile  
 AssetFiles are deleted when their associated Asset has been deleted. For an example, see [Delete an Asset](../MediaServicesREST/asset.md#delete_an_asset).  
  
## See Also  
 [ContentKey](../MediaServicesREST/contentkey.md)   
 [Asset](../MediaServicesREST/asset.md)   
 [AccessPolicy](../MediaServicesREST/accesspolicy.md)   
 [Job](../MediaServicesREST/job.md)   
 [JobTemplate](../MediaServicesREST/jobtemplate.md)   
 [Locator](../MediaServicesREST/locator.md)   
 [MediaProcessor](../MediaServicesREST/mediaprocessor.md)   
 [Task](../MediaServicesREST/task.md)   
 [TaskTemplate](../MediaServicesREST/tasktemplate.md)   
 [Quotas and Limitations](http://msdn.microsoft.com/en-us/82f7e538-6bdf-4883-aa50-24574cc4996e)
---
title: "Asset"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 219a286b-823e-439e-90ca-2ef2aab4db79
caps.latest.revision: 67
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
# Asset
The `Asset` entity contains digital files (including video, audio, images, thumbnail collections, text tracks and closed caption files) and the metadata about these files. After the digital files are uploaded into an asset, they could be used in the Media Services encoding and streaming workflows.  
  
 When you encode an asset, an output asset is produced upon completion of the encoding job. Among the files mentioned above, the output asset contains XML metadata files that describe the input asset and output asset.  For more information, see the [Input Metadata](../Topic/Input%20Metadata.md) and [Output Metadata](../Topic/Output%20Metadata.md) topics.  
  
 The following characteristics apply to an Asset in Media Services:  
 An Asset is a logical unit that represents a single audiovisual presentation.  
  
 An asset contains a collection of one to many media files.  
  
 The files of an asset are located in a single blob storage container.  
  
 Some examples of an Asset are: a full movie, TV show, specific edit; a clip from a movie, TV show, animation, camera ISO file, or event; a movie trailer or promotional video; an advertisement; an audio file, radio show, podcast, or sound file.  
  
 The following characteristics DO NOT apply to an Asset in Media Services:  
 Simply a storage container  
  
 A folder to organize and store multiple versions of the same presentation in  
  
 A folder for submitting batch processing of multiple audiovisual presentations to Azure Media Encoder  
  
 For example, you must not store a movie, its trailer, an advertisement, and an international edit version of the same movie in a single Asset.  
  
 This topic gives an overview of the `Asset` entity and also demonstrates how to execute various operations with the Media Services REST API.  
  
-   [Asset Entity Properties](../MediaServicesREST/asset.md#asset_entity_properties)  
  
-   [Create an Asset](../MediaServicesREST/asset.md#create_an_asset)  
  
-   [List an Asset](../MediaServicesREST/asset.md#list_an_asset)  
  
-   [Update an Asset](../MediaServicesREST/asset.md#update_an_asset)  
  
-   [Delete an Asset](../MediaServicesREST/asset.md#delete_an_asset)  
  
-   [Publish an Asset](../MediaServicesREST/asset.md#publish_an_asset)  
  
-   [Linking Content Keys to Assets](../MediaServicesREST/asset.md#linking_content_keys_to_assets)  
  
-   [Removing ContentKey Links](../MediaServicesREST/asset.md#removing_contentkey_links)  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://azure.microsoft.com/documentation/articles/media-services-rest-how-to-use/).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
##  <a name="asset_entity_properties"></a> Asset Entity Properties  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`Id`<br /><br /> Read-only. Set by Media Services at creation time.|String|Unique identifier.|  
|`State`<br /><br /> Read-only. Set by Media Services.|Edm.Int32|An enumeration value that describes the state of the asset. Value values are:<br /><br /> -   Initialized = 0<br />-   Published = 1 **Warning:**      The `Publish` action has been deprecated. Remove the code that checks whether an asset is in the `Published` state.<br />-   Deleted = 2<br /><br /> An asset is always in Initialized state until it is deleted.|  
|`Created`<br /><br /> Read-only. Set by Media Services at creation time.|Edm.DateTime|This value is set by Media Services at creation time.|  
|`LastModified`<br /><br /> Read-only. Set by Media Services.|Edm.DateTime|This value is updated by Media Services after any property changes are made.|  
|`AlternateId`<br /><br /> Optional.|Edm.String|An alternate Id value that corresponds to an Id in another content management system. Maximum length is 4000.|  
|`Name`<br /><br /> Optional.|Edm.String|Friendly name for your asset. Maximum length is 512.|  
|`Options`<br /><br /> Required. Cannot be updated after the entity has been created.|Edm.Int32|An enumeration value that describes the encryption options that an Asset can be created with. A valid value is one value from the list below, not a combination of values from this list:<br /><br /> -   **None** = 0: Specifies no asset creation options.<br />-   **StorageEncrypted** = 1:  Specifies that an asset's files should be encrypted on for upload and storage when creating the asset.<br />-   **CommonEncryptionProtected** = 2: Specifies that an asset’s files are protected using a common encryption method (such as PlayReady).<br />-   **EnvelopeEncryptionProtected** = 4|  
|`Uri`<br /><br /> Read-only. Set by Media Services.|Edm.String|The Uri of the blob storage container of the specified Asset.|  
|`Locators`<br /><br /> Read-only. Set by Media Services.|Locator entity set|The returned entity set contains all of the Locator entities that are linked to the specified Asset.|  
|`ContentKeys`<br /><br /> Optional.|ContentKey entity set|The returned entity set contains all of the ContentKey entities that are linked to the specified Asset.|  
|`Files`<br /><br /> Read-only. Set by Media Services.|File entity set|The returned entity set contains all of the File entities that are linked to the specified Asset.|  
|`ParentAssets`<br /><br /> Optional.|Parent Assets entity set|The returned entity set contains all of the parent Asset entities that are linked to the specified Asset.|  
|`StorageAccountName`<br /><br /> Optional. Cannot be updated after the entity has been created.|Edm.String|Name of the storage account that contains the asset’s blob container.<br /><br /> If not specified at creation time, Media Services sets the default storage account name.|  
|`StorageAccount`<br /><br /> Read-only. Set by Media Services.|[StorageAccount](../MediaServicesREST/storageaccount.md) entity set|The returned entity set contains all of the StorageAccount entities that are linked to the specified Asset.|  
|`DeliveryPolicies`|[AssetDeliveryPolicy](../MediaServicesREST/assetdeliverypolicy.md) entity set|The returned entity set contains delivery policies associated with the asset.|  
|`FormatOption`|Edm.Int32|Specifies  different format options that an asset can be created with. Allowed values are:  0 (default) - specifies no asset format option; 1 - specifies that an asset's format will be AdaptiveStreaming.|  
  
##  <a name="create_an_asset"></a> Create an Asset  
 Assets can be created using a POST HTTP request and specifying property values.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/API/Assets|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
POST https://media.windows.net/API/Assets HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d  
Host: media.windows.net  
Content-Length: 27  
Expect: 100-continue  
  
{ "Name" : "NewJSONAsset" }  
```  
  
##  <a name="list_an_asset"></a> List an Asset  
 Assets can be retrieved using a GET HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/Assets|HTTP/1.1|  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/Assets('*assetid*')|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
GET https://media.windows.net/API/Assets('nb:cid:UUID:fccb8cd9-7afa-4365-a36e-d5d68409bb64') HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d  
Host: media.windows.net  
Content-Length: 0  
  
```  
  
##  <a name="update_an_asset"></a> Update an Asset  
 Assets can be updated using a MERGE HTTP request and the specific properties that you want to change.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|MERGE|https://media.windows.net/API/Assets('*assetid*')|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
MERGE https://media.windows.net/API/Assets('nb:cid:UUID:80782407-3f87-4e60-a43e-5e4454232f60') HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337083279&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=DMLQXWah4jO0icpfwyws5k%2b1aCDfz9KDGIGao20xk6g%3d  
Host: media.windows.net  
Content-Length: 21  
Expect: 100-continue  
  
{"Name" : "NewName" }  
```  
  
##  <a name="delete_an_asset"></a> Delete an Asset  
 Assets can be deleted by referencing the Asset Id value. When an asset is deleted, all of its locators are deleted by Microsoft Azure Media Services. If the asset had origin locators, these will be revoked and deleted as well. All links to ContentKeys will be deleted and any ContentKeys not linked to other assets will be deleted.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|DELETE|https://media.windows.net/API/Assets('*assetid*')|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
DELETE https://media.windows.net/API/Assets('nb:cid:UUID:fccb8cd9-7afa-4365-a36e-d5d68409bb64') HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d  
Host: media.windows.net  
Content-Length: 0  
  
```  
  
##  <a name="publish_an_asset"></a> Publish an Asset  
  
> [!NOTE]
>  The `Publish` action has been deprecated. Starting with the latest Media Services release, `Publish` should not be used.  
>   
>  If your code uses `Publish`, be aware of the following considerations:  
>   
>  1.  The `Publish` action does not delete locators associated with the asset. You must explicitly delete the locators in code after calling `Publish`.  
> 2.  The `Publish` action does not set the asset state to `Published`. Remove the code that checks whether an asset is in the `Published` state. Currently, an asset can only have the `Initialized` or `Deleted` state.  
  
##  <a name="linking_content_keys_to_assets"></a> Linking Content Keys to Assets  
 You can link a [ContentKey](../MediaServicesREST/contentkey.md) to an asset by referencing the asset Id with an HTTP POST request. The Uri of the ContentKey must be included in the body of the request. You can only link a ContentKey type that matches the type specified in the asset’s **CreationOptions**. For example, if the Asset has options set to StorageEncrypted(1), the ContentKey must be of the StorageEncryption(1) type.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/API/Assets(‘Asset Id')/$links/ContentKeys|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
POST https://media.windows.net/API/Assets('nb:cid:UUID:3ac4c50a-09c1-4ea3-b39c-c336d97f5a13')/$links/ContentKeys HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=vodbvttest01&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fnimbustestaccounts.accesscontrol.windows.net%2f&Audience=urn%3aNimbus&ExpiresOn=1352143039&Issuer=https%3a%2f%2fnimbustestaccounts.accesscontrol.windows.net%2f&HMACSHA256=sx%2bpdQNrEi8FoEVnwnIK1sXe3GWxXELEFbwKNMQ7BNM%3d  
Host: media.windows.net  
Content-Length: 121  
Expect: 100-continue  
  
{ "uri": "https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A5db89211-c9d9-404b-a6bc-3e6b91c7a214')"}  
  
```  
  
##  <a name="removing_contentkey_links"></a> Removing ContentKey Links  
 You can remove [ContentKey](../MediaServicesREST/contentkey.md) links from an asset by referencing the asset id and the ContentKey Id in a HTTP DELETE request. If the ContentKey is not linked to any other assets, it will be deleted.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|DELETE|https://media.windows.net/API/Assets(‘Asset Id')/$links/ContentKeys('ContentKey Id')|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
DELETE https://media.windows.net/API/Assets('nb:cid:UUID:3ac4c50a-09c1-4ea3-b39c-c336d97f5a13')/$links/ContentKeys('nb:kid:UUID:5db89211-c9d9-404b-a6bc-3e6b91c7a214') HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=vodbvttest01&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fnimbustestaccounts.accesscontrol.windows.net%2f&Audience=urn%3aNimbus&ExpiresOn=1352143039&Issuer=https%3a%2f%2fnimbustestaccounts.accesscontrol.windows.net%2f&HMACSHA256=sx%2bpdQNrEi8FoEVnwnIK1sXe3GWxXELEFbwKNMQ7BNM%3d  
Host: media.windows.net  
Content-Length: 0  
  
```  
  
## See Also  
 [AccessPolicy](../MediaServicesREST/accesspolicy.md)   
 [ContentKey](../MediaServicesREST/contentkey.md)   
 [AssetFile](../MediaServicesREST/assetfile.md)   
 [Job](../MediaServicesREST/job.md)   
 [JobTemplate](../MediaServicesREST/jobtemplate.md)   
 [Locator](../MediaServicesREST/locator.md)   
 [MediaProcessor](../MediaServicesREST/mediaprocessor.md)   
 [Task](../MediaServicesREST/task.md)   
 [TaskTemplate](../MediaServicesREST/tasktemplate.md)   
 [Ingesting Assets with the Media Services REST API](http://msdn.microsoft.com/en-us/efeb5012-9a00-4d02-9712-5fe4b2043257)   
 [Quotas and Limitations](http://msdn.microsoft.com/en-us/82f7e538-6bdf-4883-aa50-24574cc4996e)
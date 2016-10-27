---
title: "Locator"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: ecb814ae-e258-4f42-93ea-1f03a61402e9
caps.latest.revision: 53
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
# Locator
`Locator` provides an entry point to access the files contained in an Asset. An AccessPolicy is used to define the permissions and duration that a client has access to a given Asset. Locators can have a many to one relationship with an AccessPolicy, such that different Locators can provide different start times and connection types to different clients while all using the same permission and duration settings; however, because of a shared access policy restriction set by Azure storage services, you cannot have more than five unique Locators associated with a given Asset at one time. For more information, see [Using a Shared Access Signature (REST API)](http://msdn.microsoft.com/library/windowsazure/ee395415.aspx).  
  
 Often, you need to transform a `Locator` Uri in order to access various file formats. For example, the SAS locator’s `Path` property gives access to the container. To access files, you need to embed the file name between the host and SAS signature. When working with OnDemandOrigin locators, the `Path` property is not useful until protocol specific part is added to it.  
  
 The following rules govern when a Locator can be created and updated:  
  
1.  Access Signature (SAS) URL Locators used with AccessPolicies that define read permissions, as well as Origin Locators, cannot be created until after the files have been uploaded to an Asset.. SAS URL Locators, which are used to download or upload files, can be created before the files are uploaded only if they are used with AccessPolicies that specify write permissions.  
  
2.  You cannot update a SAS URL Locator after it has been created; however, other Locator types, such as origin locators, can be updated with new StartTime values.  
  
3.  SAS locators' URLs will change every time  storage keys of the associated storage account get updated. For more information, see [How To: Update Media Services after Rolling Storage Access Keys](http://azure.microsoft.com/documentation/articles/media-services-roll-storage-access-keys/)  
  
4.  There may be a 30-40 second delay after a Locator is created to when it is available for use. This issue applies to both SAS URL and OnDemandOrigin locators.  
  
> [!NOTE]
>  Locators are not designed for managing per-user access control. To give different access rights to individual users, use Digital Rights Management (DRM) solutions.  
  
 This topic gives an overview of the `Locator` entity and also demonstrates how to execute various operations with the Media Services REST API.  
  
-   [Locator Entity Properties](../MediaServicesREST/locator.md#locator_entity_properties)  
  
-   [Create a Locator](../MediaServicesREST/locator.md#create_a_locator)  
  
-   [List Locators](../MediaServicesREST/locator.md#list_locators)  
  
-   [Update a Locator](../MediaServicesREST/locator.md#update_a_locator)  
  
-   [Delete a Locator](../MediaServicesREST/locator.md#delete_a_locator)  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://msdn.microsoft.com/en-us/42ae6204-93bc-4797-bf40-1c68512cfb73).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
##  <a name="locator_entity_properties"></a> Locator Entity Properties  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`Id`<br /><br /> Optional. Cannot be updated after the entity has been created.|Edm.String|Unique identifier set by Media Services.|  
|`Name`<br /><br /> Optional.|Edm.String|The name of the locator. Maximum length is 4000.|  
|`ExpirationDateTime`<br /><br /> Write-only. Use a MERGE HTTP request, to update the ExpirationDateTime value.|Edm.DateTime|The value (represented in milliseconds since midnight Jan 1, 1970) when the locator can no longer be used to access the specified asset.<br /><br /> The ExpirationDateTime must be in the following DateTime format: `YYYY-MM-DDTHH:mm:ssZ` (for example, "2014-05-23T17:53:50Z").|  
|`Type`<br /><br /> Required. Cannot be updated after the entity has been created.|Edm.Int32|Enumeration value that describes the type of Locator. Valid values are:<br /><br /> -   **None** = 0 : This is the default enumeration value. No valid locator will have this type<br />-   **SAS** = 1 : Specifies Shared Access Signature (Sas) locator type<br />-   **OnDemandOrigin** = 2 :  Specifies a locator type which refers to an Azure Media Service On Demand Origin streaming endpoint|  
|`Path`<br /><br /> Read-only. Set by Media Services.|Edm.String|URL used for accessing Asset files.|  
|`BaseUri`<br /><br /> Read-only. Set by Media Services.|Edm.String|Part of the locator that provides the store/service/container information about the asset. (for example, Dns Host name http://someservice.cloudapp.net)|  
|`ContentAccessComponent`<br /><br /> Read-only. Set by Media Services.|Edm.String|Part of the URI needed to access the content. The location of this token in the final media URL depends on the locator type, media type and streaming service.|  
|`AccessPolicyId`<br /><br /> Read-only. Set by Media Services.|Edm.String|The Id of the AccessPolicy that defines the permissions and duration for the Locator URL.<br /><br /> Note that the List permission should not be used when creating OnDemandOrigin locators.|  
|`AssetId`<br /><br /> Read-only. Set by Media Services.|Edm.String|The Id of the Asset that contains the content you want to provide access to.|  
|`StartTime`<br /><br /> Optional.|Edm.DateTime|The date and time when your locator will be available for clients to use. **Tip:**  If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time. This is because there may be clock skew between your client machine and Media Services. Also, your StartTime value must be in the following DateTime format: `YYYY-MM-DDTHH:mm:ssZ` (for example, "2014-05-23T17:53:50Z").|  
|`AssetPolicy`<br /><br /> Read-only. Set by Media Services.|`AssetPolicy` entity set|Navigation property to an AccessPolicy instance.|  
|`Asset`<br /><br /> Read-only. Set by Media Services.|`Asset` entity set|Navigation property to an Asset instance.|  
  
##  <a name="create_a_locator"></a> Create a Locator  
 Locators can be created with a POST HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/API/Locators|HTTP/1.1|  
  
> [!NOTE]
>  SAS locators' URLs will change every time  storage keys of the associated storage account get updated. For more information, see [How To: Update Media Services after Rolling Storage Access Keys](http://azure.microsoft.com/documentation/articles/media-services-roll-storage-access-keys/)  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
POST https://media.windows.net/API/Locators HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337212980&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kK7PbPM3lTAEJYIx5OTWeaSY7zvia358UjPiuvSFHz0%3d  
Host: media.windows.net  
Content-Length: 182  
Expect: 100-continue  
  
{"AccessPolicyId": "nb:pid:UUID:25544a8f-8ccf-43b1-a188-2a860b35bffa", "AssetId" : "nb:cid:UUID:d062e5ef-e496-4f21-87e7-17d210628b7c", "StartTime" : "2014-05-17T16:45:53", "Type":1}  
```  
  
 For more information, see [Delivering Assets with the Media Services REST API](http://msdn.microsoft.com/en-us/644d9f8c-2b22-43e4-828d-f6c1eae5ff96).  
  
##  <a name="list_locators"></a> List Locators  
 Locators can be retrieved using a GET HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|GET https://media.windows.net/API/Locators|HTTP/1.1|  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/Locators('*locatorid*')|HTTP/1.1|  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/Assets('*assetid*')/Locators|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
GET https://media.windows.net/API/Locators('nb:lid:UUID:627cbafb-3d81-4623-97c2-2194282b6d16') HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337219077&Issuer=https%3a%2f%2fnimbustestaccounts.accesscontrol.windows.net%2f&HMACSHA256=JSeCQMLMDLIm%2fFD%2b8qJL52dShVNGdwg1aqB%2b3GLlq5I%3d  
Host: media.windows.net  
```  
  
##  <a name="update_a_locator"></a> Update a Locator  
 Origin Locators can be updated using a MERGE HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|MERGE|https://media.windows.net/API/Locators('*locatorid*')|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
MERGE https://media.windows.net/API/Locators('nb:lid:UUID:5bfcb65d-843d-4d5e-bf71-9306ecb08203') HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337219313&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=iULfw27Jo4TIBljQr8MDMDh2TX6YZBShgvY9yblaqKU%3d  
Host: media.windows.net  
Content-Length: 38  
Expect: 100-continue  
  
{"StartTime" : "2014-05-17T16:45:53"}  
```  
  
##  <a name="delete_a_locator"></a> Delete a Locator  
 Locators can be deleted using a DELETE HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|DELETE|https://media.windows.net/API/Locators('*locatorid*')|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
DELETE https://media.windows.net/API/Locators('nb:lid:UUID:9f0e0cee-8ea5-46c4-b985-5a7cd30e7623') HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337219313&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=iULfw27Jo4TIBljQr8MDMDh2TX6YZBShgvY9yblaqKU%3d  
Host: media.windows.net  
Content-Length: 0  
Connection: Keep-Alive  
```  
  
## See Also  
 [Delivering Assets with the Media Services REST API](http://msdn.microsoft.com/en-us/644d9f8c-2b22-43e4-828d-f6c1eae5ff96)   
 [ContentKey](../MediaServicesREST/contentkey.md)   
 [Asset](../MediaServicesREST/asset.md)   
 [AccessPolicy](../MediaServicesREST/accesspolicy.md)   
 [AssetFile](../MediaServicesREST/assetfile.md)   
 [JobTemplate](../MediaServicesREST/jobtemplate.md)   
 [Job](../MediaServicesREST/job.md)   
 [MediaProcessor](../MediaServicesREST/mediaprocessor.md)   
 [Task](../MediaServicesREST/task.md)   
 [TaskTemplate](../MediaServicesREST/tasktemplate.md)   
 [Quotas and Limitations](http://msdn.microsoft.com/en-us/82f7e538-6bdf-4883-aa50-24574cc4996e)
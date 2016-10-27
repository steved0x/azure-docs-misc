---
title: "ContentKey"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: ef4dfeeb-48ae-4596-ab28-44d6b36d8769
caps.latest.revision: 41
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
# ContentKey
A ContentKey provides secure access to an Asset. In addition to creating a ContentKey entity, you must also use a protection key to encrypt the content key that you generate. For more information on retrieving the protection key, see [Encrypt the Asset (Optional)](http://msdn.microsoft.com/en-us/efeb5012-9a00-4d02-9712-5fe4b2043257) and [REST API Functions](../MediaServicesREST/rest-api-functions.md).  
  
 This topic gives an overview of the `ContentKey` entity and also demonstrates how to execute various operations with the Media Services REST API.  
  
-   [ContentKey Entity Properties](../MediaServicesREST/contentkey.md#contentkey_properties)  
  
-   [Create a ContentKey](../MediaServicesREST/contentkey.md#create_a_contentkey)  
  
-   [Get Key Delivery URL](#get_delivery_service_url)  
  
-   [List ContentKeys](../MediaServicesREST/contentkey.md#list_a_contentkey)  
  
-   [Delete a ContentKey](../MediaServicesREST/contentkey.md#delete_a_contentkey)  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://msdn.microsoft.com/en-us/42ae6204-93bc-4797-bf40-1c68512cfb73).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
##  <a name="contentkey_properties"></a> ContentKey Entity Properties  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`Id`<br /><br /> Required. This value is not set by Media Services.|Edm.String|User defined unique identifier.|  
|`Created`<br /><br /> Read-only. Set by Media Services at creation time.|Edm.DateTime|This value is set by Media Services at creation time.|  
|`LastModified`<br /><br /> Read-only. Set by Media Services.|Edm.DateTime|This value is updated by Media Services after any property changes are made.|  
|`ContentKeyType`<br /><br /> Optional.|Edm.Int32|An enumeration value that specifies the content key type. Valid values are:<br /><br /> -   CommonEncryption = 0<br />-   StorageEncryption = 1<br />-   ConfigurationEncryption = 2<br />-   EnvelopeEncryption = 4|  
|`EncryptedContentKey`<br /><br /> Optional.|Edm.String|Content key encrypted with the public key of the X.509 certificate. Maximum length is 4000.|  
|`Name`<br /><br /> Optional.|Edm.String|Friendly name for your ContentKey. Maximum length is 4000.|  
|`ProtectionKeyId`<br /><br /> Optional.|Edm.String|Thumbprint of the X.509 certificate that is used to encrypt the storage, common encryption, or configuration encryption keys. This value is returned to you when calling the GetProtectionKeyId function. Maximum length is 4000.|  
|`ProtectionKeyType`<br /><br /> Optional.|Edm.Int32|An enumeration value that specifies the protection key type. Valid values are:<br /><br /> -   X509CertificateThumbprint = 0|  
|`Checksum`<br /><br /> Optional.|Edm.String|The checksum of the ContentKey. Maximum length is 4000.|  
|`AuthorizationPolicyId`|Edm.String|The authorization policy id associated with the ContentKey.|  
  
##  <a name="create_a_contentkey"></a> Create a ContentKey  
 ContentKeys can be created using a POST HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/API/ContentKeys|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values. For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
POST https://media.windows.net/api/ContentKeys HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334276569&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Cax61TKgo%2fLo5k6AWA%2brOLdAbMMd4poqvpVqiRPdTXk%3d  
Host: media.windows.net  
Content-Length: 572  
Expect: 100-continue  
  
{"Id" : "nb:kid:UUID:316d14d4-b603-4d90-b8db-0fede8aa48f8", "ContentKeyType" : 1, "EncryptedContentKey" : "Y4NPej7heOFa2vsd8ZEOcjjpu/qOq3RJ6GRfxa8CCwtAM83d6J2mKOeQFUmMyVXUSsBCCOdufmieTKi+hOUtNAbyNM4lY4AXI537b9GaY8oSeje0NGU8+QCOuf7jGdRac5B9uIk7WwD76RAJnqyep6U/OdvQV4RLvvZ9w7nO4bY8RHaUaLxC2u4aIRRaZtLu5rm8GKBPy87OzQVXNgnLM01I8s3Z4wJ3i7jXqkknDy4VkIyLBSQvIvUzxYHeNdMVWDmS+jPN9ScVmolUwGzH1A23td8UWFHOjTjXHLjNm5Yq+7MIOoaxeMlKPYXRFKofRY8Qh5o5tqvycSAJ9KUqfg==", "ProtectionKeyId" : "7D9BB04D9D0A4A24800CADBFEF232689E048F69C", "ProtectionKeyType" : 1, "Checksum" : "TfXtjCIlq1Y=" }  
  
```  
  
##  <a name="get_delivery_service_url"></a> Get Key Delivery URL  
 Gets the key delivery URL for the specified delivery method of the content key. A client uses the returned URL to request an AES key or a PlayReady license in order to playback the protected content.  
  
 Specify the type of the URL to get in the body of the HTTP request. If you are protecting your content with PlayReady, request a Media Services PlayReady license acquisition URL, using `1` for the `keyDeliveryType`: `{"keyDeliveryType":1}`. If you are protecting your content with the envelope encryption, request a key acquisition URL by specifying `2` for `keyDeliveryType`: `{"keyDeliveryType":2}`.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/api/ContentKeys('*ContentkeyId*')/GetKeyDeliveryUrl|HTTP/1.1|  
  
### Sample  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. The example gets the PlayReady license acquisition URL.  
  
 Make sure to use valid redirected host URI and authorization bearer token values. For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
 Request headers:  
  
```  
POST https://media.windows.net/api/ContentKeys('nb:kid:UUID:14e7e815-5db3-4027-9578-a55a416a3367')/GetKeyDeliveryUrl HTTP/1.1  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json  
Accept-Charset: UTF-8  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334276569&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Cax61TKgo%2fLo5k6AWA%2brOLdAbMMd4poqvpVqiRPdTXk%3d  
x-ms-version: 2.9  
Content-Type: application/json  
Host: media.windows.net  
Content-Length: 21  
  
```  
  
 Request body:  
  
```  
{"keyDeliveryType":1}  
```  
  
 If successful, this operation returns a **200 OK** status code and the specified URL. For example:  `https://account001.keydelivery.mediaservices.windows.net/PlayReady/`.  
  
##  <a name="list_a_contentkey"></a> List ContentKeys  
 ContentKeys are retrieved using a GET HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/ContentKeys|HTTP/1.1|  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/ContentKeys('*contentkeyid*')|HTTP/1.1|  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/Assets('*assetid*')/ContentKeys|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values. For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
GET https://media.windows.net/API/ContentKeys('nb:kid:UUID:58b522a5-be4e-4988-8958-ee0cdb179273') HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334276569&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Cax61TKgo%2fLo5k6AWA%2brOLdAbMMd4poqvpVqiRPdTXk%3d  
Host: media.windows.net  
  
```  
  
##  <a name="delete_a_contentkey"></a> Delete a ContentKey  
 ContentKeys are deleted through a DELETE HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|DELETE|https://media.windows.net/API/ContentKeys('*contentkeyid*')|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab.  
  
 Make sure to use valid redirected host URI and authorization bearer token values. For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
DELETE https://media.windows.net/API/ContentKeys('nb:kid:UUID:58b522a5-be4e-4988-8958-ee0cdb179273') HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337159050&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Pq9NUjGajGnOXSZQphVl2UsHeCdrxRiWbxTSv5n6cPY%3d  
Host: media.windows.net  
Content-Length: 0  
  
```  
  
## See Also  
 [AccessPolicy](../MediaServicesREST/accesspolicy.md)   
 [Asset](../MediaServicesREST/asset.md)   
 [AssetFile](../MediaServicesREST/assetfile.md)   
 [Job](../MediaServicesREST/job.md)   
 [JobTemplate](../MediaServicesREST/jobtemplate.md)   
 [Locator](../MediaServicesREST/locator.md)   
 [MediaProcessor](../MediaServicesREST/mediaprocessor.md)   
 [Task](../MediaServicesREST/task.md)   
 [TaskTemplate](../MediaServicesREST/tasktemplate.md)   
 [Quotas and Limitations](http://msdn.microsoft.com/en-us/82f7e538-6bdf-4883-aa50-24574cc4996e)
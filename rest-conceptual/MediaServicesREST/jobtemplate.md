---
title: "JobTemplate"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 325e32c4-4a48-4694-bcb9-e5c562121ce0
caps.latest.revision: 33
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
# JobTemplate
A JobTemplate provides reusable settings for Jobs that need to be run repeatedly.  
  
 This topic gives an overview of the `JobTemplate` entity and also demonstrates how to execute various operations with the Media Services REST API.  
  
-   [Job Template Entity Properties](../MediaServicesREST/jobtemplate.md#jobtemplate_entity_properties)  
  
-   [Create a JobTemplate](../MediaServicesREST/jobtemplate.md#create_a_jobtemplate)  
  
-   [List JobTemplates](../MediaServicesREST/jobtemplate.md#list_jobtemplates)  
  
-   [Delete a JobTemplate](../MediaServicesREST/jobtemplate.md#delete_a_jobtemplate)  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://msdn.microsoft.com/en-us/42ae6204-93bc-4797-bf40-1c68512cfb73).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
##  <a name="jobtemplate_entity_properties"></a> JobTemplate Entity Properties  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`Id`<br /><br /> Read-only. Set by Media Services at creation time.|Edm.String|Unique identifier.|  
|`Name`<br /><br /> Optional.|Edm.String|Friendly name for the job template.|  
|`Created`<br /><br /> Read-only. Set by Media Services at creation time.|Edm.DateTime|Represents the number of milliseconds since midnight Jan 1, 1970.|  
|`LastModified`<br /><br /> Read-only. Set by Media Services.|Edm.DateTime|This value is updated by Media Services after any property changes are made. It represents the number of milliseconds since midnight Jan 1, 1970.|  
|`JobTemplateBody`<br /><br /> Required.|Edm.String|An Xml document that defines what TaskTemplates and the number of input and output assets to use. For example,<br /><br /> `<?xml version="1.0" encoding="utf-8"?>      <jobTemplate>         <taskBody taskTemplateId=”nb:ttid:UUID:0749DF78-5167-413D-91AA-31564ED1EF34”> … </taskBody>         <taskBody taskTemplateId=”nb:ttid:UUID:0432DF78-5167-4132-942A-88241ED1AC34”> … </taskBody>     </jobtemplate>`<br /><br /> The format for the `TaskBody` content is the same as the [Task](../MediaServicesREST/task.md)’s `TaskBody` property plus the `TaskTemplateId` (or `taskTemplateId`) attribute. Each `TaskTemplateId` should be unique and correspond to the `TaskTemplate` in the `TaskTemplates` collection. The number of `TaskBody` elements has to be the same as the count of the `TaskTemplates` collection.|  
|`NumberofInputAssets`<br /><br /> Optional. Cannot be updated after the entity has been created.|Edm.Int32|The number of input assets that can be used with this JobTemplate.|  
|`TemplateType`<br /><br /> Required. Cannot be updated after the entity has been created.|Edm.Int32|The type of JobTemplate that can be created. Valid values are:<br /><br /> - SystemLevel = 0<br /><br /> - AccountLevel  = 1<br /><br /> **Note**: SystemLevel JobTemplate types are reserved for Media Services. You must set this value to AccountLevel (that is "1").|  
|`TaskTemplates`<br /><br /> Required.|TaskTemplates entity set|Navigation property that references all associated TaskTemplate entities.|  
  
##  <a name="create_a_jobtemplate"></a> Create a JobTemplate  
 JobTemplates can be created with a POST HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/API/JobTemplates|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
POST https://media.windows.net/API/JobTemplates HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337212980&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kK7PbPM3lTAEJYIx5OTWeaSY7zvia358UjPiuvSFHz0%3d  
Host: media.windows.net  
Content-Length: 608  
Expect: 100-continue  
  
{"Name" : "NewJobTemplate14ad96d1-2d14-4618-9014-08db7d227062", "TemplateType" : "1",  "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H.264 iPad", "MediaProcessorId" : "nb:mpid:UUID:2f381738-c504-4e4a-a38e-d199e207fcd5", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }  
  
```  
  
##  <a name="list_jobtemplates"></a> List JobTemplates  
 JobTemplates can be retrieved using a GET HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/JobTemplates|HTTP/1.1|  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/JobTemplates('nb:jtid:UUID:ed10f137-7a8e-8343-9110-f54603d1136f')|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:ed10f137-7a8e-8343-9110-f54603d1136f') HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337212980&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kK7PbPM3lTAEJYIx5OTWeaSY7zvia358UjPiuvSFHz0%3d  
Host: media.windows.net  
  
```  
  
##  <a name="delete_a_jobtemplate"></a> Delete a JobTemplate  
 JobTemplates can be deleted using a DELETE HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|DELETE|https://media.windows.net/API/JobTemplates('*jobtemplateid*')|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
DELETE https://media.windows.net/API/JobTemplates('nb:jtid:UUID:1149a161-92c6-be40-8e9c-7bf640c05df6') HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337178759&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=cKlWvRDsu0bQwDkc1A4sMM5OQOGBEk8OWcuaj9zDkp0%3d  
Host: media.windows.net  
Content-Length: 0  
  
```  
  
## See Also  
 [ContentKey](../MediaServicesREST/contentkey.md)   
 [Asset](../MediaServicesREST/asset.md)   
 [AccessPolicy](../MediaServicesREST/accesspolicy.md)   
 [AssetFile](../MediaServicesREST/assetfile.md)   
 [Job](../MediaServicesREST/job.md)   
 [Locator](../MediaServicesREST/locator.md)   
 [MediaProcessor](../MediaServicesREST/mediaprocessor.md)   
 [Task](../MediaServicesREST/task.md)   
 [TaskTemplate](../MediaServicesREST/tasktemplate.md)   
 [Quotas and Limitations](http://msdn.microsoft.com/en-us/82f7e538-6bdf-4883-aa50-24574cc4996e)
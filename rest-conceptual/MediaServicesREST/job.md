---
title: "Job"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 5100ddd7-92ff-4c37-84d2-4f84fee250a7
caps.latest.revision: 57
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
# Job
A job is an entity that contains metadata about a set of tasks. Each task performs an atomic operation on the input asset(s). A job is typically used to process one audio/video presentation. If you are processing multiple videos, create a job for each video to be encoded.  
  
 This topic gives an overview of the `Job` entity and also demonstrates how to execute various operations with the Media Services REST API.  
  
-   [Job Entity Properties](../MediaServicesREST/job.md#job_entity_properties)  
  
-   [Create a Job with Notification Subscriptions](../MediaServicesREST/job.md#create_jobs_with_notifications)  
  
-   [Create a Job](../MediaServicesREST/job.md#create_a_job)  
  
-   [List Jobs](../MediaServicesREST/job.md#list_jobs)  
  
-   [Cancel a Job](../MediaServicesREST/job.md#cancel_a_job)  
  
-   [Delete a Job](../MediaServicesREST/job.md#delete_job)  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://msdn.microsoft.com/en-us/42ae6204-93bc-4797-bf40-1c68512cfb73).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
> -   When using JSON and specifying to use the __metadata keyword in the request (for example, to references a linked object) you MUST set the Accept header to JSON Verbose format (Accept: application/json;odata=verbose). Odata does not understand the \__metadata property in the request, unless you set it to verbose.  
  
##  <a name="job_entity_properties"></a> Job Entity Properties  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`Id`<br /><br /> Read-only. Set by Media Services at creation time.|Edm.String|Unique identifier.|  
|`Name`<br /><br /> Optional.|Edm.String|Friendly name for the job. Maximum length is 4000.|  
|`Created`<br /><br /> Read-only. Set by Media Services at creation time.|Edm.DateTime|Represents the number of milliseconds since midnight Jan 1, 1970.|  
|`LastModified`<br /><br /> Read-only. Set by Media Services.|Edm.DateTime|This value is updated by Media Services after any property changes are made. It represents the number of milliseconds since midnight Jan 1, 1970.|  
|`EndTime`<br /><br /> Read-only. Set by Media Services.|Edm.DateTime|The datetime when the job completed, failed, or was cancelled.|  
|`Priority`<br /><br /> Optional.|Edm.Int32|The Priority of the job. A higher value indicates a higher priority relative to your other scheduled jobs. For example, a job with Priority = 40 will be processed before a job with Priority = 30. The upper bound is equal to MaxInt. The default is 0.|  
|`RunningDuration`<br /><br /> Read-only. Set by Media Services.|Edm.Double|The elapsed time (in seconds) for the job|  
|`StartTime`<br /><br /> Read-only. Set by Media Services.|Edm.DateTime|The datetime when the job started.|  
|`State`<br /><br /> Read-only. Set by Media Services.|Edm.Int32|The State of the job. This is an aggregate of the Tasks state. If one Task fails, this property would be set to Failed. Valid values are:<br /><br /> -   Queued = 0<br />-   Scheduled = 1<br />-   Processing = 2<br />-   Finished = 3<br />-   Error = 4<br />-   Canceled = 5<br />-   Canceling = 6|  
|`TemplateId`<br /><br /> Optional.|Edm.String|Id of the JobTemplate entity.|  
|`InputMediaAssets`<br /><br /> Required.|Assets entity set|Navigation property that references all associated Asset entities that act as input assets to the Job.|  
|`OutputMediaAssets`<br /><br /> Read-only. Set by Media Services.|Assets entity set|Navigation property that references all associated Asset entities that act as output assets to the Job. The assets and their blob storage containers are created upon job creation.<br /><br /> Output assets contain files (including video, audio, thumbnails, etc.) and also the metadata about the input and output assets. For more information, see the [Asset](../MediaServicesREST/asset.md) and [Output Metadata](../Topic/Output%20Metadata.md) topics.|  
|`Tasks`<br /><br /> Optional.|Tasks entity set|Navigation property that references all associated Task entities.|  
|`JobNotificationSubscriptions`<br /><br /> Optional. Cannot be updated after the entity has been created.|[JobNotificationSubscription](../MediaServicesREST/jobnotificationsubscription.md)<br /><br /> This property was added in Media Services version 2.1. **Warning:**  Azure queue notification may have some delay.|Navigation property that references notification subscriptions for the job.<br /><br /> This property cannot be updated after the job has been created.|  
  
##  <a name="create_a_job"></a> Create a Job without notification subscriptions  
 Jobs can be created with a HTTP POST request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/API/Jobs|HTTP/1.1|  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 The following code shows how to create a request using Media Services version 2.0. Remember that when using JSON and specifying to use the __metadata keyword in the request (for example, to references a linked object) you MUST set the Accept header to JSON Verbose format (Accept: application/json;odata=verbose). Odata does not understand the \__metadata property in the request, unless you set it to verbose.  
  
```  
POST https://media.windows.net/API/Jobs HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d   
Host: media.windows.net  
Content-Length: 474  
Expect: 100-continue  
  
{"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aba5356eb-30ff-4dc6-9e5a-41e4223540e7')"}}], "Tasks" : [{"Configuration" : "H.264 HD 720p VBR", "MediaProcessorId" : "nb:mpid:UUID:2f381738-c504-4e4a-a38e-d199e207fcd5", "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}  
  
```  
  
##  <a name="create_jobs_with_notifications"></a> Create a Job with notification subscriptions  
 Jobs with notifications can be creating using HTTP POST batch request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/API/$batch|HTTP/1.1|  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 The following example code creates an encoding `Job` with notification subscriptions for the job. Note that the `JobNotificationSubscriptions` property was added in Media Services version 2.5. Remember that when using JSON and specifying to use the __metadata keyword in the request (for example, to references a linked object) you MUST set the Accept header to JSON Verbose format (Accept: application/json;odata=verbose). Odata does not understand the \__metadata property in the request, unless you set it to verbose.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
POST https://media.windows.net/API/$batch HTTP/1.1  
User-Agent: Microsoft ADO.NET Data Services  
DataServiceVersion: 1.0  
MaxDataServiceVersion: 3.0  
Accept: multipart/mixed  
Accept-Charset: UTF-8  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d   
x-ms-version: 2.11  
Content-Type: multipart/mixed; boundary=batch_c8ccf56a-87f6-4a61-bfa2-46aac3bb87d9  
Host: media.windows.net  
Content-Length: 3856  
  
--batch_c8ccf56a-87f6-4a61-bfa2-46aac3bb87d9  
Content-Type: multipart/mixed; boundary=changeset_0e31bdec-b799-400c-aa2f-d040aaa6ef2d  
  
--changeset_0e31bdec-b799-400c-aa2f-d040aaa6ef2d  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
POST https://media.windows.net/API/Jobs HTTP/1.1  
Content-ID: 1  
Content-Type: application/atom+xml  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/atom+xml,application/xml  
Accept-Charset: UTF-8  
  
<?xml version="1.0" encoding="utf-8"?><entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns:georss="http://www.georss.org/georss" xmlns:gml="http://www.opengis.net/gml"><link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/InputMediaAssets" type="application/atom+xml;type=feed" title="InputMediaAssets" href="https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A33662ded-f00b-4020-9fcf-4c4a22070c01')" /><id /><title /><updated>2013-04-20T22:41:57Z</updated><author><name /></author><content type="application/xml"><m:properties><d:Created m:type="Edm.DateTime">0001-01-01T00:00:00</d:Created><d:EndTime m:null="true" /><d:Id m:null="true" /><d:JobNotificationSubscriptions><d:element><d:NotificationEndPointId>nb:nepid:UUID:36e510df-8560-4bae-a698-87723f677e98</d:NotificationEndPointId><d:TargetJobState m:type="Edm.Int32">2</d:TargetJobState></d:element></d:JobNotificationSubscriptions><d:LastModified m:type="Edm.DateTime">0001-01-01T00:00:00</d:LastModified><d:Name>My MP4 to Smooth Streaming encoding job</d:Name><d:Priority m:type="Edm.Int32">0</d:Priority><d:RunningDuration m:type="Edm.Double">0</d:RunningDuration><d:StartTime m:null="true" /><d:State m:type="Edm.Int32">0</d:State><d:TemplateId m:null="true" /></m:properties></content></entry>  
--changeset_0e31bdec-b799-400c-aa2f-d040aaa6ef2d  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
POST https://media.windows.net/API/$1/Tasks HTTP/1.1  
Content-ID: 2  
Content-Type: application/atom+xml  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
Accept: application/atom+xml,application/xml  
Accept-Charset: UTF-8  
  
<?xml version="1.0" encoding="utf-8"?><entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns:georss="http://www.georss.org/georss" xmlns:gml="http://www.opengis.net/gml"><id /><title /><updated>2013-04-20T22:41:57Z</updated><author><name /></author><content type="application/xml"><m:properties><d:Configuration>H264 Smooth Streaming 720p</d:Configuration><d:EncryptionKeyId m:null="true" /><d:EncryptionScheme m:null="true" /><d:EncryptionVersion m:null="true" /><d:EndTime m:null="true" /><d:ErrorDetails /><d:HistoricalEvents /><d:Id></d:Id><d:InitializationVector m:null="true" /><d:MediaProcessorId>nb:mpid:UUID:70bdc2c3-ebf4-42a9-8542-5afc1e55d217</d:MediaProcessorId><d:Name>My Mp4 to Smooth Task</d:Name><d:Options m:type="Edm.Int32">0</d:Options><d:PerfMessage m:null="true" /><d:Priority m:type="Edm.Int32">0</d:Priority><d:Progress m:type="Edm.Double">0</d:Progress><d:RunningDuration m:type="Edm.Double">0</d:RunningDuration><d:StartTime m:null="true" /><d:State m:type="Edm.Int32">0</d:State><d:TaskBody><?xml version="1.0" encoding="utf-16"?>  
<taskBody>  
  <inputAsset>JobInputAsset(0)</inputAsset>  
  <outputAsset assetCreationOptions="0" assetName="Output asset">JobOutputAsset(0)</outputAsset>  
</taskBody></d:TaskBody></m:properties></content></entry>  
--changeset_0e31bdec-b799-400c-aa2f-d040aaa6ef2d--  
--batch_c8ccf56a-87f6-4a61-bfa2-46aac3bb87d9--  
  
```  
  
 The following is the response for job creation with notifications:  
  
```  
HTTP/1.1 202 Accepted  
Cache-Control: no-cache  
Content-Length: 6056  
Content-Type: multipart/mixed; boundary=batchresponse_2ae0b2a5-ec8b-438b-ae62-a02bf2b4a502  
Server: Microsoft-IIS/7.5  
request-id: 9a3f6a5e-8363-42db-97bd-1f693b71f7f0  
x-ms-request-id: 9a3f6a5e-8363-42db-97bd-1f693b71f7f0  
X-Content-Type-Options: nosniff  
DataServiceVersion: 1.0;  
X-Powered-By: ASP.NET  
Date: Sat, 20 Apr 2013 22:42:02 GMT  
  
--batchresponse_2ae0b2a5-ec8b-438b-ae62-a02bf2b4a502  
Content-Type: multipart/mixed; boundary=changesetresponse_10441dcf-ec34-4b8a-919e-2368b2c6444e  
  
--changesetresponse_10441dcf-ec34-4b8a-919e-2368b2c6444e  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
HTTP/1.1 201 Created  
DataServiceVersion: 3.0;  
Content-Type: application/atom+xml;type=entry;charset=utf-8  
Content-ID: 1  
X-Content-Type-Options: nosniff  
Cache-Control: no-cache  
Location: https://media.windows.net/api/Jobs('nb%3Ajid%3AUUID%3A7dc2642f-ab1e-9f4c-8ecd-027eeac2a4ab')  
  
<?xml version="1.0" encoding="utf-8"?><entry xml:base="https://media.windows.net/api/" xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns:georss="http://www.georss.org/georss" xmlns:gml="http://www.opengis.net/gml"><id>https://media.windows.net/api/Jobs('nb%3Ajid%3AUUID%3A7dc2642f-ab1e-9f4c-8ecd-027eeac2a4ab')</id><category term="Microsoft.Cloud.Media.Vod.Rest.Data.Models.Job" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" /><link rel="edit" title="Job" href="Jobs('nb%3Ajid%3AUUID%3A7dc2642f-ab1e-9f4c-8ecd-027eeac2a4ab')" /><link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/Tasks" type="application/atom+xml;type=feed" title="Tasks" href="Jobs('nb%3Ajid%3AUUID%3A7dc2642f-ab1e-9f4c-8ecd-027eeac2a4ab')/Tasks" /><link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/OutputMediaAssets" type="application/atom+xml;type=feed" title="OutputMediaAssets" href="Jobs('nb%3Ajid%3AUUID%3A7dc2642f-ab1e-9f4c-8ecd-027eeac2a4ab')/OutputMediaAssets" /><link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/InputMediaAssets" type="application/atom+xml;type=feed" title="InputMediaAssets" href="Jobs('nb%3Ajid%3AUUID%3A7dc2642f-ab1e-9f4c-8ecd-027eeac2a4ab')/InputMediaAssets" /><title /><updated>2013-04-20T22:42:02Z</updated><author><name /></author><content type="application/xml"><m:properties><d:Id>nb:jid:UUID:7dc2642f-ab1e-9f4c-8ecd-027eeac2a4ab</d:Id><d:Name>My MP4 to Smooth Streaming encoding job</d:Name><d:Created m:type="Edm.DateTime">0001-01-01T00:00:00</d:Created><d:LastModified m:type="Edm.DateTime">0001-01-01T00:00:00</d:LastModified><d:EndTime m:null="true" /><d:Priority m:type="Edm.Int32">0</d:Priority><d:RunningDuration m:type="Edm.Double">0</d:RunningDuration><d:StartTime m:null="true" /><d:State m:type="Edm.Int32">0</d:State><d:TemplateId m:null="true" /><d:JobNotificationSubscriptions m:type="Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.JobNotificationSubscription)"><d:element><d:TargetJobState m:type="Edm.Int32">2</d:TargetJobState><d:NotificationEndPointId>nb:nepid:UUID:36e510df-8560-4bae-a698-87723f677e98</d:NotificationEndPointId></d:element></d:JobNotificationSubscriptions></m:properties></content></entry>  
--changesetresponse_10441dcf-ec34-4b8a-919e-2368b2c6444e  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
HTTP/1.1 201 Created  
DataServiceVersion: 3.0;  
Content-Type: application/atom+xml;type=entry;charset=utf-8  
Content-ID: 2  
X-Content-Type-Options: nosniff  
Cache-Control: no-cache  
Location: https://media.windows.net/api/Tasks('nb%3Atid%3AUUID%3A94d3c509-24c2-467f-aa65-d16a4ea28b19')  
  
<?xml version="1.0" encoding="utf-8"?><entry xml:base="https://media.windows.net/api/" xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns:georss="http://www.georss.org/georss" xmlns:gml="http://www.opengis.net/gml"><id>https://media.windows.net/api/Tasks('nb%3Atid%3AUUID%3A94d3c509-24c2-467f-aa65-d16a4ea28b19')</id><category term="Microsoft.Cloud.Media.Vod.Rest.Data.Models.Task" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" /><link rel="edit" title="Task" href="Tasks('nb%3Atid%3AUUID%3A94d3c509-24c2-467f-aa65-d16a4ea28b19')" /><link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/OutputMediaAssets" type="application/atom+xml;type=feed" title="OutputMediaAssets" href="Tasks('nb%3Atid%3AUUID%3A94d3c509-24c2-467f-aa65-d16a4ea28b19')/OutputMediaAssets" /><link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/InputMediaAssets" type="application/atom+xml;type=feed" title="InputMediaAssets" href="Tasks('nb%3Atid%3AUUID%3A94d3c509-24c2-467f-aa65-d16a4ea28b19')/InputMediaAssets" /><title /><updated>2013-04-20T22:42:02Z</updated><author><name /></author><content type="application/xml"><m:properties><d:Id>nb:tid:UUID:94d3c509-24c2-467f-aa65-d16a4ea28b19</d:Id><d:Configuration>H264 Smooth Streaming 720p</d:Configuration><d:EndTime m:null="true" /><d:ErrorDetails m:type="Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.ErrorDetail)" /><d:HistoricalEvents m:type="Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.TaskHistoricalEvent)" /><d:MediaProcessorId>nb:mpid:UUID:70bdc2c3-ebf4-42a9-8542-5afc1e55d217</d:MediaProcessorId><d:Name>My Mp4 to Smooth Task</d:Name><d:PerfMessage m:null="true" /><d:Priority m:type="Edm.Int32">0</d:Priority><d:Progress m:type="Edm.Double">0</d:Progress><d:RunningDuration m:type="Edm.Double">0</d:RunningDuration><d:StartTime m:null="true" /><d:State m:type="Edm.Int32">0</d:State><d:TaskBody><?xml version="1.0" encoding="utf-16"?>  
<taskBody>  
  <inputAsset>JobInputAsset(0)</inputAsset>  
  <outputAsset assetCreationOptions="0" assetName="Output asset">JobOutputAsset(0)</outputAsset>  
</taskBody></d:TaskBody><d:Options m:type="Edm.Int32">0</d:Options><d:EncryptionKeyId m:null="true" /><d:EncryptionScheme m:null="true" /><d:EncryptionVersion m:null="true" /><d:InitializationVector m:null="true" /></m:properties></content></entry>  
--changesetresponse_10441dcf-ec34-4b8a-919e-2368b2c6444e--  
--batchresponse_2ae0b2a5-ec8b-438b-ae62-a02bf2b4a502--  
  
```  
  
 The [Get Messages](http://msdn.microsoft.com/library/windowsazure/dd179474.aspx) operation for the queue with the endpoint address specified earlier generates the following notification messages:  
  
```  
{  
"MessageVersion":"1.0",  
"EventType":"NotificationEndPointRegistration",  
"ETag":"d7a67e6e19acdb35c3de63e5d5a655b0a06cefb18192b4a6d6dc551298a2c01f",  
"TimeStamp":"2013-04-22T19:33:32",  
"Properties":  
    {  
    "NotificationEndPointId":"nb:nepid:UUID:36e510df-8560-4bae-a698-87723f677e98",  
    "State":"Registered",  
    "Name":"c9251969-d74e-40b3-927f-62de9c0cc3d1",  
    "Created":"2013-04-22T19:33:31"  
    }  
}  
  
{  
"MessageVersion":"1.0",  
"EventType":"JobStateChange",  
"ETag":"4bc48c4bf9ae7f50e4dfdc5cda32a032e30c9ba94f9cd45d859c64e28e7e9937",  
"TimeStamp":"2013-04-22T19:34:12",  
"Properties":  
    {  
    "JobId":"nb:jid:UUID:3A7dc2642f-ab1e-9f4c-8ecd-027eeac2a4ab",  
    "JobName":"My MP4 to Smooth Streaming encoding job",  
    "NewState":"Scheduled",  
    "OldState":"Queued",  
    "AccountName":"account001"  
    }  
}  
  
{  
"MessageVersion":"1.0",  
"EventType":"JobStateChange",  
"ETag":"4f5ca985235ed262df7b995a278de24fea4bae1a630d5106dd215853a42cf2ca",  
"TimeStamp":"2013-04-22T19:34:13",  
"Properties":  
    {  
    "JobId":"nb:jid:UUID:3A7dc2642f-ab1e-9f4c-8ecd-027eeac2a4ab",  
    "JobName":"My MP4 to Smooth Streaming encoding job",  
    "NewState":"Processing",  
    "OldState":"Scheduled",  
    "AccountName":"account001"  
    }  
}  
  
{  
"MessageVersion":"1.0",  
"EventType":"JobStateChange",  
"ETag":"25af87b23c92a52d140fcf0915b3b1868f3bd9822347de9287688a9cff653623",  
"TimeStamp":"2013-04-22T19:35:28",  
"Properties":  
    {  
    "JobId":"nb:jid:UUID:3A7dc2642f-ab1e-9f4c-8ecd-027eeac2a4ab",  
    "JobName":"My MP4 to Smooth Streaming encoding job",  
    "NewState":"Finished",  
    "OldState":"Processing",  
    "AccountName":"account001"  
    }  
}  
```  
  
 Notification `EventType` could have the following values: None = 0, JobStateChange = 1, NotificationEndPointRegistration = 2, and NotificationEndPointUnregistration = 3.  
  
 The `JobStateChange` event could have the following job states: Queued = 0, Scheduled = 1, Processing = 2, Finished = 3, Error = 4, Canceled = 5, and Canceling = 6.  
  
##  <a name="list_jobs"></a> List Jobs  
 Jobs can be retrieved using a HTTP GET request.  
  
> [!IMPORTANT]
>  When making a request to list Job entities, a maximum of 1000 will be returned per request. If you need to keep track of all submitted Jobs, you can use top/skip as described in [OData system query options](http://msdn.microsoft.com/library/gg309461.aspx).  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/Jobs|HTTP/1.1|  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|https://media.windows.net/API/Jobs('*jobid*')|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
GET https://media.windows.net/API/Jobs('nb:jid:UUID:b1f956b3-774c-bb44-a3f7-ee47e23add31') HTTP/1.1  
Content-Type: application/json;odata=verbose  
Accept: application/json;odata=verbose  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
x-ms-version: 2.11  
Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d   
Host: media.windows.net  
  
```  
  
##  <a name="cancel_a_job"></a> Cancel a Job  
 Running Jobs can be canceled using the CancelJob function. For an example, see [REST API Functions](../MediaServicesREST/rest-api-functions.md).  
  
##  <a name="delete_job"></a> Delete a Job  
 Jobs can be deleted using a HTTP DELETE request. This is useful to clean old completed jobs from the An Azure Media Service account database.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|DELETE|https://media.windows.net/API/Jobs('*jobid*')|HTTP/1.1|  
  
## Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
```  
DELETE https://media.windows.net/api/Jobs('nb:jid:UUID:9f5b35d0-68ac-c249-8ece-ece9ea22a461') HTTP/1.1  
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
 [ContentKey](../MediaServicesREST/contentkey.md)   
 [Asset](../MediaServicesREST/asset.md)   
 [AccessPolicy](../MediaServicesREST/accesspolicy.md)   
 [AssetFile](../MediaServicesREST/assetfile.md)   
 [JobTemplate](../MediaServicesREST/jobtemplate.md)   
 [Locator](../MediaServicesREST/locator.md)   
 [MediaProcessor](../MediaServicesREST/mediaprocessor.md)   
 [Task](../MediaServicesREST/task.md)   
 [TaskTemplate](../MediaServicesREST/tasktemplate.md)   
 [Quotas and Limitations](http://msdn.microsoft.com/en-us/82f7e538-6bdf-4883-aa50-24574cc4996e)
---
title: "Program"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a22d0d8f-c485-44d0-97e0-d03a6762cdbc
caps.latest.revision: 12
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
# Program
A Program enables you to control the publishing and storage of segments in a live stream. Programs can run concurrently. This allows you to publish and archive different parts of the event as needed.  
  
 You can specify the number of hours you want to retain the recorded content for the program by setting the `ArchiveWindowLength` property (up to 25 hours). Clients can seek through the archived content for the specified number of hours. If the program runs longer than the specified ArchiveWindowLength, the older content is removed. For more information, see the `ArchiveWindowLength` documentation below.  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://msdn.microsoft.com/en-us/42ae6204-93bc-4797-bf40-1c68512cfb73).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
 This topic gives an overview of the `Program` entity and also demonstrates how to execute various operations with the Media Services REST API.  
  
-   [Create Programs](#create_programs)  
  
-   [Start Programs](#start_programs)  
  
-   [Stop Programs](#stop_programs)  
  
-   [List Programs](#list_programs)  
  
-   [Update Programs](#update_programs)  
  
-   [Delete Programs](#delete_programs)  
  
##  <a name="program_properties"></a> Program Entity Properties  
 The Program entity contains the following properties.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`Id`<br /><br /> Read-only. Set by Media Services.|Edm.String|The Program ID, assigned upon creation. The format is: nb:pgid:UUID:\<GUID>.|  
|`Name`|Edm.String|The name of the Program. The maximum length is 256 characters and can consist of any English characters and numbers, including '-' and ' ' as long as it starts and ends with alphanumeric characters.|  
|`AssetId`|Edm.String|The Asset ID to be used for Program processing. The property can only be updated when the Program is in the **Stopped** state.<br /><br /> An asset cannot be deleted if it is used by a program. You can delete an asset after deleting the program that uses it.|  
|`Created`<br /><br /> Read-only. Set by Media Services.|Edm.DateTime|A UTC date/time value that indicates the time of creation.|  
|`Description`|Edm.String|User provided description. The maximum length is 256 characters.|  
|`ArchiveWindowLength`<br /><br /> Required.|Edm.Time|The number of hours you want to retain the recorded content for the program. This value can be set from a minimum of 5 minutes to a maximum of 25 hours. This also dictates the maximum amount of time clients can seek back in time from the current live position. Programs can run over the specified amount of time, but content that falls behind the window length is continuously discarded. This value of this property also determines how long the client manifests can grow.<br /><br /> To delete archived content, stop and delete the program and then delete the asset associated with the program.|  
|`LastModified`<br /><br /> Read-only. Set by Media Services.|Edm.DateTime|The date and time of the last modification.|  
|`ManifestName`|Edm.String|The manifest file name, without extension. This property can be updated only when the Program is in the **Stopped** state.|  
|`State`<br /><br /> Read-only. Set by Media Services.|Edm.String|Gets the current state. Possible values include:<br /><br /> -   Stopped. After creating a Program, it is in the **Stopped** state. In this state, the Program properties can be updated, but streaming is not allowed. The Program can be started, updated, or deleted from this state.<br />-   Starting. Program is being started. No updates or streaming is allowed during this state.<br />-   Running. Program is capable of processing and archiving live streams.<br />-   Stopping. Program is being stopped. No updates or streaming is allowed during this state.|  
|`ChannelId`<br /><br /> Read-only. Set by Media Services.|Edm.String|The ID of the Program's parent Channel.|  
|`Channel`|[Channel](../MediaServicesREST/channel.md)|The Program's parent channel specified by the **ChannelId**.|  
  
##  <a name="create_programs"></a> Create Programs  
 Create a new Program.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/api/Programs|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
POST https://testrest.cloudapp.net/api/Programs HTTP/1.1  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json;odata=minimalmetadata  
Accept-Charset: UTF-8  
x-ms-version: 2.11  
Content-Type: application/json;odata=minimalmetadata  
Host: <redirected host URI>  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
  
```  
  
 Request body:  
  
```  
{"Id":null,"Name":"testprogram001","Description":"","Created":"0001-01-01T00:00:00","LastModified":"0001-01-01T00:00:00","ChannelId":"nb:chid:UUID:83bb19de-7abf-4907-9578-abe90adfbabe","AssetId":"nb:cid:UUID:bc495364-5357-42a1-9a9d-be54689cfae2","ArchiveWindowLength":"PT1H","State":null,"ManifestName":null}  
```  
  
 If successful, a **202 Accepted** status code is returned along with a representation of the created entity in the response body.  
  
```  
{"odata.metadata":"https://testrest.cloudapp.net/api/$metadata#Programs/@Element","Id":"nb:pgid:UUID:b870dd57-4b04-41b6-849d-b2470e50e7e6","Name":"testprogram001","Description":"","Created":"2014-08-11T18:12:27.8381256Z","LastModified":"2014-08-11T18:12:27.8381256Z","ChannelId":"nb:chid:UUID:83bb19de-7abf-4907-9578-abe90adfbabe","AssetId":"nb:cid:UUID:bc495364-5357-42a1-9a9d-be54689cfae2","ArchiveWindowLength":"PT1H","State":"Stopped","ManifestName":"f91329ec-26f5-4026-87f5-f5437d4da9e6"}  
  
```  
  
> [!NOTE]
>  This operation completes synchronously, so therefore, there is no operation-id to track.  
  
##  <a name="start_programs"></a> Start Programs  
 Start a Program. A Program can only be started when it is in the **Stopped** state and the channel is in the **Running** state.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|Start|https://media.windows.net/api/Programs(‘*ProgramId*’)/Start|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
POST https://testrest.cloudapp.net/api/Programs('nb:pgid:UUID:0f9ceb51-50fe-4769-aaed-f8c19d76b9bc')/Start HTTP/1.1  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json;odata=minimalmetadata  
Accept-Charset: UTF-8  
x-ms-version: 2.11  
Content-Type: application/json;odata=minimalmetadata  
Host: <redirected host URI>  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
  
```  
  
 If successful, a **202 Accepted** status code is returned. The **202 Accepted** status code indicates an asynchronous operation, in which case the operation-id header value is also provided for use in polling and tracking the status of long-running operations, such as starting or stopping a Program. Pass the operation-id header value into the Operation Entity to retrieve the status. For more information, see [Manually Polling Long-Running Operations](http://msdn.microsoft.com/en-us/3f8c9717-b557-47b8-bbef-18f867e98019).  
  
##  <a name="stop_programs"></a> Stop Programs  
 Stop a Program. A Program can be stopped only when it is in the **Running** state. This is an asynchronous operation.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|Stop|https://media.windows.net/api/Programs(‘*ProgramId*’)/Stop|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
POST https://testrest.cloudapp.net/api/Programs('nb:pgid:UUID:0f9ceb51-50fe-4769-aaed-f8c19d76b9bc')/Stop HTTP/1.1  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json;odata=minimalmetadata  
Accept-Charset: UTF-8  
x-ms-version: 2.11  
Content-Type: application/json;odata=minimalmetadata  
Host: <redirected host URI>  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
  
```  
  
 If successful, a **202 Accepted** status code is returned. The **202 Accepted** status code indicates an asynchronous operation, in which case the operation-id header value is also provided for use in polling and tracking the status of long-running operations, such as starting or stopping a Program. Pass the operation-id header value into the Operation Entity to retrieve the status. For more information, see [Manually Polling Long-Running Operations](http://msdn.microsoft.com/en-us/3f8c9717-b557-47b8-bbef-18f867e98019).  
  
##  <a name="list_programs"></a> List Programs  
 Programs are retrieved using a GET HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|Get all Programs in the Media Services account:<br /><br /> https://media.windows.net/api/Programs<br /><br /> Get a specified Program in the Media Services account:<br /><br /> https://media.windows.net/api/Programs(‘*ProgramId*’)<br /><br /> Get all Programs associated with a specified Channel:<br /><br /> https://media.windows.net/api/Channels('*channelid*')/Programs|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
GET https://testrest.cloudapp.net/api/Programs HTTP/1.1  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json;odata=minimalmetadata  
Accept-Charset: UTF-8  
x-ms-version: 2.11  
Content-Type: application/json;odata=minimalmetadata  
Host: <redirected host URI>  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
  
```  
  
 If successful, this operation returns a **200 OK** status code and a list of all of the Programs created in your Media Services account.  
  
##  <a name="update_programs"></a> Update Programs  
 Update a Program. The Program must be the **Stopped** state.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|PATCH/PUT/MERGE<br /><br /> For more information about these operations, see [PATCH/PUT/MERGE](http://msdn.microsoft.com/library/dd541276.aspx).|https://media.windows.net/api/Programs(‘*ProgramId*’)|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
PATCH https://testrest.cloudapp.net/api/Programs('nb:pgid:UUID:0f9ceb51-50fe-4769-aaed-f8c19d76b9bc') HTTP/1.1  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json;odata=minimalmetadata  
Accept-Charset: UTF-8  
x-ms-version: 2.11  
Content-Type: application/json;odata=minimalmetadata  
Host: <redirected host URI>  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
  
```  
  
 Request body:  
  
```  
{"ArchiveWindowLength":"PT3H"}  
```  
  
 If the update completes synchronously, it returns a **204 No Content** status code; otherwise it returns a **202 Accepted** status code. The **202 Accepted** status code indicates an asynchronous operation, in which case the operation-id header value is also provided for use in polling and tracking the status of long-running operations, such as starting or stopping a Program. Pass the operation-id header value into the Operation Entity to retrieve the status. For more information, see [Manually Polling Long-Running Operations](http://msdn.microsoft.com/en-us/3f8c9717-b557-47b8-bbef-18f867e98019).  
  
##  <a name="delete_programs"></a> Delete Programs  
 Delete a Program. A Program can be deleted only when it is in the **Stopped** state.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|DELETE|https://media.windows.net/api/Programs(‘*ProgramId*’)|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
DELETE https://testrest.cloudapp.net/api/Programs('nb:pgid:UUID:0f9ceb51-50fe-4769-aaed-f8c19d76b9bc') HTTP/1.1  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json;odata=minimalmetadata  
Accept-Charset: UTF-8  
x-ms-version: 2.11  
Content-Type: application/json;odata=minimalmetadata  
Host: <redirected host URI>  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
  
```  
  
 If successful, a **204 No Content** status code is returned.  
  
> [!NOTE]
>  This operation completes synchronously, so therefore, there is no operation-id to track.  
  
## See Also  
 [Channel](../MediaServicesREST/channel.md)
---
title: "Playback"
ms.custom: na
ms.date: 2016-07-13
ms.prod: azure
ms.reviewer: na
ms.service: media-services
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f1edd9eb-c4ea-4e09-8772-43a430fa7106
caps.latest.revision: 5
author: juliako
manager: dwrede
translation.priority.mt: 
  - de-de
  - es-es
  - fr-fr
  - it-it
  - ja-jp
  - ko-kr
  - pt-br
  - ru-ru
  - zh-cn
  - zh-tw
---
# Playback
The Playback action is used to retrieve the playback URL of a Video. This PlaybackEndpoint will only be available after the video is ready for playback and all processing is completed in the backend.  
  
## Get playback URL  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|/api/Videos/{id}/PlaybackEndpoint?endpointType= {‘`endpoint type’`}|HTTP/1.1|  
  
 Endpoint type can be one of the following:  
  
|EndpointType value|Playback format|  
|------------------------|---------------------|  
|Streaming|Microsoft Smooth Streaming|  
|HLS|Apple HTTP Live Streaming (HLS) format|  
|DASH|Dynamic Adaptive Streaming over HTTP (DASH), also known as MPEG-DASH|  
  
### Sample request/response  
 Request headers  
  
```  
GET https://testazuremediaservicesconnector.azurewebsites.net/api/Videos/9457d368-3a6b-4e8a-a64e-a1ec5e3e357b/PlaybackEndpoint?endpointType=Streaming HTTP/1.1  
```  
  
 Body  
  
```  
None  
```  
  
 If successful, a 200 OK status code is returned along with a representation of the created entity in the response body.  
  
```  
HTTP/1.1 200 OK   
Cache-Control: no-cache   
Pragma: no-cache   
Content-Length: 183   
Content-Type: application/json; charset=utf-8   
Expires: -1   
Server: Microsoft-IIS/8.0   
Set-Cookie: ARRAffinity=4ffc8e980cb737c94f36786019b7991cf401d053cc900e4e68629f786f0d288b;Path=/;Domain=ctest2gateway.azurewebsites.net   
X-AspNet-Version: 4.0.30319   
X-Powered-By: ASP.NET   
x-ms-proxy-outgoing-newurl: https://testazuremediaservicesconnector.azurewebsites.net/api/Videos/9457d368-3a6b-4e8a-a64e-a1ec5e3e357b/PlaybackEndpoint?endpointType=Streaming   
X-Powered-By: ASP.NET   
Set-Cookie: ARRAffinity=4ffc8e980cb737c94f36786019b7991cf401d053cc900e4e68629f786f0d288b;Path=/;Domain=ctest2gateway.azurewebsites.net   
Date: Mon, 23 Mar 2015 19:52:42 GMT   
{   
"Type":"Streaming",   
"PlaybackUrl":"http://cdn-cvprbl203m01.streaming.mediaservices.windows.net/b8400467-959d-4707-b418-2906b2574460/9dcf086e-8866-44fd-83fa-6888913e9986.ism/Manifest"   
}  
```  
  
 If the VideoID is invalid, you will get a 404 Not Found status.  
  
 If the video is still processing you will get 403 – Forbidden status.
---
title: "Thumbnail"
ms.custom: na
ms.date: 2016-07-13
ms.prod: azure
ms.reviewer: na
ms.service: media-services
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5d5155b0-fc39-4e03-ba2d-27be7f7d3392
caps.latest.revision: 4
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
# Thumbnail
The Thumbnail entity represents a thumbnail image derived from a video.  
  
## Thumbnail properties  
  
|Property|Type|Description|Required?|  
|--------------|----------|-----------------|---------------|  
|Height|int|Height of thumbnail in pixels.|No|  
|ID|string|Primary id of the entity.|No|  
|Index|int|For indexed thumbnails, the index of this thumbnail; otherwise 0.|No|  
|Time|int|For time-based thumbnails, the time offset in seconds; otherwise 0.|No|  
|Url|string|The URL of the thumbnail. The URL returned here is valid for a limited period of time.|No|  
|VideoId|string|The key of the Video from which this Thumbnail is derived.|No|  
  
## Get a thumbnail  
 Clients use this to check if the content is ready for streaming  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|/api/Videos/{id}/Thumbnails|HTTP/1.1|  
  
### Sample request/response  
 Request headers  
  
```  
GET https://testazuremediaservicesconnector.azurewebsites.net/api/Videos/4f13e32f-7eab-4c24-948a-f817647dbe2b/Thumbnails HTTP/1.1   
Content-Type: application/json  
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
Content-Length: 520   
Content-Type: application/json; charset=utf-8   
Expires: -1   
Server: Microsoft-IIS/8.0   
Set-Cookie: ARRAffinity=4ffc8e980cb737c94f36786019b7991cf401d053cc900e4e68629f786f0d288b;Path=/;Domain=ctest2gateway.azurewebsites.net   
X-AspNet-Version: 4.0.30319   
X-Powered-By: ASP.NET   
x-ms-proxy-outgoing-newurl: https://testazuremediaservicesconnector.azurewebsites.net/api/Videos/9457d368-3a6b-4e8a-a64e-a1ec5e3e357b/Thumbnails   
X-Powered-By: ASP.NET   
Set-Cookie: ARRAffinity=4ffc8e980cb737c94f36786019b7991cf401d053cc900e4e68629f786f0d288b;Path=/;Domain=ctest2gateway.azurewebsites.net   
Date: Mon, 23 Mar 2015 19:57:19 GMT    
[   
{   
"Kind":"Poster",   
"Height":"960",   
"Index":"0",   
"Time":"0",    
"Url":"https://cvprbl203v.cloudvideo.azure.net:443/api/ImageProxy?mediaservicesurl=https%3a%2f%2fcvprbl203m01r14.blob.core.windows.net%2fasset-e41e435d-1500-80c3-01a7-f1e4d195f969%2fPoster.jpg%3fsv%3d2012-02-12%26sr%3dc%26si%3d37390e8f-c4d2-4125-8233-df100fa99b84%26sig%3dpjVZnvGMDECtg3bc1ekKaMtASELYjtaKeilXhwODIoM%253D%26st%3d2015-03-23T19%253A47%253A30Z%26se%3d2015-04-06T19%253A47%253A30Z&imagemetadata=nb%3acid%3aUUID%3ae41e435d-1500-80c3-01a7-f1e4d195f969"   
}   
]  
```  
  
 If a wrong video id is specified, you will get a 404 – Not Found.
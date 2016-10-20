---
title: "Formats"
ms.custom: na
ms.date: 2016-07-13
ms.prod: azure
ms.reviewer: na
ms.service: media-services
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b25075b2-bdfd-4795-ae63-2f911c109c99
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
# Formats
The Formats endpoint is used to retrieve a list of supported input video formats.  
  
## Formats properties  
  
|Property|Type|Description|Required?|  
|--------------|----------|-----------------|---------------|  
|Extension|string|File extension of format|No|  
|MimeType|string|The MIME type for this format|No|  
  
## Get formats  
 Clients use this to check if the content is ready for streaming  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|/api/Formats|HTTP/1.1|  
  
### Sample request/response  
 Request headers  
  
```  
GET https://testazuremediaservicesconnector.azurewebsites.net/api/Formats HTTP/1.1  
```  
  
 Request body  
  
```  
None  
```  
  
 If successful, a 200 OK status code is returned along with a representation of the created entity in the response body.  
  
```  
 HTTP/1.1 200 OK   
Cache-Control: no-cache   
Pragma: no-cache   
Content-Length: 1746   
Content-Type: application/json; charset=utf-8   
Expires: -1   
Server: Microsoft-IIS/8.0   
Set-Cookie: ARRAffinity=4ffc8e980cb737c94f36786019b7991cf401d053cc900e4e68629f786f0d288b;Path=/;Domain=ctest2gateway.azurewebsites.net   
X-AspNet-Version: 4.0.30319   
X-Powered-By: ASP.NET   
x-ms-proxy-outgoing-newurl: https://azuremediaservicesconnectorc0691ddba6f2424ea4aa3e4644091464.azurewebsites.net/api/Formats   
X-Powered-By: ASP.NET   
Set-Cookie: ARRAffinity=4ffc8e980cb737c94f36786019b7991cf401d053cc900e4e68629f786f0d288b;Path=/;Domain=ctest2gateway.azurewebsites.net   
Date: Mon, 23 Mar 2015 20:07:35 GMT   
[{"Extension":"aif","MimeType":"audio/x-aiff"},{"Extension":"aifc","MimeType":"audio/x-aiff"},{"Extension":"aiff","MimeType":"audio/x-aiff"},{"Extension":"au","MimeType":"audio/basic"},{"Extension":"avi","MimeType":"video/x-msvideo"},{"Extension":"dif","MimeType":"video/x-dv"},{"Extension":"dv","MimeType":"video/x-dv"},{"Extension":"m3u","MimeType":"audio/x-mpegurl"},{"Extension":"m4a","MimeType":"audio/mp4a-latm"},{"Extension":"m4b","MimeType":"audio/mp4a-latm"},{"Extension":"m4p","MimeType":"audio/mp4a-latm"},{"Extension":"m4u","MimeType":"video/vnd.mpegurl"},{"Extension":"m4v","MimeType":"video/x-m4v"},{"Extension":"mid","MimeType":"audio/midi"},{"Extension":"midi","MimeType":"audio/midi"},{"Extension":"mov","MimeType":"video/quicktime"},{"Extension":"movie","MimeType":"video/x-sgi-movie"},{"Extension":"mp2","MimeType":"audio/mpeg"},{"Extension":"mp3","MimeType":"audio/mpeg"},{"Extension":"mp4","MimeType":"audio/mp4"},{"Extension":"mpe","MimeType":"audio/mpeg"},{"Extension":"mpeg","MimeType":"audio/mpeg"},{"Extension":"mpg","MimeType":"audio/mpeg"},{"Extension":"mpga","MimeType":"audio/mpeg"},{"Extension":"mxu","MimeType":"video/vnd.mpegurl"},{"Extension":"qt","MimeType":"video/quicktime"},{"Extension":"ra","MimeType":"audio/x-pn-realaudio"},{"Extension":"ram","MimeType":"audio/x-pn-realaudio"},{"Extension":"wav","MimeType":"audio/x-wav"},{"Extension":"asf","MimeType":"video/x-ms-asf"},{"Extension":"asx","MimeType":"video/x-ms-asf"},{"Extension":"wma","MimeType":"audio/x-ms-wma"},{"Extension":"wax","MimeType":"audio/x-ms-wax"},{"Extension":"wmv","MimeType":"audio/x-ms-wmv"},{"Extension":"wvx","MimeType":"video/x-ms-wvx"},{"Extension":"wm","MimeType":"video/x-ms-wm"},{"Extension":"wmx","MimeType":"video/x-ms-wmx"}]  
```
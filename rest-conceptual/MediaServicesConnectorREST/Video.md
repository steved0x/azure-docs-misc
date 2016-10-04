---
title: "Video"
ms.custom: na
ms.date: 2016-07-13
ms.prod: azure
ms.reviewer: na
ms.service: media-services
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78fb6d4b-9042-4865-b910-219f6210fd8a
caps.latest.revision: 6
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
# Video
A Video is the primary entity in the Media Services Connector API. It represents a video on which the following operations can be performed:  
  
 [Create a video](#create)  
  
 [Retrieve a video](#retrieve)  
  
 [Mark complete](#markcomplete)  
  
 [Get authorization token](#authtoken)  
  
## Video properties  
  
|Property|Type|Description|Required?|  
|--------------|----------|-----------------|---------------|  
|ContentProtectionKeyId|string|If ContentProtectionMode=”AES128”, this property contains the ID of the key used to secure the video.|No|  
|ContentProtectionMode|string|Controls the protection mode used when streaming the video for playback. Expected values: “None” or “AES128”|No|  
|Duration|int|Duration of video in seconds, if available.|No|  
|ID|string|Primary key of entity|No|  
|InputStorageEncryptionMode|string|Encryption mode for input video. Expected values: empty or “AES256”.|No|  
|InputStorageEncryptionSymmetricKey|string|The symmetric key to be used by the client to encrypt video content before uploading, base 64 encoded. This value is present only on a Video entity returned by a POST operation|No|  
|InputStorageEncryptionIv|string|The initialization vector to be used by the client to encrypt video content before uploading, base 64 encoded. This value is present only on a Video entity returned by a POST operation.|No|  
|OriginalFileName|string|The name of the video file which you are uploading. Once the file is uploaded, you will receive a response back with the new name in the following format: `<guid>.<file-extension>`.|Yes|  
|UploadUri|string|This is the URI where video content should be uploaded to an Azure Storage location (managed by Media Services). Once you have uploaded a video and notified Media Services (by calling MarkComplete described below), it is no longer modifiable and this URL is empty.|No|  
|||||  
  
##  <a name="create"></a> Create a video  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|/api/Videos|HTTP/1.1|  
  
### Sample request/response  
 Request headers  
  
```  
POST https://testazuremediaservicesconnector.azurewebsites.net/api/Videos/ HTTP/1.1   
Content-Type: application/json  
```  
  
 Request body  
  
```  
{“OriginalFileName”:”yourfilename.mp4”}  
```  
  
 If successful, a 200 OK status code is returned along with a representation of the created entity in the response body.  
  
```  
HTTP/1.1 200 OK   
Cache-Control: no-cache   
Pragma: no-cache   
Content-Length: 611   
Content-Type: application/json; charset=utf-8   
Expires: -1   
Server: Microsoft-IIS/8.0   
Set-Cookie: ARRAffinity=4ffc8e980cb737c94f36786019b7991cf401d053cc900e4e68629f786f0d288b;Path=/;Domain=ctest2gateway.azurewebsites.net   
X-AspNet-Version: 4.0.30319   
X-Powered-By: ASP.NET   
x-ms-proxy-outgoing-newurl: https://testazuremediaservicesconnector.azurewebsites.net/api/Videos   
X-Powered-By: ASP.NET   
Set-Cookie: ARRAffinity=4ffc8e980cb737c94f36786019b7991cf401d053cc900e4e68629f786f0d288b;Path=/;Domain=ctest2gateway.azurewebsites.net   
Date: Mon, 23 Mar 2015 19:35:07 GMT   
{   
"Id":"ee0dfd10-4a38-469f-98dc-2c8e34de0be8",   
"UploadUri":"https://cvprbl203m01r12.blob.core.windows.net:443/asset-0914435d-1500-80c3-9b0e-f1e4d193b00f/a6dad4be-6a34-423d-85de-b43491133140.mp4?sv=2012-02-12&sr=c&si=5e9ce4f6-9075-40d1-929a-831ebdc1edd9&sig=61s0EbC%2FWsz9zaJYh%2FOnsj3%2FG7Mbzo%2FuBDARATEKQcs%3D&st=2015-03-23T19%3A30%3A07Z&se=2015-03-24T08%3A00%3A07Z",   
"ContentProtectionMode":"None",   
"ContentProtectionKeyId":null,   
"Duration":0,   
"OriginalFileName":"a6dad4be-6a34-423d-85de-b43491133140.mp4",   
"InputStorageEncryptionMode":null,   
"InputStorageEncryptionSymmetricKey":null,   
"InputStorageEncryptionIv":null   
}  
  
```  
  
 If you don’t provide an OriginalFileName, you will get a 400 – Unable to deserialize JSON into Video object  
  
```  
HTTP/1.1 400 Unable to deserialize JSON into Video object...   
HTTP/1.1 400 Unable to deserialize JSON into Video object. You must minimally specify OriginalFileName field. FileName doesn't matter but you must provide CORRECT extension.   
Cache-Control: no-cache   
Pragma: no-cache   
Content-Length: 478   
Content-Type: text/html; charset=Windows-1252   
Expires: -1   
Server: Microsoft-IIS/8.0   
Set-Cookie: ARRAffinity=4ffc8e980cb737c94f36786019b7991cf401d053cc900e4e68629f786f0d288b;Path=/;Domain=ctest2gateway.azurewebsites.net   
X-AspNet-Version: 4.0.30319   
X-Powered-By: ASP.NET   
x-ms-proxy-outgoing-newurl: https://testazuremediaservicesconnector.azurewebsites.net/api/Videos   
X-Powered-By: ASP.NET   
Set-Cookie: ARRAffinity=4ffc8e980cb737c94f36786019b7991cf401d053cc900e4e68629f786f0d288b;Path=/;Domain=ctest2gateway.azurewebsites.net   
Date: Mon, 23 Mar 2015 19:40:05 GMT   
<h1>Error</h1> <table> <tbody> <tr> <td><strong>Request</strong> </td> <td>https://azuremediaservicesconnectorc0691ddba6f2424ea4aa3e4644091464.azurewebsites.net/api/Videos</td> </tr> <tr> <td><strong>Error</strong></td> <td>BadRequest</td> </tr> <tr> <td><strong>Message</strong></td> <td>Unable to deserialize JSON into Video object. You must minimally specify OriginalFileName field. FileName doesn't matter but you must provide CORRECT extension.</td> </tr> </tbody> </table>  
```  
  
 If ContentProtectionMode is anything other than ‘AES128’ or ‘empty’ or if InputStorageEncryptionMode is anything other than AES256 or ‘empty’, you will get a 400 Bad Request  
  
```  
HTTP/1.1 400 Bad Request   
Cache-Control: no-cache   
Pragma: no-cache   
Content-Length: 173   
Content-Type: application/json; charset=utf-8   
Server: Microsoft-IIS/8.0  
Set-Cookie: ARRAffinity=4ffc8e980cb737c94f36786019b7991cf401d053cc900e4e68629f786f0d288b;Path=/;Domain=ctest2gateway.azurewebsites.net   
X-AspNet-Version: 4.0.30319   
X-Powered-By: ASP.NET   
x-ms-proxy-outgoing-newurl: https://testazuremediaservicesconnector.azurewebsites.net/api/Videos   
X-Powered-By: ASP.NET   
Set-Cookie: ARRAffinity=4ffc8e980cb737c94f36786019b7991cf401d053cc900e4e68629f786f0d288b;Path=/;Domain=ctest2gateway.azurewebsites.net   
Date: Mon, 23 Mar 2015 19:42:14 GMT   
{   
"status": 0,   
"source": "https://testazuremediaservicesconnector.azurewebsites.net/api/Videos",   
"message": "The request is invalid."   
}  
```  
  
##  <a name="retrieve"></a> Retrieve a video  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|/api/Videos/{id}|HTTP/1.1|  
  
### Sample request/response  
 Request headers  
  
```  
GET https://testazuremediaservicesconnector.azurewebsites.net/api/Videos/fc68482e-c4e2-49cf-b39f- 56264a4e2ddf HTTP/1.1  
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
Content-Length: 307   
Content-Type: application/json; charset=utf-8   
Expires: -1   
Server: Microsoft-IIS/8.0   
Set-Cookie: ARRAffinity=4ffc8e980cb737c94f36786019b7991cf401d053cc900e4e68629f786f0d288b;Path=/;Domain=ctest2gateway.azurewebsites.net   
X-AspNet-Version: 4.0.30319   
X-Powered-By: ASP.NET   
x-ms-proxy-outgoing-newurl: https:// testazuremediaservicesconnector.azurewebsites.net/api/Videos/fc68482e-c4e2-49cf-b39f-56264a4e2ddf   
X-Powered-By: ASP.NET   
Set-Cookie: ARRAffinity=4ffc8e980cb737c94f36786019b7991cf401d053cc900e4e68629f786f0d288b;Path=/;Domain=ctest2gateway.azurewebsites.net   
Date: Mon, 23 Mar 2015 19:31:39 GMT   
{"Id":"fc68482e-c4e2-49cf-b39f-56264a4e2ddf","UploadUri":null,"ContentProtectionMode":"None","ContentProtectionKeyId":null,"Duration":13,"OriginalFileName":"1141fb2a-af46-43c9-aa13-f0b49c7c13ae.mp4","InputStorageEncryptionMode":null,"InputStorageEncryptionSymmetricKey":null,"InputStorageEncryptionIv":null} HTTP/1.1 200 OK   
Cache-Control: no-cache   
Pragma: no-cache   
Content-Length: 307   
Content-Type: application/json; charset=utf-8   
Expires: -1   
Server: Microsoft-IIS/8.0   
Set-Cookie:   
ARRAffinity=4ffc8e980cb737c94f36786019b7991cf401d053cc900e4e68629f786f0d288b;Path=/;Domain=ctest2gateway.azurewebsites.net   
X-AspNet-Version: 4.0.30319   
X-Powered-By: ASP.NET   
x-ms-proxy-outgoing-newurl: https:// testazuremediaservicesconnector.azurewebsites.net/api/Videos/fc68482e-c4e2-49cf-b39f-56264a4e2ddf   
X-Powered-By: ASP.NET   
Set-Cookie:   
ARRAffinity=4ffc8e980cb737c94f36786019b7991cf401d053cc900e4e68629f786f0d288b;Path=/;Domain=ctest2gateway.azurewebsites.net   
Date: Mon, 23 Mar 2015 19:31:39 GMT   
  
{"Id":"fc68482e-c4e2-49cf-b39f- 56264a4e2ddf","UploadUri":null,"ContentProtectionMode":"None","ContentProtectionKeyId":null,"Duration": 13,"OriginalFileName":"1141fb2a-af46-43c9-aa13- f0b49c7c13ae.mp4","InputStorageEncryptionMode":null,"InputStorageEncryptionSymmetricKey":null,"InputSto rageEncryptionIv":null}  
```  
  
 If the video ID is incorrect, then you get 404 – Not Found  
  
```  
HTTP/1.1 404 Not Found  
```  
  
##  <a name="delete"></a> Delete a video  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|DELETE|/api/Videos/{id}|HTTP/1.1|  
  
### Sample request/response  
 Request headers  
  
```  
DELETE https://testazuremediaservicesconnector.azurewebsites.net/api/Videos/4f13e32f-7eab-4c24-948a-f817647dbe2b HTTP/1.1  
```  
  
 Request body  
  
```  
None  
```  
  
 If the video is successfully deleted or if you do not upload the video after calling create video, you get a 204 – No Content  
  
```  
HTTP/1.1 204 No Content   
Cache-Control: no-cache   
Pragma: no-cache   
Content-Length: 0   
Expires: -1   
Vary: Content-Type   
Server: Microsoft-IIS/8.0   
Set-Cookie: ARRAffinity=4ffc8e980cb737c94f36786019b7991cf401d053cc900e4e68629f786f0d288b;Path=/;Domain=ctest2gateway.azurewebsites.net   
X-Content-Type-Options: nosniff   
x-ms-svc-ver: 0.0.1503.1901   
x-ms-request-elapsed-ms: 39   
client-request-id: ceeba89a-8d64-47fe-bbb2-9e0087139fdd   
request-id: 20bd48f5-88f4-41ee-8ef0-41dba8bd626f   
ocp-cloudvideo-instance-id: VideoManagementService_IN_1   
X-AspNet-Version: 4.0.30319   
X-Powered-By: ASP.NET   
X-Powered-By: ASP.NET   
x-ms-proxy-outgoing-newurl: https:// testazuremediaservicesconnector.azurewebsites.net/api/Videos/ee0dfd10-4a38-469f-98dc-2c8e34de0be8   
X-Powered-By: ASP.NET   
Set-Cookie: ARRAffinity=4ffc8e980cb737c94f36786019b7991cf401d053cc900e4e68629f786f0d288b;Path=/;Domain=ctest2gateway.azurewebsites.net   
Date: Mon, 23 Mar 2015 19:44:22 GMT   
If you specify a wrong video id, you will get a 404  
```  
  
 If you specify a wrong video id, you will get a 404 – Not Found  
  
```  
HTTP/1.1 404 Not Found   
Cache-Control: no-cache   
Pragma: no-cache   
Content-Length: 0   
Expires: -1   
Vary: Content-Type  
Server: Microsoft-IIS/8.0   
Set-Cookie: ARRAffinity=4ffc8e980cb737c94f36786019b7991cf401d053cc900e4e68629f786f0d288b;Path=/;Domain=ctest2gateway.azurewebsites.net   
X-Content-Type-Options: nosniff   
x-ms-svc-ver: 0.0.1503.1901   
x-ms-request-elapsed-ms: 27   
client-request-id: 4a77af4e-4a0c-45fb-8056-f3ba903acbf0   
request-id: bc9f67e4-dbc1-430a-aae5-f3dd2a7dcf63   
ocp-cloudvideo-instance-id: VideoManagementService_IN_0   
X-AspNet-Version: 4.0.30319   
X-Powered-By: ASP.NET   
X-Powered-By: ASP.NET   
x-ms-proxy-outgoing-newurl: https://testazuremediaservicesconnector.azurewebsites.net/api/Videos/ee0dfd10-4a38-469f-asddsa98dc-2c8e34de0be8   
X-Powered-By: ASP.NET   
Set-Cookie: ARRAffinity=4ffc8e980cb737c94f36786019b7991cf401d053cc900e4e68629f786f0d288b;Path=/;Domain=ctest2gateway.azurewebsites.net   
Date: Mon, 23 Mar 2015 19:45:37 GMT  
```  
  
##  <a name="markcomplete"></a> Mark complete  
 Clients signal that they have completed uploading to BLOB storage by calling the MarkComplete action on a video  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|/api/Videos/{id}/MarkComplete|HTTP/1.1|  
  
### Sample request/response  
 Request headers  
  
```  
POST https://testazuremediaservicesconnector.azurewebsites.net/api/Videos/ee0dfd10-4a38-469f-asddsa98dc-2c8e34de0be8/MarkComplete HTTP/1.1  
```  
  
 Request body  
  
```  
None  
```  
  
 If successful, a 200 OK status code is returned.  
  
```  
HTTP/1.1 200 OK   
Cache-Control: no-cache  
```  
  
 If you submit a wrong video id for Mark Complete, you will get a 404 – Not Found  
  
```  
HTTP/1.1 404 Not Found   
Cache-Control: no-cache  
```  
  
## Get authorization token  
 Clients can use AuthorizationToken to retrieve a key token if the content is protected with AES-128 key (AES128 content protection mode).  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|/api/Videos/{id}/AuthorizationToken|HTTP/1.1|  
  
### Sample request/response  
 Request headers  
  
```  
GET https://testazuremediaservicesconnector.azurewebsites.net/api/Videos/221c2fa3-6440-4a7a-b1e4-88a3c8878233/AuthorizationToken?KeyId=f6eb7a33-e745-4e0b-bebb-54abcb56ee5f HTTP/1.1   
Content-Type: application/json  
```  
  
 Query string parameter  
  
```  
KeyId=<”ContentProtectionKeyId”>  
```  
  
 If successful, a 200 OK status code is returned.  
  
```  
HTTP/1.1 200 OK   
Cache-Control: no-cache   
Pragma: no-cache   
Content-Length: 591   
Content-Type: application/json; charset=utf-8   
Expires: -1   
Server: Microsoft-IIS/8.0   
Set-Cookie: ARRAffinity=add8315422140763770796c2c64f39117104178581c607b765efa5f51854d152;Path=/;Domain=ctest2gateway.azurewebsites.net   
X-AspNet-Version: 4.0.30319   
X-Powered-By: ASP.NET   
x-ms-proxy-outgoing-newurl: https://azuremediaservicesconnectorc0691ddba6f2424ea4aa3e4644091464.azurewebsites.net/api/Videos/221c2fa3-6440-4a7a-b1e4-88a3c8878233/AuthorizationToken?KeyId=f6eb7a33-e745-4e0b-bebb-54abcb56ee5f   
X-Powered-By: ASP.NET   
Set-Cookie: ARRAffinity=add8315422140763770796c2c64f39117104178581c607b765efa5f51854d152;Path=/;Domain=ctest2gateway.azurewebsites.net   
Date: Mon, 23 Mar 2015 21:19:30 GMT   
{   
"value":"Bearer=urn%3amicrosoft%3aazure%3amediaservices%3acontentkeyidentifier=f6eb7a33-e745-4e0b-bebb-54abcb56ee5f&urn%3amicrosoft%3aazure%3amediaservices%3akeyacquisitionhostname=cvprbl203m01.keydelivery.mediaservices.windows.net&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fnimbuslkgglobacs.accesscontrol.windows.net&urn%3aServiceAccessible=service&Audience=urn%3aNimbus&ExpiresOn=1427145871&Issuer=https%3a%2f%2fnimbuslkgglobacs.accesscontrol.windows.net%2f&HMACSHA256=rjG0atj1iIavsPn%2b894DtHFpZM4dWXL2lULgB26QeEo%3d"  
```  
  
## Check status  
 Clients use this to check if the content is ready for streaming  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|/api/Videos/{id}/Status|HTTP/1.1|  
  
### Sample request/response  
 Request headers  
  
```  
GET https://testazuremediaservicesconnector.azurewebsites.net/api/Videos/221c2fa3-6440-4a7a-b1e4-88a3c8878233/Status HTTP/1.1   
Content-Type: application/json  
```  
  
 If the video is still being processed, clients will get a 200 OK status code.  
  
```  
HTTP/1.1 200 OK   
Cache-Control: no-cache   
Pragma: no-cache   
Content-Length: 99   
Content-Type: application/json; charset=utf-8   
Expires: -1   
Server: Microsoft-IIS/8.0   
Set-Cookie: ARRAffinity=add8315422140763770796c2c64f39117104178581c607b765efa5f51854d152;Path=/;Domain=ctest2gateway.azurewebsites.net   
X-AspNet-Version: 4.0.30319   
X-Powered-By: ASP.NET   
x-ms-proxy-outgoing-newurl: https://testazuremediaservicesconnector.azurewebsites.net/api/Videos/221c2fa3-6440-4a7a-b1e4-88a3c8878233/Status   
X-Powered-By: ASP.NET   
Set-Cookie: ARRAffinity=add8315422140763770796c2c64f39117104178581c607b765efa5f51854d152;Path=/;Domain=ctest2gateway.azurewebsites.net   
Date: Mon, 23 Mar 2015 21:13:23 GMT   
{   
"StatusCode":1,   
"Status":"Processing",   
"Message":"Video is still being processed. Try again later."   
}  
```  
  
 If the video is successfully encoded, clients will get a 200 OK status code with the following status message in the body:  
  
```  
HTTP/1.1 200 OK   
Cache-Control: no-cache   
Pragma: no-cache   
Content-Length: 65   
Content-Type: application/json; charset=utf-8   
Expires: -1   
Server: Microsoft-IIS/8.0   
Set-Cookie: ARRAffinity=add8315422140763770796c2c64f39117104178581c607b765efa5f51854d152;Path=/;Domain=ctest2gateway.azurewebsites.net   
X-AspNet-Version: 4.0.30319   
X-Powered-By: ASP.NET   
x-ms-proxy-outgoing-newurl: https://testazuremediaservicesconnector.azurewebsites.net/api/Videos/221c2fa3-6440-4a7a-b1e4-88a3c8878233/Status   
X-Powered-By: ASP.NET   
Set-Cookie: ARRAffinity=add8315422140763770796c2c64f39117104178581c607b765efa5f51854d152;Path=/;Domain=ctest2gateway.azurewebsites.net   
Date: Mon, 23 Mar 2015 21:17:30 GMT   
{   
"StatusCode":2,   
"Status":"Completed",   
"Message":"Video is ready."   
}  
```  
  
##  <a name="upload_encrypted"></a> Upload encrypted content  
 Media Services enables you to upload encrypted videos. To upload an encrypted video, set the `InputStorageEncryptionMode` property of the Video to `AES256`.  
  
 During the [creation of the video](#create), Media Services Connector assigns a symmetric key and initialization vector (IV) to be used by the client.  
  
 The client is then responsible for encrypting the content using the AES-256 algorithm. Use cipher mode CTR and no padding. C# clients can use the `AesCryptoServiceProvider` class to perform the encryption.  
  
## See Also  
 [Upload a video to Azure blob](https://code.msdn.microsoft.com/Windows-Azure-Storage-CORS-45e5ce76)   
 [Getting Started with Azure Media Services Connector](https://azure.microsoft.com/blog/2015/03/25/getting-started-with-azure-media-services-connector/)
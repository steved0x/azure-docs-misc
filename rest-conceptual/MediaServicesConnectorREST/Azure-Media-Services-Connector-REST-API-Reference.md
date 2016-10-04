---
title: "Azure Media Services Connector REST API Reference"
ms.custom: na
ms.date: 2016-07-13
ms.prod: azure
ms.reviewer: na
ms.service: media-services
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cee3442a-652c-4046-9413-a24e5c228398
caps.latest.revision: 6
author: juliako
manager: erikre
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
# Azure Media Services Connector REST API Reference
Azure Media Services Connector enables users to easily host, manage, discover, and playback videos.  
  
 Azure Media Services Connector exposes the following resources via the REST API: Each resource may support GET, PUT, POST, or delete methods, based on the scenarios supported. For more details see the following topics:  
  
 [Video](../MediaServicesConnectorREST/Video.md) –represents the set of videos available within a given account  
  
 [Thumbnail](../MediaServicesConnectorREST/Thumbnail.md) –represents an image derived from a frame within a Video.  
  
 [Formats](../MediaServicesConnectorREST/Formats.md) –used to retrieve a list of supported input video formats.  
  
 [Playback](../MediaServicesConnectorREST/Playback.md) – used to retrieve the playback URL of the video.  
  
## Common scenarios  
  
### Upload and playback clear (unencrypted) content  
 Create Video.  
  
 Upload Video to Azure BLOB.  
  
 Indicate Completion of Upload.  
  
 Wait for Encoding Completion.  
  
 Get Playback URL for the desired playback format.  
  
 Get Thumbnail URL for the image to be displayed.  
  
 Configure [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) or your own player to playback media.  
  
### Upload and playback encrypted content  
 Create Video with encryption option selected.  
  
 Upload Video to Azure BLOB.  
  
 Indicate Completion of Upload.  
  
 Wait for Encoding Completion.  
  
 Get Authorization Token to playback encrypted content.  
  
 Get Playback URL for the desired playback format.  
  
 Get Thumbnail URL for the image to be displayed.  
  
 Configure [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) or your own player to playback media.  
  
## Headers supported by these APIs  
  
### Accept request header  
 The Accept request header controls the format of response data produced by Media Services. Clients may specify formats as shown. Media Services Connector defaults to ‘application/json’ responses if not specified.  
  
```  
application/json  
```  
  
### Content-Type request/response header  
 The Content-Type header specifies the media type of request or response content.  
  
```  
application/json  
```  
  
## HTTP status codes  
  
|Status|Condition|Method|Transient|  
|------------|---------------|------------|---------------|  
|200|OK|GET|n/a|  
|201|Created|POST|n/a|  
|202|Accepted|POST|n/a|  
|204|No content|POST, PUT, DELETE|n/a|  
|307|Temporary Redirect|GET|n/a|  
|304|Not Modified|Conditional GET|n/a|  
|400|Bad request|All|No|  
|401|Unauthorized; authentication not provided|All|No|  
|403|Forbidden; authenticated but not authorized|All|No|  
|404|Not found|All|No|  
|405|(Method) Not allowed|All|No|  
|406|Not acceptable - Accept header doesn't match a response type supported by the server|GET|No|  
|408|Timeout|All|Yes|  
|409|Resource conflict - state of resource doesn't allow modification|PUT, POST, DELETE|Yes|  
|412|Precondition failed|PUT|No|  
|413|Request entity too large -- size of request exceeded server limit|POST, PUT|No|  
|414|Request URI too long|POST, PUT|No|  
|415|Unsupported type -- representation not supported|POST, PUT|No|  
|500|Server error (internal)<br /><br /> This should be used only in situations that are not covered by above options.|All|No|  
|501|Not implemented|All|Yes|  
|503|Service Unavailable|All|No|  
  
## See Also  
 [Upload a video to Azure blob](https://code.msdn.microsoft.com/Windows-Azure-Storage-CORS-45e5ce76)   
 [Getting Started with Azure Media Services Connector](https://azure.microsoft.com/blog/2015/03/25/getting-started-with-azure-media-services-connector/)   
 [Announcing Media APIs for Azure App Service](http://azure.microsoft.com/blog/2015/03/25/announcing-media-apis-for-azure-app-service/)
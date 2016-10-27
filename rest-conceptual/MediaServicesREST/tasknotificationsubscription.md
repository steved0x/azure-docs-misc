---
title: "TaskNotificationSubscription"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4cf7990b-4d2b-4b56-a553-a6cac29a427c
caps.latest.revision: 3
author: "Juliako"
ms.author: "juliako"
manager: "erikre"
---
# TaskNotificationSubscription
Defines the notification endpoint task state changes. Also,  indicates whether to include task progress for which to be notified.  
  
 This topic gives an overview of the `TaskNotificationSubscription` entity and also demonstrates how to execute various operations with the Media Services REST API.  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://msdn.microsoft.com/en-us/42ae6204-93bc-4797-bf40-1c68512cfb73).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
## TaskNotificationSubscription Entity Properties  
 Insert section body here.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|IncludeTaskProgress<br /><br /> Required.|Edm.Boolean|Boolean that indicates whether to include the task progress or not.|  
|NotificationEndPointId|Edm.String|Endpoint Id from which the subscriber receives notifications.|  
|TargetTaskState<br /><br /> Required.|Edm.Int32|The state changes for which the subscriber is receiving notifications.|  
||||
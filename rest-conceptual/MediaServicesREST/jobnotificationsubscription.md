---
title: "JobNotificationSubscription"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 6345e97e-6755-4c73-9291-ae30c8bc8da3
caps.latest.revision: 10
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
# JobNotificationSubscription
Contains information about the state of the job and the endpoint from which the notification is sent.  
  
 This type was added in Media Services version 2.1.  
  
> [!NOTE]
>  Azure queue notification may have some delay.  
  
##  <a name="job_entity_properties"></a> JobNotificationSubscription Complex Type Properties  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`TargetJobState`<br /><br /> Required.|Edm.Int32|The state of the job that subscriber wants to get notifications about.<br /><br /> Valid values are:<br /><br /> -   FinalStatesOnly = 1. The final states are: Finished, Canceled, and Error.<br />-   AllStates = 2<br />     Queued, Scheduled, Processing, Finished, Error, Canceled, Canceling.<br />-   None = 0<br />     If a job with JobNotificationSubscription.TargetJobState = None is submitted, the `DataServiceRequestException` exception is thrown with the following message “JobNotificationSubscription.TargetJobState must not be 0”.|  
|`NotificationEndPointId`<br /><br /> Required.|Edm.String|The id of the endpoint from which the subscriber receives notifications about the job state.|  
  
## See Also  
 [Job](../MediaServicesREST/job.md)
---
title: "StorageAccount"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 39588ce7-2714-4bdd-bf76-27b1f4d39633
caps.latest.revision: 6
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
# StorageAccount
A collection of `StorageAccount` objects contains all of the storage accounts linked to the specified Microsoft Azure Media Services account.  
  
## StorageAccount Entity Properties  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`Name`<br /><br /> Read-only.|Edm.String|The name of the storage account.|  
|`IsDefault`<br /><br /> Read-only.|Edm.Boolean|This Boolean value indicates whether this storage account is the default one.|  
|`BytesUsed`|Edm.Int64|If Storage Account Metrics are enabled on the storage account, this returns the number of bytes used in the storage account by blob data. If Storage Account Metrics are not enabled or no data is available, then null is returned.|
---
title: "AssetDeliveryPolicy"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 882d5eae-417d-4cd3-85b7-deb3b4e49726
caps.latest.revision: 7
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
# AssetDeliveryPolicy
Describes delivery polices for an asset.  
  
##  <a name="mediaprocessor_entity_properties"></a> AssetDeliveryPolicy Entity Properties  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`Id`<br /><br /> Read-only. Set by Media Services.|Edm.String|Unique identifier.|  
|`Name`|Edm.String|Friendly name of the asset delivery policy.|  
|`AssetDeliveryProtocol`|Edm. Int32|Delivery protocol.|  
|`AssetDeliveryPolicyType`|Edm. Int32|Policy type.|  
|`AssetDeliveryConfiguration`|Edm. String|Asset delivery configuration.|  
|`Crated`<br /><br /> Read-only. Set by Media Services at creation time.|Edm.DateTime|This value is set by Media Services at creation time.|  
|`LastModified`<br /><br /> Read-only. Set by Media Services.|Edm.DateTime|This value is updated by Media Services after any property changes are made.|
---
title: "Task Preset for Azure Media Hyperlapse (preview)"
ms.custom: na
ms.date: 2016-07-13
ms.prod: azure
ms.reviewer: na
ms.service: media-services
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95892de4-8e14-4715-9a1e-83f5d6705c86
caps.latest.revision: 5
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
# Task Preset for Azure Media Hyperlapse (preview)
The `Azure Media Hyperlapse` media processor enables you to smooth out the "bumps" in your video with video stabilization. Also allows you to speed up your content into a consumable clip. For more detailed information, see [Announcing Azure Media Hyperlapse](http://go.microsoft.com/fwlink/?LinkId=613274).  
  
## Azure Media Hyperlapse Configuration XML  
 The following table explains elements and attributes of the configuration XML.  
  
|Name|Description|  
|----------|-----------------|  
|`StartFrame`|The frame to begin Hyperlapse processing.|  
|`NumFrames`|The number of frames to process (during preview, any number larger than 10,000 will be capped at 10,000).|  
|`Speed`|The speed factor of the Hyperlapse (for example, 2 would mean a 1 minute video Hyperlapse’d to 30 seconds).|  
  
 The following example shows the Azure Media Hyperlapse configuration XML.  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Sources>  
    <Source StartFrame="0" NumFrames="2147483647">  
      <InputFiles />  
    </Source>  
  </Sources>  
  <Options>  
    <Speed>12</Speed>  
  </Options>  
</Preset>  
  
```  
  
## See Also  
 [Announcing Azure Media Hyperlapse](http://azure.microsoft.com/blog/?p=286281&preview=1&_ppp=61e1a0b3db)
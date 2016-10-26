---
title: "Get the state of a batch job"
ms.custom: ""
ms.date: "2015-12-02"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 8c4adc28-9716-4892-9c2a-33de94320381
caps.latest.revision: 6
author: "nitinme"
ms.author: "nitinme"
manager: "jhubbard"
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
# Get the state of a batch job
## Request  
 See Common parameters and headers for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://{cluster-endpoint}/livy/batches/{batch-id}`|  
  
## Response  
 If validation is complete and the request is accepted, the operation will return 200 (OK).  
  
 Status code: 200 OK  
  
 Response body:  
  
```  
{  
"id" : 1,  
"state" : "starting",  
“log" : ["logline"]  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|id|Yes|Integer|The batch session id|  
|log|Yes|Array of strings|Array of log lines for this batch job.|  
|state|Yes|String|The session state. Possible value: [“starting”, “idle”, “error”]|
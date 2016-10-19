---
title: "Get the state of an interactive session"
ms.custom: ""
ms.date: "2015-12-02"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: b931460e-7781-4ac3-a3c1-4f111b11f268
caps.latest.revision: 5
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
# Get the state of an interactive session
## Request  
 See [Common parameters and headers](../HDInsightSparkREST/interactive-sessions.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://{cluster-endpoint}/livy/sessions/{session-id}`|  
  
## Response  
 If validation is complete and the request is accepted, the operation will return 200 (OK).  
  
 **Status code:** 200 OK  
  
 **Response body:**  
  
```  
{  
"id" : 1,  
"state" : "starting",  
"kind" : "spark",  
“log" : ["logline"]  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|id|Yes|Integer|The batch session id|  
|Kind|Yes|String|The session kind. Possible values: [“spark”, “pyspark”, “sparkr”]|  
|log|Yes|Array of strings|Array of log lines for this batch job.|  
|state|Yes|String|The session state. Possible value: [“starting”, “idle”, “error”]|
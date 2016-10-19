---
title: "Return all active interactive sessions"
ms.custom: ""
ms.date: "2015-12-02"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 47017666-1c28-4d5f-b9d6-b7b8373e2ff5
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
# Return all active interactive sessions
## Request  
 See [Common parameters and headers](../HDInsightSparkREST/interactive-sessions.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://{cluster-endpoint}/livy/sessions`|  
  
## Response  
 If validation is complete and the request is accepted, the operation will return 200 (OK).  
  
 **Status code:** 200 OK  
  
 **Response body:**  
  
```  
{  
	"from" : 0,  
	"total" : 2,  
	"sessions" : [{  
			"id" : 1,  
			"state" : "starting",  
			"kind" : "spark",  
			"log" : ["logline"]  
		}, {  
			"id" : 0,  
			"state" : "idle",  
			"kind" : "spark",  
			"log" : ["logline"]  
		}  
	]  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|from|Yes|String|Offset|  
|total|Yes|String|Amount of sessions to return|  
|sessions|Yes|Array of Complex  Type (Session)|A list of active sessions|  
  
### Session  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|id|Yes|Integer|The interactive session id|  
|Kind|Yes|String|The session kind. Possible values: [“spark”, “pyspark”, “sparkr”]|  
|log|Yes|Array of strings|Array of log lines for this session.|  
|state|Yes|String|The session state. Possible value: [“starting”, “idle”, “error”, “running”, “success”]|
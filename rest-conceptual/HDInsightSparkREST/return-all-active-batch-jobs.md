---
title: "Return all active batch jobs"
ms.custom: ""
ms.date: "2016-11-16"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: d1a4b77c-9ae6-4abf-9de4-8f7171db8980
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
# Return all active batch jobs
## Request  
 See [Common parameters and headers](../HDInsightSparkREST/batch-jobs.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://{cluster-endpoint}/livy/batches`|  
  
## Response  
 If validation is complete and the request is accepted, the operation will return 200 (OK).  
  
 **Status code**: 200 OK  
  
 **Response body:**  
  
```json  
{  
	"from" : 0,  
	"total" : 2,  
	"sessions" : [{  
			"id" : 1,  
			"state" : "starting",  
			"log" : ["logline"]  
		}, {  
			"id" : 0,  
			"state" : "idle",  
			"log" : ["logline"]  
		}  
	]  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|from|Yes|String|Offset|  
|total|Yes|String|Amount of batches to return|  
|session|Yes|Array of Complex  Type (Batch)|A list of active batch jobs|  
  
### Batch  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|id|Yes|Integer|The batch session id|  
|log|Yes|Array of strings|Array of log lines for this batch job.|  
|state|Yes|String|The session state. Possible value: [“starting”, “idle”, “error”]|
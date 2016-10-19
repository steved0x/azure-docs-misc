---
title: "Get the full log of a batch job"
ms.custom: ""
ms.date: "2015-12-02"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 10f744f1-a073-4a45-ba78-1847fcbb668c
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
# Get the full log of a batch job
## Request  
 See [Common parameters and headers](../HDInsightSparkREST/batch-jobs.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://{cluster-endpoint}/livy/batches/{batch-id}/log`|  
  
## Response  
 If validation is complete and the request is accepted, the operation will return 200 (OK).  
  
 Status code: 200 OK  
  
 Response body:  
  
```  
{  
"id" : 1,  
"from":0,  
"total":54  
“log" : ["logline1", “logline2”]  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|id|Yes|Integer|The batch session id|  
|from|Yes|Integer|Offset|  
|size|Yes|Integer|Total amount of lines|  
|log|Yes|Array of string|Array of log lines for this batch job.|
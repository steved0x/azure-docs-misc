---
title: "Kill a batch job"
ms.custom: ""
ms.date: "2016-11-16"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: b29ac44f-cea3-4a4d-b67b-b92457078f23
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
# Kill a batch job
## Request  
 See [Common parameters and headers](../HDInsightSparkREST/batch-jobs.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|DELETE|`https://{cluster-endpoint}/livy/batches/{batch-id}`|  
  
## Response  
 If validation is complete and the request is accepted, the operation will return 200 (OK).  
  
 Status code: 200 OK  
  
 Response body:  
  
```  
{  
"msg" : "deleted"  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|Message|Yes|String|The message of the delete.|  
  
## Interactive sessions  
  
-   Start, submit statement, retrieve statement result and terminate an interactive session
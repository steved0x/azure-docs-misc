---
title: "Submit statement(s) to an interactive session1"
ms.custom: ""
ms.date: "2015-12-02"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: b6cbcdbf-182d-46c7-9e44-d61e0a740367
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
# Submit statement(s) to an interactive session
## Request  
 See [Common parameters and headers](../HDInsightSparkREST/interactive-sessions.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|POST|`https://{cluster-endpoint}/livy/sessions/{session-id}/statements`|  
  
 Following shows an example request to create a new interactive session.  
  
```  
{  
	"code" : "1 + 1"  
}  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|Code|Yes|String|The code to execute|  
  
## Response  
 If validation is complete and the request is accepted, the operation will return 200 (OK).  
  
 **Status code:** 200 OK  
  
 **Response body:**  
  
```  
{  
"id" : 1,  
"state" : "running",  
"output" : null  
}  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|id|Yes|Integer|The batch session id|  
|Output|Yes|String|Output of statement|  
|state|Yes|String|The session state. Possible value: [“starting”, “idle”, “error”]|
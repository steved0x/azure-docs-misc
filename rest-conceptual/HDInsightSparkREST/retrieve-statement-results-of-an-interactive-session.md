---
title: "Retrieve statement results of an interactive session"
ms.custom: ""
ms.date: "2015-12-02"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 0bb04aa7-5016-49ed-97bd-2f60e2a95a12
caps.latest.revision: 7
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
# Retrieve statement results of an interactive session
## Request  
 See [Common parameters and headers](../HDInsightSparkREST/interactive-sessions.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://{cluster-endpoint}/livy/sessions/{session-id}/statements`|  
  
## Response  
 If validation is complete and the request is accepted, the operation will return 200 (OK).  
  
 **Status code:** 200 OK  
  
 **Response body:**  
  
```  
{  
"total_statements" : 1,  
"statements" : [{  
			"id" : 0,  
			"state" : "available",  
			"output" : {  
				"status" : "ok",  
				"execution_count" : 1,  
				"data" : {  
					"text/plain" : "res1: Int = 2"  
				}  
			}  
		}  
	]  
}  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|Total_statements|Yes|Integer|Total number of statements|  
|Statements|Yes|Array of complex Type (Statement)|Output of statement|  
  
 **Statement**  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|Id|Yes|Integer|The statement id|  
|State|Yes|String|The statement state.|  
|Output|Yes|Complex type (Output)|The output of the statement.|  
  
 **Output**  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|Status|Yes|String|The statement status|  
|Execution_count|Yes|Integer|The number of execution|  
|data|Yes|Complex type (Text)|The text output of the statement.|  
  
 **Text**  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|Text/plain|Yes|String|The plain text of the output|
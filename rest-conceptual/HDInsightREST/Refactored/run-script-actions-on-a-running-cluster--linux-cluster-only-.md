---
title: "Run Script Actions on a running cluster (Linux cluster only)"
ms.custom: ""
ms.date: "2016-11-16"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 765ad75a-52b4-4187-aff4-f6d862a2d8d1
caps.latest.revision: 4
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
# Run Script Actions on a running cluster (Linux cluster only)
Execute Script action on a running cluster.  
  
## Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|POST|https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/executeScriptActions?api-version={api-version}|  
  
 **Request Body**  
  
```  
{  
  "scriptActions": [  
    {  
      "name": "script-name",  
      "uri": "script-uri",  
      "parameters": "script-parameters",  
      "roles": [  
        "headnode",  
        "workernode"  
      ]  
    },  
    ...  
  ],  
  "persistOnSuccess": true  
}  
  
```  
  
###  <a name="rdpSettings"></a> scriptActions  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|name|Yes|String|Specifies the name of the script action|  
|uri|Yes|String|Specifies the URI of the script action|  
|parameters|Yes|String|Specifies the parameters required by the script ation|  
|roles|Yes|Array of String|Specifies the target roles that the script action executes on|  
|persistOnSuccess|Yes|Boolean|Specifies whether the script actions will be persisted after successful executions|  
  
## Response  
 If validation is complete and the request is accepted, the operation will return 202 (Accepted).  
  
 **Status code:** 202 (Accepted)
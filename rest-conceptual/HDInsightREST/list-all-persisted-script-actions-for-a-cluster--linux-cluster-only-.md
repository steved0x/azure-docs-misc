---
title: "List all persisted Script Actions for a cluster (Linux cluster only)"
ms.custom: ""
ms.date: "2016-11-16"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 9cfe6578-b2c9-43db-a006-d3f01b5d127f
caps.latest.revision: 3
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
# List all persisted Script Actions for a cluster (Linux cluster only)
This operation returns all the persisted scripts actions of the specified cluster.  
  
## Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/scriptActions?api-version={api-version}|  
  
## Response  
 HTTP 200 (OK) on successful completion of the operation.  
  
 **Status code:** 200 OK  
  
 Example response:  
  
```  
{  
"value":  
[  
  {  
    "name":"script-name",  
    "uri":"script-uri",  
    "parameters":"script-parameters",  
    "roles":["headnode","workernode"],  
    "applicationName":null  
  },  
  ...  
]  
}  
```  
  
|Element name|Type|Description|  
|------------------|----------|-----------------|  
|name|String|Specifies the name of the script action.|  
|uri|String|Specifies the URI of the script action.|  
|parameters|String|Specifies the parameters required by the script action|  
|roles|Array of String|Specifies the targeted roles that the script action executes on.|  
|applicationName|String|Specifies the corresponding application that the script is associated with. applicationName is null if the script is provided by users|
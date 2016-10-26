---
title: "List clusters in a resource group"
ms.custom: ""
ms.date: "2015-11-18"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 4318887e-22ef-49c2-88b0-2bc5cf22f8f7
caps.latest.revision: 9
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
# List clusters in a resource group
This operation lists all the clusters in the user’s subscription.  
  
## Request  
 See  [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://management.azure.com/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupId}/providers/Microsoft.HDInsight/clusters?api-version={api-version}`|  
  
## Response  
 The operation will return 200 (OK) if the request is completed successfully.  
  
 **Status code**: 200 OK  
  
 Response body is an array of cluster details. For more information, see [Get cluster properties](../HDInsightREST/get-cluster-properties.md).  
  
```  
{  
  “value”: [  
		{ Cluster details }  
    ]  
}  
  
```
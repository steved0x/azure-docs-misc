---
title: "List clusters in a subscription3"
ms.custom: ""
ms.date: "2015-11-05"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 1d9d3a66-29f6-47f0-af93-e4c920b12a82
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
# List clusters in a subscription
This operation lists all the clusters in the user’s subscription.  
  
## Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.HDInsight/clusters?api-version={api-version}`|  
  
## Response  
 The operation will return 200 (OK) if the request is completed successfully.  
  
 **Status code:** 200 OK  
  
 Response body is an array of cluster details.  
  
```  
{  
  “value”: [  
		{ Cluster details }  
    ]  
}  
```
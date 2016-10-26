---
title: "Resize cluster"
ms.custom: ""
ms.date: "2015-11-05"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 045d64b7-6f08-4731-a95d-09c21971f1dd
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
# Resize cluster
This operation allows users to resize an existing HDInsight cluster.  
  
## Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|POST|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/roles/{rolename}/resize?api-version={api-version}`|  
  
 Following shows an example request to update tags for a cluster  
  
```  
{  
    "targetInstanceCount": 10  
}  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|targetInstanceCount|Yes|Int|Specifies the new instance count for the role|  
  
## Response  
 HTTP 202 (Accepted) to indicate that the operation will complete asynchronously. Async polling will return a 204 (NoContent) once the operation completes successfully.  
  
## Remarks  
 To track progress of a delete cluster request, see [Asynchronous Operations (202 Accepted and Location header)](../HDInsightREST/asynchronous-operations--202-accepted-and-location-header-.md)
---
title: "Delete a cluster"
ms.custom: ""
ms.date: "2015-11-05"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: f94e6abd-8891-4293-9f87-682eab047be6
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
# Delete a cluster
This operation deletes an HDInsight cluster.  
  
## Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|DELETE|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}?api-version={api-version}`|  
  
## Response  
 HTTP 202 (Accepted) to indicate that the operation will complete asynchronously. Async polling will return a 204 (NoContent) once the operation completes successfully.  
  
## Remarks  
 To track progress of a delete cluster request, see [Asynchronous Operations (202 Accepted and Location header)](../HDInsightREST/asynchronous-operations--202-accepted-and-location-header-.md)
---
title: "Remove an HDInsight application"
ms.custom: ""
ms.date: "2016-11-16"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: eaadd5bc-b6dd-467c-82dc-a9f50c3fcb98
caps.latest.revision: 3
author: "nitinme"
ms.author: "nitinme"
manager: "jhubbard"
robots: noindex,nofollow
---
# Remove an HDInsight application
This operation removes an HDInsight application from the cluster.  
  
## Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|DELETE|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/applications/{applicationName}?api-version={api-version}`|  
  
## Response  
 The operation will return 202 (Accepted) if the request is completed successfully  
  
 **Status code:** 202 Accepted.
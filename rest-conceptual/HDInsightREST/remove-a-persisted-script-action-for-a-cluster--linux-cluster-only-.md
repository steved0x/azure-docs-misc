---
title: "Remove a persisted Script Action for a cluster (Linux cluster only)"
ms.custom: ""
ms.date: "2016-11-16"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 325f0b4c-4829-41d1-ad8a-f39cb56566b7
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
# Remove a persisted Script Action for a cluster (Linux cluster only)
This operation removes an HDInsight persisted script action for a cluster.  
  
## Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|DELETE|https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/scriptActions/{scriptName}?api-version={api-version}|  
  
## Response  
  
-   HTTP 200 (OK) to indicate that the script action has been removed from the list of persisted script actions.  
  
-   HTTP 404 (NotFound) to indicate that there is no existing persisted script action with corresponding scriptName.
---
title: "Update a cluster2"
ms.custom: ""
ms.date: "2015-11-05"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 2e73be89-9193-49b6-a764-b7ce564a7588
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
# Update a cluster
Update tags for a cluster.  
  
 All other updates are separate actions described separately.  
  
## Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|PATCH|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}?api-version={api-version}`|  
  
 Following shows an example request to update tags for a cluster  
  
```  
{   
    "tags": {"department": "finance"}  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|tags|Yes|String|Specifies the tags that will be assigned to the cluster. For more information about using tags, see [Using tags to organize your Azure resources](https://azure.microsoft.com/en-us/documentation/articles/resource-group-using-tags/).|  
  
## Response  
 The operation will return 200 (OK) if the request is completed successfully.  
  
 **Status code:** 200 OK  
  
 Response body is the same as [Create a cluster](../HDInsightREST/create-a-cluster.md).
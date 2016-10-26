---
title: "Get cluster configuration type details"
ms.custom: ""
ms.date: "2016-11-16"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 75afe517-38b6-4773-b095-20fc541f8d14
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
# Get cluster configuration type details
This operation allows users to get details about a single configuration type.  
  
## Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/configurations/{configurationType}?api-version={api-version}`|  
  
## Response  
 HTTP 200 (OK) on successful completion of the operation.  
  
 Example response:  
  
```  
“gateway”: {  
     “restAuthCredential.isEnabled”: true,  
     "restAuthCredential.username": "user",  
     "restAuthCredential.password": "password here"     
   }  
  
```
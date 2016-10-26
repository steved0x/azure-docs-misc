---
title: "Change connectivity settings"
ms.custom: ""
ms.date: "2016-11-16"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: e4cc9de6-506f-49f7-85df-cc5100de63e6
caps.latest.revision: 5
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
# Change connectivity settings
This operation allows users to enable/disable the HTTPS connectivity to the cluster.  
  
## Request  
 See [Common parameters and headers](../HDInsightREST/clusters.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|POST|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/configurations/{configurationType}?api-version={api-version}`|  
  
 **To enable connectivity**  
  
```  
{  
   "restAuthCredential.isEnabled": true,  
   "restAuthCredential.username": "user",  
   "restAuthCredential.password": "password here"  
}  
  
```  
  
 **To disable connectivity**  
  
```  
{  
   "restAuthCredential.isEnabled": false  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|restAuthCredential.isEnabled|Yes|Boolean|Specifies if connectivity should be enabled or disabled|  
|restAuthCredential.username|No|String|Required if isEnabled=true <br />Specifies the username for connectivity settings|  
|restAuthCredential.password|No|String|Required if isEnabled=true <br />Specifies the password for connectivity settings|  
  
## Response  
 HTTP 202 (Accepted) to indicate that the operation will complete asynchronously. Async polling will return a 204 (NoContent) once the operation completes successfully.  
  
## Remarks  
 To track progress of a delete cluster request, see [Asynchronous Operations (202 Accepted and Location header)](../HDInsightREST/asynchronous-operations--202-accepted-and-location-header-.md)
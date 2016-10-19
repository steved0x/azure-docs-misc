---
title: "Get cluster configurations"
ms.custom: ""
ms.date: "2016-11-16"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 7c0e49be-dfd3-4edb-92b9-65a29139a3e8
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
# Get cluster configurations
This operation allows users to cluster configuration details.  
  
## Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/configurations?api-version={api-version}`|  
  
## Response  
 HTTP 200 (OK) on successful completion of the operation.  
  
 Example response:  
  
```  
"configurations":   
{  
   “gateway”: {  
     “restAuthCredential.isEnabled”: true,  
     "restAuthCredential.username": "user",  
     "restAuthCredential.password": "password here"     
   },  
  
   "core-site": {  
	   “key1”: “value1”  
   }  
}  
  
```  
  
|Element name|Type|Description|  
|------------------|----------|-----------------|  
|configurations|Dictionary|This is a dictionary of configuration type and its associated value dictionary.  <br />gateway configuration type is used to configure the http user used for connecting to web api;s and the ambari portal  <br />core-site configuration type is used to configure the default storage account for the cluster|
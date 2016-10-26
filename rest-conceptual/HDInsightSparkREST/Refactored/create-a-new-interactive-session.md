---
title: "Create a new interactive session"
ms.custom: ""
ms.date: "2015-12-02"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: a492e0fa-8fb8-4ecd-bdd8-d3d92356ef1b
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
# Create a new interactive session
Start a new interactive session.  
  
## Request  
 See [Common parameters and headers](../HDInsightSparkREST/interactive-sessions.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|POST|`https://{cluster-endpoint}/livy/sessions`|  
  
 Following shows an example request to create a new interactive session  
  
```  
{  
	"kind" : "spark",  
	"jars" : ["wasb://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/helper.jar"],  
	"files" : ["wasb://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/config.xml"],  
	"driverMemory" : "1G",  
	"driverCores" : 2,  
	"executorMemory" : "1G",  
	"executorCores" : 10,  
	"numExecutors" : 10  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|Kind|Yes|String|The session kind. Possible values: [“spark”, “pyspark”, “sparkr”]|  
|proxyUser|No|String|The user to impersonate that will execute the job|  
|jars|No|Array of String|Files to be placed on the java classpath|  
|pyFiles|No|Array of String|Files to be placed on the PYTHONPATH|  
|files|No|Array of String|Files to be placed in executor working directory|  
|driverMemory|No|String|Memory for driver (e.g. 1000M, 2G)|  
|driverCores|No|Integer|Number of cores used by driver|  
|executorMemory|No|String|Memory for executor (e.g. 1000M, 2G)|  
|executorCores|No|Integer|Number of cores used by executor|  
|numExecutors|No|Integer|number of executor|  
|archives|No|Array of String|Archives to be uncompressed (YARN mode only)|  
  
## Response  
 The operation will return 200 (OK) if the request is completed successfully  
  
 **Status code:** 200 OK  
  
 **Response body:**  
  
```  
{  
"id" : 1,  
"state" : "starting",  
"kind" : "spark",  
“log" : ["logline"]  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|id|Yes|Integer|The interactive session id|  
|Kind|Yes|String|The session kind. Possible values: [“spark”, “pyspark”, “sparkr”]|  
|log|Yes|Array of strings|Array of log lines for this batch job.|  
|State|Yes|String|The session state. Possible value: [“starting”, “idle”, “error”, “running”, “success”]|
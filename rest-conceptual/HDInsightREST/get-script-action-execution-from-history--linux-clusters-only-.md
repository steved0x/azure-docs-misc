---
title: "Get Script Action execution from history (Linux clusters only)"
ms.custom: ""
ms.date: "2016-11-16"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 205c22af-8013-45d9-9473-77c62aa02433
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
# Get Script Action execution from history (Linux clusters only)
This operation returns latest scripts action execution of the specified cluster or execution details for an individual script execution.  
  
## Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/scriptExecutionHistory/{scriptExecutionId}?api-version={api-version}|  
  
## Response  
 The operation will return 200 (OK) if the request is completed successfully. Response body is an array of script execution details or a single script execution details if scriptExecutionId is provided. Below is an example of a script execution detail.  
  
 **Status code:** 200 (OK)  
  
 Example response:  
  
```  
{  
  "scriptExecutionId":script-execution-id,  
  "name":"script-name",  
  "applicationName":null,  
  "uri":"script-uri",  
  "parameters":"script-parameters",  
  "roles":["headnode","workernode"],  
  "startTime":"2016-02-26T23:49:13.0773637Z",  
  "endTime":"2016-02-26T23:49:33.4964725Z",  
  "status":"Succeeded",  
  "operation":"PostClusterCreateScriptActionRequest",  
  "executionSummary":  
	[{"status":"COMPLETED",  
	 "instanceCount":4}],  
  "debugInformation": "debug-information"  
}  
  
```  
  
|Element name|Type|Description|  
|------------------|----------|-----------------|  
|scriptExecutionId|Long|Specifies the execution id of the script action.|  
|name|String|Specifies the name of the script action.|  
|applicationName|String|Specifies the corresponding application that the script is associated with. applicationName is null if the script is provided by users|  
|uri|String|Specifies the URI of the script action.|  
|parameters|String|Specifies the parameters required by the script action|  
|roles|Array of String|Specifies the targeted roles that the script action executes on.|  
|startTime|DateTime|Specifies the start time of the script action execution|  
|endTime|DateTime|Specifies the end time of the script action execution|  
|status|String|Specifies the status of the script action execution|  
|operation|String|Specifies the reason why the script action was executed. E.g: ScaleUp means that the script action was executed during cluster scale up.|  
|executionSummary|Array of complex type|Specifies the summary of execution in terms of how many hosts succeeded and how many hosts failed to execute the script.|  
|debugInformation|String|Specifies detailed debug information for the script. debugInformation is returned only when a scriptExecutionId is provided in the request.|  
  
### executionSummary  
  
|Element name|Type|Description|  
|------------------|----------|-----------------|  
|status|String|Specifies the status of the execution on individual hosts.|  
|instanceCount|Int|Specifies the number of executions with corresponding status.|
---
title: "Create Transformation (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 2fe3e3dc-1fcf-4c7d-a0cf-ff6d668a9b2e
caps.latest.revision: 18
author: jeffstokes72
manager: jhubbard
translation.priority.mt: 
  - de-de
  - es-es
  - fr-fr
  - it-it
  - ja-jp
  - ko-kr
  - pt-br
  - ru-ru
  - zh-cn
  - zh-tw
---
# Create Transformation (Azure Stream Analytics)
  Creates a new transformation within a Stream Analytics job.  
  
## Request  
 The **Create Transformation** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**PUT**|https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs/{job-name}/transformations/{transformation-name}?api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that the job belongs to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name of the Stream Analytics job.  
  
 Replace {transformation-name} with the name (or alias) that you want to assign to the transformation that you are creating. The transformation name is case insensitive and must contain only numbers, letters, and hyphens. It must be 3 to 63 characters long.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
 **JSON**  
  
```  
  
{    
   "properties":{    
      "streamingUnits":1,  
      "query":"select * from MyEventHubSource"  
   }  
}  
  
```  
  
|Element name|Required|Notes|  
|------------------|--------------|-----------|  
|**streamingUnits**|No|The number of streaming units that the streaming job uses. Defaults to 1 if the value is not specified.|  
|**query**|Yes|The query that will be run in the Stream Analytics job.|  
  
## Response  
 Status code: 201  
  
 **JSON**  
  
```  
  
{    
   "id":"/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/Default-SA-CentralUS/providers/Microsoft.StreamAnalytics/streamingjobs/myStreamingSample/transformations/MyTransformation",  
   "name":"MyTransformation",  
   "type":"Microsoft.StreamAnalytics/streamingjobs/transformations",  
   "properties":{    
      "streamingUnits":1,  
      "script":null,  
      "query":"select * from MyEventHubSource"  
   }  
}  
  
```  
  
  
---
title: "Get Information about an Output (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: e6dd7ec2-9c6a-4611-a04d-cb42ffc6938e
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
# Get Information about an Output (Azure Stream Analytics)
  Gets information about a specific output.  
  
## Request  
 The **Get Information about an Output** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**GET**|https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs/{job-name}/outputs/output?api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name of the Stream Analytics job that your output will be associated with.  
  
 Replace {input-name} with the name of the input that you want information about.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
## Response  
 Status code: 200  
  
 **JSON**  
  
```  
  
{    
   "id":"/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/Default-SA-CentralUS/providers/Microsoft.StreamAnalytics/streamingjobs/myStreamingSample/outputs/output",  
   "name":"output",  
   "type":"Microsoft.StreamAnalytics/streamingjobs/outputs",  
   "properties":{    
      "datasource":{    
         "type":"Microsoft.Sql/Server/Database",  
         "properties":{    
            "server":"sampleserver",  
            "database":"sampleDB",  
            "table":"sampleTable",  
            "user":"user@sampleserver"  
         }  
      }  
   }  
}  
```  
  
 Secrets are never returned in the **GET** response.  
  
  
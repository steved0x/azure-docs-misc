---
title: "List Functions (Stream Analytics)"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: efed01fe-a836-476f-b5e0-b2db9562dc58
caps.latest.revision: 5
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
# List Functions (Stream Analytics)
  Lists all of the functions that are defined in a Stream Analytics job.  
  
## Request  
 The **List Functions** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**GET**|https://managment.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs/{job-name}/functions&api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name of the Stream Analytics job.  
  
 Replace {api-version} with 2015-10-01-preview in the URI.  
  
## Response  
 Status code: 200  
  
 **JSON**  
  
 The example below shows a response from a List Functions  request for an Stream Analytics job with one Azure Machine Learning Function.  
  
```  
  
{   
  "id": "/subscriptions/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx/resourceGroups/0c3767c3-b17f-45ba-a306-cd490802f99f/providers/Microsoft.StreamAnalytics/streamingjobs/581ca559-5224-46b6-8668-dae42d0194be/functions/azuremlscalarFunction",  
  "name": "azuremlscalarFunction",   
  "type": "Microsoft.StreamAnalytics/streamingjobs/functions",   
  "properties": {   
    "type": "Scalar",   
    "properties": {   
      "inputs": [   
        {   
          "dataType": "nvarchar(max)",   
          "isConfigurationParameter": false   
        }   
      ],   
      "output": {   
        "dataType": "nvarchar(max)"   
      },   
      "binding": {   
        "type": "Microsoft.MachineLearning/WebService",   
        "properties": {   
          "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77fa4a46bf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",   
          "apiKey": null,   
          "inputs": {   
            "name": "input1",   
            "columnNames": [   
              {   
                "name": "78f69f41-aab4-43d2-844a-800b116eed3a",   
                "dataType": "Boolean",   
                "mapTo": 0   
       }   
            ]   
          },   
          "outputs": [   
            {   
              "name": "output",   
              "dataType": "String"   
            }   
          ],   
          "batchSize": 100   
        }   
      }   
    }   
  }   
}  
  
```  
  
  
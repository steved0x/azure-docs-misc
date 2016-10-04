---
title: "Get Function (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: df7039ac-b64b-4708-95ef-941b7ee73fa8
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
# Get Function (Azure Stream Analytics)
  Gets information about a specific user-defined function.  
  
## Request  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**GET**|https://<endpoint\>/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions/{functionName}?api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name of the Stream Analytics job that you want information about.  
  
 Replace functionName with the name of the user-defined function.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
## Response  
 Status code: 200  
  
 **JSON**  
  
```  
  
{  
  "id": "/subscriptions/{id}/resourceGroups/{group}/providers/microsoft.streamAnalytics/streamingjobs/filterSample/functions/{functionName}",  
  "name": {functionName},  
  "type": "Microsoft.StreamAnalytics/streamingjobs/functions",  
  "properties": {  
    "type": {functionType},  
    "properties": {  
      .  
      . function type-specific properties  
      .  
    }  
  }  
}  
  
```  
  
 Example Azure Machine Learning RRS scalar UDF response.  
  
```  
{  
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/providers/Microsoft.StreamAnalytics/streamingjobs/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/functions/azuremlscalarFunction",  
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
          "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx/services/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx/execute",  
          "apiKey": null,  
          "inputs": {  
            "name": "input1",  
            "columnNames": [  
              {  
                "name": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",  
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
  
 **Note**: The Azure Machine Learning RRS apiKey secret is not returned in the GET response.  
  
  
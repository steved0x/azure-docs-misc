---
title: "List Outputs (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: ebcf4673-7cf1-41b7-b9b2-e040aa9d9cd7
caps.latest.revision: 9
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
# List Outputs (Azure Stream Analytics)
  Lists all of the inputs that are defined in a Stream Analytics job.  
  
## Request  
 The **List Outputs** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx)  
  
|Method|Request URI|  
|------------|-----------------|  
|**GET**|https://managment.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs/{job-name}/outputs&api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/)  
  
 Replace {job-name} with the name of the Stream Analytics job.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
## Response  
 Status code: 200  
  
 **JSON**  
  
```  
  
{  
  "value": [  
    {  
      "id": "/subscriptions/{id}/resourceGroups/{group}/providers/microsoft.streamAnalytics/streamingjobs/filterSample/outputs/filteredData",  
      "name": "filteredData",  
      "type": "Microsoft.StreamAnalytics/streamingjobs/outputs",  
      "properties": {  
        "etag": "47956D46-4756-4857-9832-D3955AA721FB",  
        "datasource": {  
         "type": "Microsoft.Sql/Server/Database",  
          "properties": {  
           "server": "xyzzy1.database.windows.net",  
            "database": "Samples",  
            "table": "filteredSampleResults"  
          }  
        }  
      }  
    }  
  ],  
  "nextLink": null  
}  
  
```  
  
  
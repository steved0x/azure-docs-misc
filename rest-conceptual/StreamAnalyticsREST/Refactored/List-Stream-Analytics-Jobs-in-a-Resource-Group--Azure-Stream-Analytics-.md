---
title: "List Stream Analytics Jobs in a Resource Group (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 1bf2cd0d-b5d7-4b79-8941-8c8892b5b92e
caps.latest.revision: 20
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
# List Stream Analytics Jobs in a Resource Group (Azure Stream Analytics)
  Lists all of the Stream Analytics jobs that are defined in a resource group.  
  
## Request  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**GET**|https://managment.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs?$expand={properties-to-expand}&api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace the values of the following parameters as you need them:  
  
-   The request will support the $expand query option. The endpoint will by default exclude the Inputs, Transformation, Outputs, and  Functions properties if the request does not have the $expand query parameter. Specifying the query parameter ($expand=Inputs,Transformation,Outputs,Functions) will return those properties.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
## Response  
 Status code: 200  
  
```  
  
{    
   "value":[    
      {    
         "id":"/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/Default-SA-CentralUS/providers/Microsoft.StreamAnalytics/streamingjobs/myStreamingSample",  
         "name":"myStreamingSample",  
         "type":"Microsoft.StreamAnalytics/streamingjobs",  
         "location":"Central US",  
         "properties":{    
            "sku":{    
               "name":"Standard"  
            },  
            "jobId":"26688533-29cb-4706-b411-5c7e4bfcd0cb",  
            "provisioningState":"Succeeded",  
            "jobState":"Created",  
            "createdDate":"2014-10-08T23:03:59.737",  
            "etag":"6a7bdc17-1c24-403a-aa60-076274ef7f2f"  
         }  
      },  
      {    
         "id":"/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/Default-SA-CentralUS/providers/Microsoft.StreamAnalytics/streamingjobs/sample2",  
         "name":"sample2",  
         "type":"Microsoft.StreamAnalytics/streamingjobs",  
         "location":"Central US",  
         "properties":{    
            "sku":{    
               "name":"Standard"  
            },  
            "jobId":"1f5f1618-c14d-40fe-8d52-f5700ac9d3d7",  
            "provisioningState":"Succeeded",  
            "jobState":"Created",  
            "createdDate":"2014-10-09T04:43:27.96",  
            "etag":"6912b24a-aa95-4114-9149-8dc884f2fce2"  
         }  
      }  
   ],  
   "nextLink":  
}  
  
```  
  
  
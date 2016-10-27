---
title: "List Inputs (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 14589d3e-e03f-40f8-b7f1-6932a82a8de8
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
# List Inputs (Azure Stream Analytics)
  Lists all of the inputs that are defined in a Stream Analytics job.  
  
## Request  
 The **List Inputs** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**GET**|https://managment.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs/{job-name}/inputs&api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name of the Stream Analytics job.  
  
 Replace {api-version} with 2015-10-01-preview in the URI.  
  
## Response  
 Status code: 200  
  
 **JSON**  
  
 The example below shows a response from a List Inputs request for an Stream Analytics job with one Azure Blob Storage input.  
  
```  
  
{    
   "value":[    
      {    
         "id":"/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/Default-SA-CentralUS/providers/Microsoft.StreamAnalytics/streamingjobs/myStreamingSample/inputs/inputSample2",  
         "name":"inputSample2",  
         "type":"Microsoft.StreamAnalytics/streamingjobs/inputs",  
         "properties":{    
            "type":"Reference",  
            "datasource":{    
               "type":"Microsoft.Storage/Blob",  
               "properties":{    
                  "blobName":"$Default/0",  
                  "storageAccounts":[    
                     {    
                        "accountName":"samplestorage"  
                     }  
                  ],  
                  "container":"samplecontainer"  
               }  
            },  
            "serialization":{    
               "type":"Csv",  
               "properties":{    
                  "fieldDelimiter":",",  
                  "encoding":"UTF8"  
               }  
            },  
            "etag":"54eae50b-9ff2-4285-a727-773f55f5deac"  
         }  
      }  
   ],  
   "nextLink":  
}  
  
```  
  
  
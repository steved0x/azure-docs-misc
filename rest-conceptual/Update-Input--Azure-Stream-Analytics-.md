---
title: "Update Input (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: edc46259-6240-42ac-be34-584ee5ce0f8e
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
# Update Input (Azure Stream Analytics)
  Updates the properties that are assigned to an input.  
  
## Request  
 The **Update Input** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**PATCH**|https://managment.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs/{job-name}/inputs/{input-name}?api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name of the Stream Analytics job that you are updating.  
  
 Replace {input-name} with the name of the input that you are updating.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
 **JSON**  
  
```  
  
{    
   "properties":{    
      "type":"reference",  
      "serialization":{    
         "type":"JSON",  
         "properties":{    
            "encoding":"UTF8"  
         }  
      }  
   }  
}  
  
```  
  
 Any one or more of the input properties may be specified in the request body, setting/replacing any existing value for each property specified.  
  
 For more information about input properties, see [Create Input &#40;Azure Stream Analytics&#41;](../rest-conceptual/Create-Input--Azure-Stream-Analytics-.md).  
  
## Response  
 Status code: 201  
  
 **JSON**  
  
```  
  
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
         "type":"Json",  
         "properties":{    
            "encoding":"UTF8"  
         }  
      }  
   }  
}  
  
```  
  
 The response body contains the updated input resource. Any secrets in the **PATCH** response body are redacted.  
  
  
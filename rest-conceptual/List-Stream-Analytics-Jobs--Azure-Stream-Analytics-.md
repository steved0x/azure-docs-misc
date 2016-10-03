---
title: "List Stream Analytics Jobs (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 8b1c0b2f-b1a1-4da4-8d44-9e3b32e035bf
caps.latest.revision: 21
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
# List Stream Analytics Jobs (Azure Stream Analytics)
  Lists all of the Stream Analytics jobs that are defined in a subscription.  
  
## Request  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**GET**|https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.StreamAnalytics/streamingjobs?$expand={properties-to-expand}&api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
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
            "eventsLateArrivalMaxDelayInSeconds":-1,  
            "createdDate":"2014-10-08T23:03:59.737",  
            "etag":"6a7bdc17-1c24-403a-aa60-076274ef7f2f"  
         }  
      },  
      {    
         "id":"/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/New-SA-CentralUS/providers/Microsoft.StreamAnalytics/streamingjobs/sample3",  
         "name":"sample3",  
         "type":"Microsoft.StreamAnalytics/streamingjobs",  
         "location":"Central US",  
         "properties":{    
            "sku":{    
               "name":"Standard"  
            },  
            "jobId":"259ccfa8-76ec-4662-9568-8752787f737d",  
            "provisioningState":"Succeeded",  
            "jobState":"Created",            "createdDate":"2014-10-08T21:56:57.583",  
            "etag":"c815791e-5d50-4b85-b3f0-c78acec5dd41"  
         }  
      }  
   ],  
   "nextLink":  
}  
```  
  
  
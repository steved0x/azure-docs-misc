---
title: "Get Information about a Stream Analytics Job (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 19e5f349-bebd-4610-af34-35464b76a771
caps.latest.revision: 27
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
# Get Information about a Stream Analytics Job (Azure Stream Analytics)
  Gets information about a specific Stream Analytics job.  
  
## Request  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**GET**|https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs/{job-name}?$expand={properties-to-expand}&api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name of the Stream Analytics job that you want information about.  
  
 The request will support the $expand query option. The endpoint will by default exclude the Inputs, Transformation, Outputs, and  Functions properties if the request does not have the $expand query parameter. Specifying the query parameter ($expand=Inputs,Transformation,Outputs,Functions) will return those properties.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
## Response  
 Status code: 200  
  
 Example with $expand=inputs,transformation,outputs,functions  
  
 **JSON**  
  
```  
{    
   "id":"/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/Default-SA-CentralUS/providers/Microsoft.StreamAnalytics/streamingjobs/myStreamingSample",  
   "name":"myStreamingSample",  
   "type":"Microsoft.StreamAnalytics/streamingjobs",  
   "location":"Central US",  
   "properties":{    
      "sku":{    
         "name":"Standard"  
      },  
      "jobId":"e4563ba8-0ab7-4bff-8528-61893c526797",  
      "provisioningState":"Succeeded",  
      "jobState":"Created",  
      "outputStartTime":"2014-07-03T01:00:00",  
      "lastOutputEventTime": "2014-07-05T03:00Z",   
      "outputStartMode":"CustomTime",  
      "eventsOutOfOrderPolicy":"Drop",  
      "eventsOutOfOrderMaxDelayInSeconds":10,  
      "eventsLateArrivalMaxDelayInSeconds":-1,  
      "dataLocale":"en-US",,  
      "createdDate":"2014-10-10T03:36:13.95",  
      "inputs":[    
         {    
            "id":"/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/Default-SA-CentralUS/providers/Microsoft.StreamAnalytics/streamingjobs/myStreamingSample/inputs/MyBlobSource",  
            "name":"MyBlobSource",  
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
               "etag":"0f18d8d3-66b7-44c6-be12-a5814e7260bb"  
            }  
         },  
         {    
            "id":"/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/Default-SA-CentralUS/providers/Microsoft.StreamAnalytics/streamingjobs/myStreamingSample/inputs/MyEventHubSource",  
            "name":"MyEventHubSource",  
            "type":"Microsoft.StreamAnalytics/streamingjobs/inputs",  
            "properties":{    
               "type":"Stream",  
               "datasource":{    
                  "type":"Microsoft.ServiceBus/EventHub",  
                  "properties":{    
                     "serviceBusNamespace":"sampleServiceBus",  
                     "sharedAccessPolicyName":"SampleReceiver",  
                     "eventHubName":"sampleEventHub"  
                  }  
               },  
               "serialization":{    
                  "type":"Json",  
                  "properties":{    
                     "encoding":"UTF8"  
                  }  
               },  
               "etag":"21f7092b-a5b6-4599-8b6c-3d710a68293f"  
            }  
         }  
      ],  
      "transformation":{    
         "id":"/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/Default-SA-CentralUS/providers/Microsoft.StreamAnalytics/streamingjobs/myStreamingSample/transformations/ProcessSampleData",  
         "name":"ProcessSampleData",  
         "type":"Microsoft.StreamAnalytics/streamingjobs/transformations",  
         "properties":{    
            "streamingUnits":1,  
            "script":null,  
            "query":"select * from MyEventHubSource",  
            "etag":"ab035edc-6d3b-41f7-902e-1e3124307981"  
         }  
      },  
      "outputs":[    
         {    
            "id":"/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/Default-SA-CentralUS/providers/Microsoft.StreamAnalytics/streamingjobs/myStreamingSample/outputs/output",  
            "name":"output",  
            "type":"Microsoft.StreamAnalytics/streamingjobs/outputs",  
            "properties":{    
               "etag":"18303c87-a8dd-496c-9fb7-c9028da9a3fc",  
               "datasource":{    
                  "type":"Microsoft.Sql/Server/Database",  
                  "properties":{    
                     "server":"sampleserver.database.windows.net",  
                     "database":"sampleDB",  
                     "table":"sampleTable",  
                     "user":"user@sampleserver"  
                  }  
               }  
            }  
         }  
      ],  
    "functions": [  
      {  
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/Default-SA-CentralUS/providers/microsoft.streamAnalytics/streamingjobs/filterSample/functions/ScoreAlert",  
        "name": "ScoreAlert",  
        "type": "Microsoft.StreamAnalytics/streamingjobs/functions",  
        "properties": {  
          "etag": "F86B9B70-D5B1-451D-AFC8-0B42D4729B8C",  
          "type": "Microsoft.MachineLearning/WebService",  
          "properties": {  
            "endpoint": "https://ussouthcentral.services.azureml.net/odata/workspaces/c32528db4ede4300bb70e0c6da66ef5a/services/a2449cb837c042aa8146dbec41c9ee67",  
          }  
        }  
      }  
    ]  
  }  
}  
```  
  
> [!NOTE]  
>  The response includes $expand=Inputs,Transformation,Outputs,Functions  
  
  
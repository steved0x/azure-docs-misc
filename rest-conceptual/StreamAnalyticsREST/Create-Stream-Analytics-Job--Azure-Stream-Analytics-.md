---
title: "Create Stream Analytics Job (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-05-20
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 13beb8e4-f561-4435-bd04-998e695b53c2
caps.latest.revision: 37
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
# Create Stream Analytics Job (Azure Stream Analytics)
  Creates a new Stream Analytics job in Microsoft Azure. For more information about Stream Analytics and how you can use it, see [What is Azure Stream Analytics](http://go.microsoft.com/fwlink/?LinkId=517303).  
  
 Before you can run this operation, you must create an Azure subscription and obtain the subscription identifier. You can obtain the subscription identifier on the **Settings** page of the Azure classic portal.  
  
## Request  
 The **Create Stream Analytics Job** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**PUT**|https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs/{job-name}?api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name that you want to assign to the Stream Analytics job that you are creating. The job name is case insensitive and must be unique among all inputs in the job, containing only numbers, letters, and hyphens. It must be 3 to 63 characters long.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
 **JSON**  
  
```  
  
{    
   "location":"Central US",  
   "properties":{    
      "sku":{    
         "name":"standard"  
      },  
      "eventsOutOfOrderPolicy":"drop",  
      "eventsOutOfOrderMaxDelayInSeconds":10,  
      "inputs":[    
         {    
            "name":"MyEventHubSource",  
            "properties":{    
               "type":"stream",  
               "serialization":{    
                  "type":"JSON",  
                  "properties":{    
                     "encoding":"UTF8"  
                  }  
               },  
               "datasource":{    
                  "type":"Microsoft.ServiceBus/EventHub",  
                  "properties":{    
                     "serviceBusNamespace":"sampleServiceBus",  
                     "sharedAccessPolicyName":"SampleReceiver",  
                     "sharedAccessPolicyKey":"***/**********/******************************",  
                     "eventHubName":"sampleEventHub"  
                  }  
               }  
            }  
         },  
         {    
            "name":"MyBlobSource",  
            "properties":{    
               "type":"reference",  
               "serialization":{    
                  "type":"CSV",  
                  "properties":{    
                     "fieldDelimiter":",",  
                     "encoding":"UTF8"  
                  }  
               },  
               "datasource":{    
                  "type":"Microsoft.Storage/Blob",  
                  "properties":{    
                     "storageAccounts":[    
                        {    
                           "accountName":"samplestorage",  
                           "accountKey":"*****************************************************************************"  
                        }  
                     ],  
                     "container":"samplecontainer",  
                     "blobName":"$Default/0"  
                  }  
               }  
            }  
         }  
      ],  
      "transformation":{    
         "name":"ProcessSampleData",  
         "properties":{    
            "streamingUnits":1,  
            "query":"select * from MyEventHubSource"  
         }  
      },  
      "outputs":[    
         {    
            "name":"output",  
            "properties":{    
               "datasource":{    
                  "type":"Microsoft.Sql/Server/Database",  
                  "properties":{    
                     "server":"sampleserver.database.windows.net",  
                     "database":"sampleDB",  
                     "table":"sampleTable",  
                     "user":"user@sampleserver",  
                     "password":"****************"  
                  }  
               }  
            }  
         }  
      ]  
   }  
}  
  
```  
  
|Element name|Required|Notes|  
|------------------|--------------|-----------|  
|**location**|Yes|The value of **location** must be a supported Azure Stream Analytics location. For more information, see [List all of the available geo-locations](http://msdn.microsoft.com/library/azure/dn790540.aspx).|  
|**tags**|No|This element contains a collection of one or more name/value pairs that describe a tag. The value can be null for a tag.|  
|**sku**|Yes|This element specifies the SKU being purchased for this Stream Analytics job. For the preview release, the value of the name property in **sku** must be Standard.|  
|**eventsOutOfOrderPolicy**|No|Events that arrive within the time window specified for **eventsOutOfOrderMaxDelayInSeconds** will be reordered automatically. Events that arrive outside the delay window will be dropped or adjusted based on the value selected. Values supported: Adjust, Drop.|  
|**eventsOutOfOrderMaxDelayInSeconds**|No|This element specifies the time window (in seconds) within which events should be automatically reordered. The delay specified will directly affect the job latency.|  
|**outputStartMode**|No|This property should only be utilized when it is desired that the job be started immediately upon creation.<br /><br /> Value may be JobStartTime, CustomTime, or LastOutputEventTime to indicate whether the starting point of the output event stream should either start whenever the job is started, start at a custom user time stamp specified via the **outputStartTime** property, or start from the last event output time. The **outputStartMode** property can be set to LastOutputEventTime only when **GetStreamingJobResponse** from the **GetStreamingJob** request has LastOutputEventTime set, meaning there was at least one output event generated from the streaming job previously.<br /><br /> **Note:** If this property is specified the job will automatically start when the service creates it. Therefore a full job definition (at a minimum the required job properties and fully specified inputs, outputs, and transformation) needs to be specified in the PUT request.|  
|**outputStartTime**|No|Value is either an ISO-8601 formatted time stamp that indicates the starting point of the output event stream, or null to indicate that the output event stream will start whenever the streaming job is started. This property *must* have a value if **outputStartMode** is set to CustomTime. <br /><br />If a non-null value is specified, the job will begin streaming data from the input source (data stream) from that time to ensure it produces the correct output.  It is also possible the job will need to begin streaming data at a point in time preceding the value given for **outputStartTime**, (if your query requires it).  For example, if your job query is computing some aggregate within an hourly time window and you specify an **outputStartTime** of ‘2016-05-18 12:00’, then the job will begin at streaming the data that corresponds to an 11:00 AM timestamp. <br /><br />**Note**: If you specify a custom time which is before 'when last stopped', the job will reprocess data it has already processed. Depending on your query, this could result in duplicates in your output stream(s).<br /><br />**Additionally**, when starting a job with a custom time, Stream Analytics will compare the value you give for **outputStartTime** against either (a) the datetime field specified in your query’s **TIMESTAMP BY** clause; or (b) the default timestamp field for a given input source type, e.g. **‘EventEnqueuedUtcTime’** for IoT Hub and Event Hub sources.|  
|**dataLocale**|No|This element identifies the specific country/region associated with the data processed by a streaming job. The value determines the formats used with dates and other types.<br /><br /> For example, with a **dataLocale** value of fr-FR, the date “10/11/2015” is interpreted as Tuesday, November 10, 2015.<br /><br /> The value is an Internet Engineering Task Force (IETF) language tag that names a [specific culture](https://msdn.microsoft.com/library/system.globalization.cultureinfo.createspecificculture(v=vs.110).aspx) supported by Microsoft .NET. The default value is en-US.|  
|**inputs**|No|This element specifies an array of one or more inputs to the streaming job. An input is a stream-processing component that feeds a job with streaming or reference input data from a resource that is outside Stream Analytics; for example, Azure Blob storage or Azure Service Bus Event Hub. Each Job requires at least one streaming input, and may contain one or more reference data inputs.|  
|**transformation**|No|A transformation is a stream-processing component that performs a query on one or more incoming streams. A transformation is described by a transformation query in the JSON body of the resource. Each job may have only one transformation.|  
|**outputs**|No|This element specifies an array of one or more outputs to the streaming job. An output is a stream-processing component that pushes the output of a streaming job to a resource that is outside Stream Analytics; for example, Azure Blob storage, SQL Database, or Azure Service Bus Event Hub.|  
  
## Response  
 Status code: 201 or 200  
  
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
      "outputStartTime":"2014-07-03T01:00:00Z",  
      "outputStartMode":"CustomTime",  
      "eventsOutOfOrderPolicy":"Drop",  
      "eventsOutOfOrderMaxDelayInSeconds":10,  
      "eventsLateArrivalMaxDelayInSeconds":-1,  
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
               "datasource":{    
                  "type":"Microsoft.Sql/Server/Database",  
                  "properties":{    
                     "server":"sampleserver",  
                     "database":"sampleDB",  
                     "table":"sampleTable",  
                     "user":"user@sampleserver"  
                  }  
               },  
               "etag":"18303c87-a8dd-496c-9fb7-c9028da9a3fc"  
            }  
         }  
      ]  
   }  
}  
  
```  
  
> [!NOTE]  
>  For security reasons, secrets and passwords are not returned in the response.  
  
|Element name|Notes|  
|------------------|-----------|  
|**id**|This element specifies a URI that refers directly to the Stream Analytics job just created.|  
|**location**|Region in which to create the streaming job|  
|**tags**|This element is not returned if tags were not included in the request.|  
|**jobId**|This is a read-only property, set by the service when the streaming job is created. It is returned in **PUT** and **GET** response bodies.|  
|**provisioningState**|The provisioningSate field has three terminal states: **Succeeded**, **Failed** and **Canceled**. If the resource returns no provisioningState, it is assumed to be **Succeeded**.|  
|**jobState**|Indicates the current execution state of the streaming job. Client can use start/stop resource actions (POST) to change the state.|  
|**outputStartMode**|Specifies if the job should start producing output at a given timestamp or at the point when the job starts. Value may be JobStartTime, CustomTime, or LastOutputEventTime|  
|**OutputStartTime**|The earliest timestamp of events from inputs that this job processes. This is not a start time for the job itself.|  
|**eventsOutOfOrderPolicy**|Police on what to do for events arriving out of order.|  
|**eventsOutOfOrderMaxDelayInSeconds**|Value in seconds|  
|**eventsLateArrivalMaxDelayInSeconds**|Value in seconds|  
|**createdDate**|The value is an ISO-8601 formatted Coordinated Universal Time (UTC) time stamp that indicates when the streaming job was created.|  
|**Inputs**|A list of one or more inputs.|  
|**Transformation**|Returns the value of the current transformation component of the stream job.|  
|**Outputs**|A list of one or more outputs.|  
|**dataLocale**|This element identifies the specific country/region associated with the data processed by a streaming job. The value determines the formats used with dates and other types.<br /><br /> For example, with a **dataLocale** value of fr-FR, the date “10/11/2015” is interpreted as Tuesday, November 10, 2015.<br /><br /> The value is an IETF language tag that names a [specific culture](https://msdn.microsoft.com/library/system.globalization.cultureinfo.createspecificculture(v=vs.110).aspx) supported by .NET. The default value is en-US.|  
  
  
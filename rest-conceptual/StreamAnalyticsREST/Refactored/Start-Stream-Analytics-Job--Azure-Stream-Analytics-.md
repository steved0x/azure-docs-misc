---
title: "Start Stream Analytics Job (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-05-20
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: d5c03dd5-f9f1-46bd-86e6-2c5b6be189ca
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
# Start Stream Analytics Job (Azure Stream Analytics)
  Deploys and starts a Stream Analytics job in Microsoft Azure.  
  
## Request  
 The **Start Stream Analytics Job** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**POST**|https://managment.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs/{job-name}/start?api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/en-us/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name of the Stream Analytics job that you are starting.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
 **JSON**  
  
```  
{  
    "outputStartMode" : "JobStartTime | CustomTime | LastOutputEventTime",  
    "outputStartTime": "2014-07-03T01:00Z",  
}  
  
```  
  
|Element name|Required|Notes|  
|------------------|--------------|-----------|  
|**outputStartMode**|No|Value may be JobStartTime, CustomTime, or LastOutputEventTime to indicate whether the starting point of the output event stream should either start whenever the job is started, start at a custom user time stamp specified via the **outputStartTime** property, or start from the last event output time. If the property is absent, the default is JobStartTime. The **outputStartMode**property can be set to LastOutputEventTime only when **GetStreamingJobResponse** from the **GetStreamingJob** request has LastOutputEventTime set, meaning there was at least one output event generated from the streaming job previously.|  
|**outputStartTime**|No|Value is either an ISO-8601 formatted time stamp that indicates the starting point of the output event stream, or null to indicate that the output event stream will start whenever the streaming job is started. This property *must* have a value if **outputStartMode** is set to CustomTime. <br /><br />If a non-null value is specified, the job will begin streaming data from the input source (data stream) from that time to ensure it produces the correct output.  It is also possible the job will need to begin streaming data at a point in time preceding the value given for **outputStartTime**, (if your query requires it).  For example, if your job query is computing some aggregate within an hourly time window and you specify an **outputStartTime** of ‘2016-05-18 12:00’, then the job will begin at streaming the data that corresponds to an 11:00 AM timestamp. <br /><br />**Note**: If you specify a custom time which is before 'when last stopped', the job will reprocess data it has already processed. Depending on your query, this could result in duplicates in your output stream(s).<br /><br />**Additionally**, when starting a job with a custom time, Stream Analytics will compare the value you give for **outputStartTime** against either (a) the datetime field specified in your query’s **TIMESTAMP BY** clause; or (b) the default timestamp field for a given input source type, e.g. **‘EventEnqueuedUtcTime’** for IoT Hub and Event Hub sources.|  
  
## Response  
 Status code: 202  
  
 This is an asynchronous operation that returns a status of 202 until the job has successfully started. The **Location** response header contains the URI that is used to obtain the status of the process. While the process is running, a call to the URI in the **Location** header returns a status of 202. When the process finishes, the URI in the **Location** header returns a status of 200. To get a more detailed status of the job progress, use the **Get Information about a Stream Analytics Job** operation. The job response returned will include a **jobState** property.  
  
  
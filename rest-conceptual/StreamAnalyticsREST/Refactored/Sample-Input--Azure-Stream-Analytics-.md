---
title: "Sample Input (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: f1a9c086-b93b-4f72-9a6f-85fb1053ebbf
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
# Sample Input (Azure Stream Analytics)
  ASA service will attempt to get sample events for a limited time, if there are no events in the source when it queries it would not wait, it would return zero events. ASA service will only spend a fixed amount of time to get sample events, it would return as many events as it could read within the limited time. Please note that this is a sample set of events, the order the events are received in the sample and the order the events are processed can be different.  
  
## Request  
  
|Method|Request URI|  
|------------|-----------------|  
|**Post**|https://<endpoint\>/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/inputs/{inputName}/sample?api-version={api-version}|  
  
 Replace {jobName} with the name of the job.  
  
 Replace {inputName} with the name of the input  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
 **JSON**  
  
```  
{  
  “eventStartTime”: “2015-03-01 10:00”,  
  “eventEndTime”: “2015-03-01 10:01”  
  “numberOfEvents”: 10  
  “serialization”:  
        {  
          “type”: “Json”  
        }  
  
}  
  
```  
  
|Element name|Required|Description|  
|------------------|--------------|-----------------|  
|eventStartTime|Yes|Time from which to get sample events.|  
|eventEndTime|Yes|Time up to which sample events should be obtained|  
|numberOfEvents|No|Number of events to sample. Between 1 to 1000.|  
|serialization|Yes|Serialization format in which to receive the events. Only CSV and JSON types are supported.|  
  
## Response  
  
### Status Code  
  
-   202 (Accepted) if request was accepted to complete asynchronously.  
  
-   404 (Not Found) if the job or input is not found  
  
-   400 (Bad Request) if sample request parameters are invalid.  
  
-   5xx if ASA service is unable to get sample input at all due to service issues  
  
### Response Body  
 None from the POST operation itself. Clients should use the Asynchronous Operations pattern to get the results of the test. Results are returned as Input Sample Operation Results.  
  
## Input Sample Operation Results  
 Results from input sample are returned as operation result. It has the following structure  
  
```  
{  
      "error" : { /* OData V4 error response structure */  
        "code": "BadArgument",  
        "message": "Customer-facing error detail."   
       }  
  
     “eventsDownloadUrl”: “url from which events can be downloaded”  
}  
  
```  
  
|Element name|Description|  
|------------------|-----------------|  
|eventsDownloadUrl|The URL from which events can be downloaded. The download will only be available for up to 15 minutes.|  
  
### Status  
  
-   NoEventsFoundInRange – There were no events in the range mentioned when the service queried the input source.  
  
-   ReadAllEventsInRange – A sample of events in the range specified were read and is available in eventsDownloadUrl. This may not be the complete set of events in the range specified, it is a sample.  
  
-   ErrorConnectingToInput – ASA couldn’t connect to the datasource successfully. Reason will be available in “error” field  
  
### Code  
 A value from the .NET HttpStatusCode enumeration, formatted as a string.  
  
### Message  
 A customer-visible, localized error message that further details the reason for the test failure.  
  
  
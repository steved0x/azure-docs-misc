---
title: "Update Stream Analytics Job (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: a183f82a-79b2-4e6d-b134-df8a939f2ec6
caps.latest.revision: 24
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
# Update Stream Analytics Job (Azure Stream Analytics)
  Updates the properties that are assigned to a Stream Analytics job.  
  
## Request  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**PATCH**|https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs/{job-name}?api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name of the Stream Analytics job that you are updating.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
 **JSON**  
  
```  
{  
  "properties": {  
    "eventsOutOfOrderMaxDelayInSeconds": 10  
  }  
}  
  
```  
  
 Any one or more of the streaming-job properties, exclusive of inputs, outputs, and transformations, may be specified in the request body, setting/replacing any existing value for each property specified. Inputs, outputs, and transformations must be patched directly via the Input, Output, and Transformation REST APIs.  
  
|Element name|Required|Notes|  
|------------------|--------------|-----------|  
|**tags**|No|This element contains a collection of one or more name/value pairs that describe a tag. The value can be null for a tag.|  
|**sku**|Yes|This element specifies the SKU being purchased for this Stream Analytics job. For the preview release, the value of **sku** must be Standard.|  
|**eventsOutOfOrderPolicy**|No|Events that arrive within the time window specified for **eventsOutOfOrderMaxDelayInSeconds** will be reordered automatically. Events that arrive outside the delay window will be dropped or adjusted based on the value selected. Values supported: Adjust, Drop.|  
|**eventsOutOfOrderMaxDelayInSeconds**|No|This element specifies the time window (in seconds) within which events should be automatically reordered. The delay specified will directly affect the job latency.|  
|**dataLocale**|No|This element identifies the specific country/region associated with the data processed by a streaming job. The value determines the formats used with dates and other types.<br /><br /> For example, with a **dataLocale** value of fr-FR, the date “10/11/2015” is interpreted as Tuesday, November 10, 2015.<br /><br /> The value is an Internet Engineering Task Force (IETF) language tag that names a [specific culture](https://msdn.microsoft.com/library/system.globalization.cultureinfo.createspecificculture(v=vs.110).aspx) supported by Microsoft .NET. The default value is en-US.|  
  
## Response  
 Status code: 201  
  
 **JSON**  
  
```  
  
{  
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/Defa  
ult-SA-CentralUS/providers/Microsoft.StreamAnalytics/streamingjobs/myStreamingSample"  
,  
  "name": "myStreamingSample",  
  "type": "Microsoft.StreamAnalytics/streamingjobs",  
  "location": "Central US",  
  "tags": {  
    "key1": "value1",  
    "key2": "value2"  
  },  
  "properties": {  
    "sku": {  
      "name": "Standard"  
    },  
    "jobId": "8f4ebd73-0696-4aa3-bddb-51254f76cf70",  
    "provisioningState": "Succeeded",  
    "jobState": "Created",  
    "outputStartTime": "2014-07-03T01:00:00",  
    "lastOutputEventTime": "2014-07-05T03:00Z",   
    "outputStartMode": "CustomTime",  
    "eventsLateArrivalMaxDelayInSeconds":-1,  
    "createdDate": "2014-10-10T03:16:50.567"  
  }  
}  
  
```  
  
 The response body contains the updated resource. For security purposes, the response does not include any secrets or passwords.  
  
  
---
title: "Create Input (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-07-13
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 4ee654f5-09a3-4583-a868-13be99694d7f
caps.latest.revision: 30
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
# Create Input (Azure Stream Analytics)
  Creates a new input within a Stream Analytics job.  
  
## Request  
 The **Create Input** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**PUT**|https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs/{job-name}/inputs/{input-name}?api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name of the Stream Analytics job that you are stopping.  
  
 Replace {input-name} with the name (or alias) that you want to assign to the input that you are creating. The input name is case insensitive and must be unique among all inputs in the job, containing only numbers, letters, and hyphens. It must be 3 to 63 characters long.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
 **JSON**  
  
```  
  
{    
   "properties":{    
      "type":"stream",  
      "serialization":{    
         "type":"CSV",  
         "properties":{    
            "fieldDelimiter":",",  
            "encoding":"UTF8"  
         }  
      },  
      "datasource":{    
         "type":"Microsoft.ServiceBus/EventHub",  
         "properties":{    
            "serviceBusNamespace":"sampleServiceBus",  
            "sharedAccessPolicyName":"SampleReceiver",  
            "sharedAccessPolicyKey":"***/**********/*****************************",  
            "eventHubName":"sampleEventHub"  
         }  
      }  
   }  
}  
  
```  
  
|Element name|Required|Notes|  
|------------------|--------------|-----------|  
|**type**|Yes|Indicates whether the input is a source of type reference data or stream data. After an input is created, its type cannot be changed (PUT or PATCH). You must delete the input and create a new one.|  
|**serialization**|Yes|Describes how data from this input is serialized. Allowed **serialization** type values are specific to the type of serialization used.|  
|**datasource**|Yes|Indicates the type of data source that incoming data will be read from. Allowed **datasource** type values are specific to the type of data source used.|  
  
 **Serialization**  
  
|Element name|Required|Notes|  
|------------------|--------------|-----------|  
|**type**|Yes|This element is associated with the **serialization** element. It indicates the type of serialization that the input uses. Supported values for stream data include: CSV, JSON, and Avro. Supported values for reference data include: CSV.<br><br> Note that CSV formatted data requires a header row where all header column names are unique. |  
|**fieldDelimiter**|For CSV|This element is associated with the **serialization** element and is required when the **serialization** type is CSV. <br />It specifies the delimiter that will be used to separate comma-separated value (CSV) records. Supported values include:<br /><br /> -   Space<br />-   Comma<br />-   Tab<br />-   ‘&#124;’<br />-   Semi-colon|  
|**Encoding**|For CSV and JSON|This element is associated with the **serialization** element and is required when the **serialization** type is CSV or JSON. It specifies the encoding of the incoming data. Supported values include: UTF8.|  
  
 **Data Source - Blob**  
  
|Element name|Required|Notes|  
|------------------|--------------|-----------|  
|**type**|Yes|This element is associated with the **datasource** element. It indicates the type of data source that incoming data will be read from. For Blob, the value should be Microsoft.Storage/Blob.|  
|**storageAccounts**|Yes|This element is associated with the **datasource** element. It provides a list of one or more Storage accounts to be used to read incoming data from.|  
|**accountName**|Yes|This element is associated with the **storageAccounts** element. It indicates the name of the Storage account.|  
|**accountKey**|Yes|This element is associated with the **storageAccounts** element. It indicates the key for the Storage account. This property is not returned on **GET** requests.|  
|**container**|Yes|This element is associated with the **storageAccounts** element. It indicates the name of the container, within the associated Storage account, in which the input data is stored.|  
|**pathPattern**|No|This element is associated with the **storageAccounts** element. It represents a pattern against which blob names will be matched to determine whether or not they should be included as input to the job. Characters are tokenized 1:1, except for the following:<br /><br /> -   {date}<br />-   {time}<br />-   {partitionCount}<br /><br /> Example: “/segment1/{date}/segment2/{time}” **Note:**  The character "*" is not an allowed value for pathprefix. Only valid [Azure blob characters](../rest-conceptual/Naming-and-Referencing-Containers--Blobs--and-Metadata.md) are allowed.|  
|**dateFormat**|No|This element is associated with the **storageAccounts** element. It is present only when {date} is used in **pathPattern**. The value is an ISO-8601 format string. Wherever {date} appears in **pathPattern**, the value of this property is used as the date format instead.<br /><br /> Example: With **dateFormat** = “yyyy/MM/dd” and **pathPattern** = “/segment1/{date}/segment2”, the resulting pattern would match a prefix like “/segment1/2014/09/25/segment2/…”|  
|**timeFormat**|No|This element is associated with the **storageAccounts** element. It is present only when {time} is present in **pathPattern**. The value is an ISO-8601 format string. Wherever {time} appears in **pathPattern**, the value of this property is used as the time format instead.<br /><br /> Example: With **timeFormat** = “HH:mm” and **pathPattern** = “/segment1/{time}/segment2”, the resulting pattern would match a prefix like  “/segment1/23:10/segment2/…”|  
|**sourcePartitionCount**|No|This element is associated with the **storageAccounts** element. It is present only when {partition} is present in **pathPattern**. The value of this property is an integer >=1. Wherever {partition} appears in **pathPattern**, a number between 0 and the value of this field -1 will be used.|  
|**blobName**|No|This element is associated with the **datasource** element and is required for inputs of type Reference Data. This property is not used for inputs of type Stream Data. It indicates the name of the single blob that holds the reference data for this input.|  
  
 **Data Source – Event Hub**  
  
|Element name|Required|Notes|  
|------------------|--------------|-----------|  
|**type**|Yes|This element is associated with the **datasource** element. It indicates the type of data source that incoming data will be read from. For an event hub, the value should be Microsoft.ServiceBus/EventHub.|  
|**serviceBusNamespace**|Yes|This element is associated with the **datasource** element for type Microsoft.ServiceBus/EventHub. This is the Service Bus namespace that was created during creation of your event-hub instance.|  
|**sharedAccessPolicyName**|Yes|This element is associated with the **datasource** element for type Microsoft.ServiceBus/EventHub. This is the shared access policy name for the event hub that you are connecting to. This and the shared access key can be created on the **Configure** tab of Event Hubs in the Azure classic portal.|  
|**sharedAccessPolicyKey**|Yes|This element is associated with the **datasource** element for type Microsoft.ServiceBus/EventHub. This is the shared access key for the policy. This property is not returned on **GET** requests.|  
|**eventHubName**|Yes|This element is associated with the **datasource** element for type Microsoft.ServiceBus/EventHub. This is the name of your event-hub instance.|  
|**consumerGroupName**|No|This element is associated with the **datasource** element. This is the name of an event-hub consumer group by which to identify this input. Specifying distinct consumer-group names for multiple inputs allows each of those inputs to receive the same events from the event hub. If the name is not specified, the input uses the event hub’s default consumer group.|  
  
 **Data Source – Iot Hub**  
  
|Element name|Required|Notes|  
|------------------|--------------|-----------|  
|**type**|Yes|This element is associated with the **datasource** element. It indicates the type of data source that incoming data will be read from. For Iot Hub, the value should be Microsoft.Devices/IotHubs.|  
|**iotHubNamespace**|Yes|The name or the URI of the IoT Hub|  
|**sharedAccessPolicyName**|Yes|The shared access policy name for the target Iot Hub with Service connect permission.|  
|**sharedAccessPolicyKey**|Yes|The shared access policy key for the target Iot Hub.|  
|**consumerGroupName**|No|Name of an Iot Hub consumer group by which to identify this input. If not specified, the input uses the Iot Hub’s default consumer group.|  
  
## Response  
 Status code: 201  
  
 **JSON**  
  
```  
  
{    
   "id":"/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/Default-SA-CentralUS/providers/Microsoft.StreamAnalytics/streamingjobs/myStreamingSample/inputs/sampleInput",  
   "name":"sampleInput",  
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
      }  
   }  
}  
  
```  
  
  
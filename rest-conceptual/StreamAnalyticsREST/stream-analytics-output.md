# Output

## Create
Creates a new output within a Stream Analytics job.  
  
### Request  
 The **Create Output** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**PUT**|https://managment.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs/{job-name}/outputs/output?api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name of the Stream Analytics job.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
### JSON
  
```  
  
{    
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
```  
  
|Element name|Required|Notes|  
|------------------|--------------|-----------|  
|**datasource**|Yes|This element indicates the type of data source that data will be written to. Allowed **datasource** type values are specific to the type of data source used.|  
|**serialization**|Yes|This element is required when the **datasource** type is Blob or EventHub. It is not required for other sources. It describes how data from this output is serialized. Allowed **serialization** type values are specific to the type of serialization used.|  
  
### Serialization 
  
|Element name|Required|Notes|  
|------------------|--------------|-----------|  
|**type**|Yes|This element is associated with the **serialization** element. It indicates the type of serialization that the output uses. Supported values include: CSV, JSON, and Avro.|  
|**fieldDelimiter**|For CSV|This element is associated with the **serialization** element and is required when the **serialization** type is CSV. <br />It specifies the delimiter that will be used to separate comma-separated value (CSV) records. Supported values include:<br /><br /> -   Space<br />-   Comma<br />-   Tab<br />-   ‘&#124;’<br />-   Semi-colon|  
|**encoding**|For CSV and JSON|This element is associated with the **serialization** element and is required when the **serialization** type is CSV or JSON. It specifies the encoding of the data.|  
|**format**|Optional for JSON|This element is associated with the **serialization** element and is optional when the **serialization** type is JSON. It is a string and supports the following values:<br /><br /> -   lineSeparated<br />     - Specifies that the output will be formatted by having each JSON object separated by a new line<br />-   array<br />     - Specifies that the output will be formatted as an array of JSON objects.<br /><br /> Default value is lineSeparated.|  

###  Data sources
 
 Note that *PowerBI* and *Azure Data Lake Stores* are not able to be created using **CREATE OUTPUT** due to an authorization requirement to attach to these services.
 
PowerBI authorization is discussed in the [Power BI Dashboard article](https://azure.microsoft.com/en-us/documentation/articles/stream-analytics-power-bi-dashboard/#add-power-bi-output).

Azure Data Lake Stores are discussed in the [Azure Data Lake output article](https://azure.microsoft.com/en-us/documentation/articles/stream-analytics-data-lake-output/#renew-data-lake-store-authorization)

###  **Data source – Azure Blob Storage**  
  
|Element name|Required|Notes|  
|------------------|--------------|-----------|  
|**type**|Yes|This element is associated with the **datasource** element. It indicates the type of data source that data will be written to. For Blob, the value should be Microsoft.Storage/Blob.|  
|**storageAccounts**|Yes|This element is associated with the **datasource** element. It provides a list of one or more Storage accounts to be used to write data to.|  
|**accountName**|Yes|This element is associated with the **storageAccounts** element. It indicates the name of the Storage account.|  
|**accountKey**|Yes|This element is associated with the **storageAccounts** element. It indicates the key for the Storage account. This property is not returned on **GET** requests.|  
|**container**|Yes|This element is associated with the **storageAccounts** element. It indicates the name of the container, within the associated Storage account, in which the output data is stored.|  
|**pathPattern**|Yes|This element is associated with the **storageAccounts** element. It represents a pattern against which blob names will be matched to determine whether or not they should be included as output to the job. Characters are tokenized 1:1, except for the following:<br /><br /> 1.  {date}<br />2.  {time}<br /><br /> Example: “/segment1/{date}/segment2/{time}”|  
|**dateFormat**|No|This element is associated with the **storageAccounts** element. It is present only when {date} is used in **pathPattern**. The value is an ISO-8601 format string. Wherever {date} appears in **pathPattern**, the value of this property is used as the date format instead.<br /><br /> Example: With **dateFormat** = “yyyy/MM/dd” and **pathPattern** = “/segment1/{date}/segment2”, the resulting pattern would match a prefix like “/segment1/2014/09/25/segment2/…”|  
|**timeFormat**|No|This element is associated with the **storageAccounts** element. It is present only when {time} is present in **pathPattern**. The value is an ISO-8601 format string. Wherever {time} appears in **pathPattern**, the value of this property is used as the time format instead.<br /><br /> Example: With **timeFormat** = “HH:mm” and **pathPattern** = “/segment1/{time}/segment2”, the resulting pattern would match a prefix like  “/segment1/23:10/segment2/…”|  
|**blobPathPrefix**|Yes|This element is associated with the **datasource** element. The string provided will be used to prefix all blob file names generated from your output. **Note that this property is deprecated as of API version 2015-06-01 but is still required for previous versions.**|  
  
#### **Data Source – Azure Table Storage**  
  
|Element name|Required|Notes|  
|------------------|--------------|-----------|  
|**accountName**|Yes|This element indicates the name of the Storage account where the table resides or will reside.|  
|**accountKey**|Yes|This element indicates the account key to access the Storage account.|  
|**table**|Yes|This element indicates the name of the table to use.|  
|**partitionKey**|Yes|This element indicates the name of a column from the **SELECT** statement in the query. Characters not valid for partition keys are removed from values used.|  
|**rowKey**|Yes|This element indicates the name of a column from the **SELECT** statement in the query. Characters not valid for row keys are removed from values used.|  
|**columnsToRemove**|No|If specified, each item in the array is the name of a column to remove (if present) from output event entities.|  
|**batchSize**|No|This element indicates the number of rows to write to the table at a time. It is an integer from 1 through 100. The default value, if not specified, is 100.|  
  
#### **Data Source – Event Hub**  
  
|Element name|Required|Notes|  
|------------------|--------------|-----------|  
|**type**|Yes|This element is associated with the **datasource** element. It indicates the type of data source that data will be written to. The value for an event hub should be Microsoft.ServiceBus/EventHub.|  
|**serviceBusNamespace**|Yes|This element is associated with the **datasource** element. This is the Service Bus namespace that was created during creation of your event-hub instance.|  
|**sharedAccessPolicyName**|Yes|This element is associated with the **datasource** element. This is the shared access policy name for the event hub that you are connecting to. This and the shared access key can be created on the **Configure** tab of Event Hubs in the Azure classic portal.|  
|**sharedAccessPolicyKey**|Yes|This element is associated with the **datasource** element. This is the shared access key for the policy. This property is not returned on **GET** requests.|  
|**eventHubName**|Yes|This element is associated with the **datasource** element. This is the name of your event-hub instance.|  
|**partitionKey**|No|The key that is used to determine to which partition to send event data.|  
  
#### **Data Source - SQL Database**  
  
|Element name|Required|Notes|  
|------------------|--------------|-----------|  
|**type**|Yes|This element is associated with the **datasource** element. It indicates the type of data source that data will be written to. The value for SQL Database should be Microsoft.Sql/Server/Database.|  
|**server**|Yes|This is the name of the server that contains the database that will be written to.|  
|**database**|Yes|This is the name of the database that output will be written to.|  
|**user**|Yes|This is the user name that will be used to connect to the SQL Database instance.|  
|**password**|Yes|This is the password that will be used to connect to the SQL Database instance.|  
|**table**|Yes|This is the name of the table that output will be written to.|  
  
#### **Data Source – Service Bus Queues**  
  
|Element name|Required|Notes|  
|------------------|--------------|-----------|  
|**type**|Yes|This element is associated with the datasource element. It indicates the type of data source that data will be sent to. The value for a Service Bus Queue should be Microsoft.ServiceBus/Queue.|  
|**serviceBusNamespace**|Yes|This element is associated with the datasource element. This is the Service Bus namespace that the queue is in.|  
|**sharedAccessPolicyName**|Yes|This element is associated with the datasource element. This is the shared access policy name for the queue that you are connecting to.|  
|**sharedAccessPolicyKey**|Yes|This element is associated with the datasource element. This is the shared access key for the policy. This property is not returned on GET requests.|  
|**queueName**|Yes|This element is associated with the datasource element. This is the name of your queue.|
|**propertyColumns**|Optional|A string array of the names of output columns to be attached to Service Bus messages as custom properties.|  
  
#### **Data Source – Service Bus Topics**  
  
|Element name|Required|Notes|  
|------------------|--------------|-----------|  
|**type**|Yes|This element is associated with the datasource element. It indicates the type of data source that data will be sent to. The value for a Service Bus Topic should be Microsoft.ServiceBus/Topic.|  
|**serviceBusNamespace**|Yes|This element is associated with the datasource element. This is the Service Bus namespace that the topic is in.|  
|**sharedAccessPolicyName**|Yes|This element is associated with the datasource element. This is the shared access policy name for the topic that you are connecting to.|  
|**sharedAccessPolicyKey**|Yes|This element is associated with the datasource element. This is the shared access key for the policy. This property is not returned on GET requests.|  
|**topicName**|Yes|This element is associated with the datasource element. This is the name of your topic.|
|**propertyColumns**|Optional|A string array of the names of output columns to be attached to Service Bus messages as custom properties.|    
  
#### **Data Source – DocumentDB**  
  
|Element name|Required|Notes|  
|------------------|--------------|-----------|  
|**type**|Yes|This element is associated with the datasource element. It indicates the type of data source that data will be written to. The value for a DocumentDB should be Microsoft.Storage/DocumentDB.|  
|**accountId**|Yes|The DocumentDB account name or ID.  This can also be fully qualified domain name endpoint for the account.|  
|**accountKey**|Yes|The shared access key for the DocumentDB account.|  
|**database**|Yes|The DocumentDB database name.|  
|**collectionNamePattern**|Yes|The collection name pattern for the collections to be used. The collection name format can be constructed using the optional {partition} token, where partitions start from 0.<br /><br /> For example the following are valid inputs:<br /><br /> ·         MyCollection{partition}<br /><br /> ·         MyCollection<br /><br /> Note that collections must exist before the Stream Analytics job is started and will not be created automatically.|  
|**partitionKey**|Yes|The name of the field in output events used to specify the key for partitioning output across collections.|  
|**documentId**|No|The name of the field in output events used to specify the primary key which insert or update operations are based on.|  
  
### Response  
 Status code: 201  
  
 **JSON**  
  
```  
  
{    
   "id":"/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/Default-SA-CentralUS/providers/Microsoft.StreamAnalytics/streamingjobs/myStreamingSample/outputs/output",  
   "name":"output",  
   "type":"Microsoft.StreamAnalytics/streamingjobs/outputs",  
   "properties":{    
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
  
```  
  
  
## Delete
Deletes an output from a Stream Analytics job in Microsoft Azure.  
  
### Request  
 The **Delete Output** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**DELETE**|https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs/{job-name}/outputs/output?api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name of the Stream Analytics job that you are deleting.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
### Response  
 Status code: 200  
  
  

## Get
Gets information about a specific output.  
  
### Request  
 The **Get Information about an Output** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**GET**|https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs/{job-name}/outputs/output?api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name of the Stream Analytics job that your output will be associated with.  
  
 Replace {input-name} with the name of the input that you want information about.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
### Response  
 Status code: 200  
  
 **JSON**  
  
```  
  
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
      }  
   }  
}  
```  
  
 Secrets are never returned in the **GET** response.  
  
  


## List
Lists all of the inputs that are defined in a Stream Analytics job.  
  
### Request  
 The **List Outputs** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx)  
  
|Method|Request URI|  
|------------|-----------------|  
|**GET**|https://managment.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs/{job-name}/outputs&api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/)  
  
 Replace {job-name} with the name of the Stream Analytics job.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
### Response  
 Status code: 200  
  
 **JSON**  
  
```  
  
{  
  "value": [  
    {  
      "id": "/subscriptions/{id}/resourceGroups/{group}/providers/microsoft.streamAnalytics/streamingjobs/filterSample/outputs/filteredData",  
      "name": "filteredData",  
      "type": "Microsoft.StreamAnalytics/streamingjobs/outputs",  
      "properties": {  
        "etag": "47956D46-4756-4857-9832-D3955AA721FB",  
        "datasource": {  
         "type": "Microsoft.Sql/Server/Database",  
          "properties": {  
           "server": "xyzzy1.database.windows.net",  
            "database": "Samples",  
            "table": "filteredSampleResults"  
          }  
        }  
      }  
    }  
  ],  
  "nextLink": null  
}  
  
```  
  
  








## Update
Updates the properties that are assigned to an output.  
  
### Request  
 The **Update Output** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**PATCH**|https://managment.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs/{job-name}/outputs/output?api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name of the Stream Analytics job that you are updating.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
 **JSON**  
  
```  
  
{    
   "properties":{    
      "datasource":{    
         "type":"Microsoft.Sql/Server/Database",  
         "properties":{    
            "table":"ClickEvents2"  
         }  
      }  
   }  
}  
  
```  
  
 Any one or more of the input properties may be specified in the request body, setting/replacing any existing value for each property specified.  
  
 For more information about input properties, see [Create Input &#40;Azure Stream Analytics&#41;](../StreamAnalyticsREST/Create-Input--Azure-Stream-Analytics-.md).  
  
### Response  
 Status code: 201  
  
 **JSON**  
  
```  
  
{    
   "id":"/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/Default-SA-CentralUS/providers/Microsoft.StreamAnalytics/streamingjobs/sample229400/outputs/output",  
   "name":"output",  
   "type":"Microsoft.StreamAnalytics/streamingjobs/outputs",  
   "properties":{    
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
  
```  
  
 The response body contains the updated input resource. Any secrets in the **PATCH** response body are redacted.  
  
  
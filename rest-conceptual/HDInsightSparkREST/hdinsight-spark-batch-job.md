# Batch Job

## Create a new batch job
Submit a new batch job from a jar.  
  
### Request  
 See [Common parameters and headers](../HDInsightSparkREST/batch-jobs.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|POST|`https://{cluster-endpoint}/livy/batches`|  
  
 Following shows an example request to create a new batch job  
  
```json  
{  
	   "file" : "wasb://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/sample.jar",  
	   "args" : ["arg0", "arg1"],  
	   "className" : "com.sample.Job1",  
	   "jars" : ["wasb://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/helper.jar"],  
	   "files" : ["wasb://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/config.xml"],  
	   "driverMemory" : "1G",  
	   "driverCores" : 2,  
	   "executorMemory" : "1G",  
	   "executorCores" : 10,  
	   "numExecutors" : 10  
}  
  
```  
  
|Element Name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|proxyUser|No|String|The user to impersonate that will execute the job|  
|file|Yes|String|Path to the batch job’s jar.|  
|args|No|Array of String|Command line arguments passed to the batch job.|  
|className|Yes|String|The class name of the main class.|  
|jars|No|Array of String|Files to be placed on the java classpath|  
|pyFiles|No|Array of String|Files to be placed on the PYTHONPATH|  
|files|No|Array of String|Files to be placed in executor working directory|  
|driverMemory|No|String|Memory for driver (e.g. 1000M, 2G)|  
|driverCores|No|Integer|Number of cores used by driver|  
|executorMemory|No|String|Memory for executor (e.g. 1000M, 2G)|  
|executorCores|No|Integer|Number of cores used by executor|  
|numExecutors|No|Integer|number of executor|  
|archives|No|Array of String|Archives to be uncompressed (YARN mode only)|  
  
### Response  
 The operation will return 200 (OK) if the request is completed successfully  
  
 **Status code:** 200 OK  
  
 **Response body:**  
  
```  
{  
   "id" : 1,  
   "state" : "starting",  
   "log" : ["logline"]  
}  
  
```  
  
|Element Name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|id|Yes|Integer|The batch session id|  
|log|Yes|Array of string|Array of log lines for this batch job.|  
|state|No|String|The session state. Possible value: [“starting”, “idle”, “error”]|



## Get the full log of a batch job
### Request  
 See [Common parameters and headers](../HDInsightSparkREST/batch-jobs.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://{cluster-endpoint}/livy/batches/{batch-id}/log`|  
  
### Response  
 If validation is complete and the request is accepted, the operation will return 200 (OK).  
  
 Status code: 200 OK  
  
 Response body:  
  
```  
{  
"id" : 1,  
"from":0,  
"total":54  
“log" : ["logline1", “logline2”]  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|id|Yes|Integer|The batch session id|  
|from|Yes|Integer|Offset|  
|size|Yes|Integer|Total amount of lines|  
|log|Yes|Array of string|Array of log lines for this batch job.|



## Get the state of a batch job
### Request  
 See Common parameters and headers for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://{cluster-endpoint}/livy/batches/{batch-id}`|  
  
### Response  
 If validation is complete and the request is accepted, the operation will return 200 (OK).  
  
 Status code: 200 OK  
  
 Response body:  
  
```  
{  
"id" : 1,  
"state" : "starting",  
“log" : ["logline"]  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|id|Yes|Integer|The batch session id|  
|log|Yes|Array of strings|Array of log lines for this batch job.|  
|state|Yes|String|The session state. Possible value: [“starting”, “idle”, “error”]|

## Kill a batch job
### Request  
 See [Common parameters and headers](../HDInsightSparkREST/batch-jobs.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|DELETE|`https://{cluster-endpoint}/livy/batches/{batch-id}`|  
  
### Response  
 If validation is complete and the request is accepted, the operation will return 200 (OK).  
  
 Status code: 200 OK  
  
 Response body:  
  
```  
{  
"msg" : "deleted"  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|Message|Yes|String|The message of the delete.|  
  
### Interactive sessions  
  
-   Start, submit statement, retrieve statement result and terminate an interactive session

## Return all active batch jobs
### Request  
 See [Common parameters and headers](../HDInsightSparkREST/batch-jobs.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://{cluster-endpoint}/livy/batches`|  
  
### Response  
 If validation is complete and the request is accepted, the operation will return 200 (OK).  
  
 **Status code**: 200 OK  
  
 **Response body:**  
  
```json  
{  
	"from" : 0,  
	"total" : 2,  
	"sessions" : [{  
			"id" : 1,  
			"state" : "starting",  
			"log" : ["logline"]  
		}, {  
			"id" : 0,  
			"state" : "idle",  
			"log" : ["logline"]  
		}  
	]  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|from|Yes|String|Offset|  
|total|Yes|String|Amount of batches to return|  
|session|Yes|Array of Complex  Type (Batch)|A list of active batch jobs|  
  
#### Batch  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|id|Yes|Integer|The batch session id|  
|log|Yes|Array of strings|Array of log lines for this batch job.|  
|state|Yes|String|The session state. Possible value: [“starting”, “idle”, “error”]|


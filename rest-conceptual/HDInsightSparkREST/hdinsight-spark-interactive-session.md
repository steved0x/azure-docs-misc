# Interactive session

## Create a new interactive session
Start a new interactive session.  
  
### Request  
 See [Common parameters and headers](../HDInsightSparkREST/interactive-sessions.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|POST|`https://{cluster-endpoint}/livy/sessions`|  
  
 Following shows an example request to create a new interactive session  
  
```  
{  
	"kind" : "spark",  
	"jars" : ["wasb://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/helper.jar"],  
	"files" : ["wasb://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/config.xml"],  
	"driverMemory" : "1G",  
	"driverCores" : 2,  
	"executorMemory" : "1G",  
	"executorCores" : 10,  
	"numExecutors" : 10  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|Kind|Yes|String|The session kind. Possible values: [“spark”, “pyspark”, “sparkr”]|  
|proxyUser|No|String|The user to impersonate that will execute the job|  
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
"kind" : "spark",  
“log" : ["logline"]  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|id|Yes|Integer|The interactive session id|  
|Kind|Yes|String|The session kind. Possible values: [“spark”, “pyspark”, “sparkr”]|  
|log|Yes|Array of strings|Array of log lines for this batch job.|  
|State|Yes|String|The session state. Possible value: [“starting”, “idle”, “error”, “running”, “success”]|


## Get the state of an interactive session
### Request  
 See [Common parameters and headers](../HDInsightSparkREST/interactive-sessions.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://{cluster-endpoint}/livy/sessions/{session-id}`|  
  
### Response  
 If validation is complete and the request is accepted, the operation will return 200 (OK).  
  
 **Status code:** 200 OK  
  
 **Response body:**  
  
```  
{  
"id" : 1,  
"state" : "starting",  
"kind" : "spark",  
“log" : ["logline"]  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|id|Yes|Integer|The batch session id|  
|Kind|Yes|String|The session kind. Possible values: [“spark”, “pyspark”, “sparkr”]|  
|log|Yes|Array of strings|Array of log lines for this batch job.|  
|state|Yes|String|The session state. Possible value: [“starting”, “idle”, “error”]|


## Retrieve statement results of an interactive session
### Request  
 See [Common parameters and headers](../HDInsightSparkREST/interactive-sessions.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://{cluster-endpoint}/livy/sessions/{session-id}/statements`|  
  
### Response  
 If validation is complete and the request is accepted, the operation will return 200 (OK).  
  
 **Status code:** 200 OK  
  
 **Response body:**  
  
```  
{  
"total_statements" : 1,  
"statements" : [{  
			"id" : 0,  
			"state" : "available",  
			"output" : {  
				"status" : "ok",  
				"execution_count" : 1,  
				"data" : {  
					"text/plain" : "res1: Int = 2"  
				}  
			}  
		}  
	]  
}  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|Total_statements|Yes|Integer|Total number of statements|  
|Statements|Yes|Array of complex Type (Statement)|Output of statement|  
  
 **Statement**  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|Id|Yes|Integer|The statement id|  
|State|Yes|String|The statement state.|  
|Output|Yes|Complex type (Output)|The output of the statement.|  
  
 **Output**  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|Status|Yes|String|The statement status|  
|Execution_count|Yes|Integer|The number of execution|  
|data|Yes|Complex type (Text)|The text output of the statement.|  
  
 **Text**  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|Text/plain|Yes|String|The plain text of the output|


## Return all active interactive sessions
### Request  
 See [Common parameters and headers](../HDInsightSparkREST/interactive-sessions.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://{cluster-endpoint}/livy/sessions`|  
  
### Response  
 If validation is complete and the request is accepted, the operation will return 200 (OK).  
  
 **Status code:** 200 OK  
  
 **Response body:**  
  
```  
{  
	"from" : 0,  
	"total" : 2,  
	"sessions" : [{  
			"id" : 1,  
			"state" : "starting",  
			"kind" : "spark",  
			"log" : ["logline"]  
		}, {  
			"id" : 0,  
			"state" : "idle",  
			"kind" : "spark",  
			"log" : ["logline"]  
		}  
	]  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|from|Yes|String|Offset|  
|total|Yes|String|Amount of sessions to return|  
|sessions|Yes|Array of Complex  Type (Session)|A list of active sessions|  
  
#### Session  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|id|Yes|Integer|The interactive session id|  
|Kind|Yes|String|The session kind. Possible values: [“spark”, “pyspark”, “sparkr”]|  
|log|Yes|Array of strings|Array of log lines for this session.|  
|state|Yes|String|The session state. Possible value: [“starting”, “idle”, “error”, “running”, “success”]|


## Submit statement(s) to an interactive session
### Request  
 See [Common parameters and headers](../HDInsightSparkREST/interactive-sessions.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|POST|`https://{cluster-endpoint}/livy/sessions/{session-id}/statements`|  
  
 Following shows an example request to create a new interactive session.  
  
```  
{  
	"code" : "1 + 1"  
}  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|Code|Yes|String|The code to execute|  
  
### Response  
 If validation is complete and the request is accepted, the operation will return 200 (OK).  
  
 **Status code:** 200 OK  
  
 **Response body:**  
  
```  
{  
"id" : 1,  
"state" : "running",  
"output" : null  
}  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|id|Yes|Integer|The batch session id|  
|Output|Yes|String|Output of statement|  
|state|Yes|String|The session state. Possible value: [“starting”, “idle”, “error”]|

## Terminate an interactive session
### Request  
 See [Common parameters and headers](../HDInsightSparkREST/interactive-sessions.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|DELETE|`https://{cluster-endpoint}/livy/sessions/{session-id}`|  
  
### Response  
 If validation is complete and the request is accepted, the operation will return 200 (OK).  
  
 **Status code:** 200 OK  
  
 **Response body:**  
  
```  
{  
"msg" : "deleted"  
}  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|Message|Yes|String|The message of the delete.|


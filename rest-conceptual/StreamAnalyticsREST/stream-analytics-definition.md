# Definition

## Retrieve Default Definition (Azure Stream Analytics)
  Takes programmatically queryable interface for a UDF binding and returns the default function definition. This definition can then be used to create the UDF. This endpoint helps user to construct the initial UDF definition which they can later change according to their requirements if needed.  
  
### Request  
 The **Retrieve Default Definition Function** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
 Request  
  
|Method|Request URI|  
|------------|-----------------|  
|**POST**|https://<endpoint\>/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions/{functionName}/RetrieveDefaultDefinition?api-version={api-version}|  
  
 **Parameters**  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to.  
  
 Replace {job-name} with the name that you want to assign to the Stream Analytics job that you are creating. The job name is case insensitive and must be unique among all inputs in the job, containing only numbers, letters, and hyphens. It must be 3 to 63 characters long.  
  
 Replace {functionName} with the name of the user-defined function.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
 **Request Headers**  
  
 Common request headers only.  
  
 **Request Body**  
  
```  
{  
  "bindingType": "Microsoft.MachineLearning/WebService",  
  "bindingRetrievalProperties": {  
    "executeEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77fa4a46bf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",  
    "udfype": "Scalar"  
  }  
}  
```  
  
|Property|Description|  
|--------------|-----------------|  
|bindingType|Type of the function binding. Microsoft.MachineLearning/WebService is the only binding currently supported.|  
|bindingRetrievalProperties|Properties that describe how the interface for the binding can be obtained. Properties are dependent on the type of the binding.|  
  
 Azure Machine Learning RSS binding retrieval properties.  
  
|||  
|-|-|  
|bindingRetrievalProperties.udfType|Type of the UDF. Scalar is currently the only supported type.|  
|bindingRetrievalProperties.executeEndpoint|Request-Response execute endpoint of the Azure Machine Learning Webservice. <br />This endpoint is available from the Request-Response endpoint documentation page in the Azure management portal.|  
  
 **Response**  
  
 **Status Code:**  
  
-   200 if default udf definition is created successfully.  
  
-   400 (Bad Reqeust) if binding retrieval properties are invalid or if the endpoint provided did not respond.  
  
 **Response Headers**  
  
 Common response headers  
  
  
# Function

  A (User-Defined) Function provides an extensible way for a Streaming Job to transform input data to output data using a facility that is not completely described by the Transformation query. Currently Azure Machine Learning Request-Response Service (RRS) is the supported UDF framework.  
  
### Request  
 The **Function** property is a properties bag needed to completely specify the information needed to make use of an Azure Machine Learning function.  
  
```  
{  
  "type": <function type>,  
  "properties": {  
    .  
    .  
    .  
  }  
}  
  
```  
  
 **Type**: Scalar  
  
 Properties  
  
 Azure Machine Learning Request-Response Service (RRS) Endpoint  
  
 A transformation query can call out to an operationalized Azure ML Request-Response Service (RRS) endpoint to perform scoring against a trained model. The properties in the property bag are just those needed to call the operationalized RRS endpoint.  
  
 Example payload to create an Azure Machine Learning scalar function  
  
```  
{  
  "name": "scoreTweet",  
  "properties": {  
    "type": "Scalar",  
    "properties": {  
      "inputs": [  
        {  
          "dataType": "nvarchar(max)",  
          "isConfigurationParameter": false  
        }  
      ],  
      "output": {  
        "dataType": "nvarchar(max)"  
      },  
      "binding": {  
        "type": "Microsoft.MachineLearning/WebService",  
        "properties": {  
          "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77fa4a46bf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",  
          "apiKey": "apiKey",  
          "inputs": {  
            "name": "input1",  
            "columnNames": [  
              {  
                "name": "tweet",  
                "dataType": "String",  
                "mapTo": 0  
              }  
            ]  
          },  
          "outputs": [  
            {  
              "name": "Sentiment",  
              "dataType": "String"  
            }  
          ],  
          "batchSize": 100  
        }  
      }  
    }  
  }  
}  
  
```  
  
|Property|Description|  
|--------------|-----------------|  
|name|Name of the UDF|  
|Type|Scalar|  
|inputs|An array of inputs, describing the parameters of the UDF.|  
|Inputs.dataType|Data type of the UDF parameter. List of valid Azure Stream Analytics data types are  described at [Azure Stream Analytics data types](https://msdn.microsoft.com/en-us/library/azure/dn835065.aspx).|  
|Input.isConfigurationParameter|Optional. True if this parameter is expected to be a constant. Default is false.|  
|output|Described output of the UDF.|  
|Output.dataType|Data type of UDF output. List of valid Azure Stream Analytics data types are  described at [Azure Stream Analytics data types](https://msdn.microsoft.com/en-us/library/azure/dn835065.aspx).|  
|Binding|Described the physical binding for the UDF. For example, in Azure Machine Learning RRS's this described the endpoint.|  
|Binding.Type|Type of the binding. Currently **Microsoft.MachineLearning/WebService** is the only valid binding at this time.|  
|Binding.Properties|Properties for the binding. Values are dependent on the type of binding.|  
  
 Binding properties for Microsoft.MachineLearning/WebService.  
  
|Property|Description|  
|--------------|-----------------|  
|Endpoint|Request-Response execute endpoint of Azure Machine Learning Webservice. This endpoint is available from the Request-Response Endpoint documentation page in the Azure Management portal.|  
|apiKey|API key used to authenticate with Request-Response endpoint. This is available from the Azure Management portal.|  
|batchSize|Optional. Value between 10 and 1000 describing maximum number of rows for every Azure Machine Learning RRS execute request. Default is 10.|  
|Inputs|Describes the set of inputs for RRS enpoint.|  
|Inputs.name|Name of the input. This is the name provided while authoring the endpoint. The name is available from Azure Machine Learning Studio or from the RRS endpoint documentation page.|  
|Input.ColumnNames|Array describing inputs to Azure Machine Learning  endpoint|  
  
 Element properties of Input.ColumnNames  
  
|Property|Description|  
|--------------|-----------------|  
|Name|Name of the input column.|  
|dataType|Azure Machine Learning data type. List of valid types are available at [Azure Machine Learning data types](https://msdn.microsoft.com/library/azure/dn905923.aspx). These are also described in RRS endpoint documentation.|  
|MapTo|Zero based index of the UDF parameter this input maps to.|  
|Outputs|Array describing outputs from an Azure Machine Learning RRS endpoint execution.|  
  
 Element properties of Outputs  
  
|Property|Description|  
|--------------|-----------------|  
|Name|Name of the output column.|  
|dataType|Azure Machine Learning data type. List of valid types are available at [Azure Machine Learning data types](https://msdn.microsoft.com/library/azure/dn905923.aspx). These are also described in RRS endpoint documentation.|  
  
  

## Create
Creates a new Stream Analytics user-defined function.  
  
### Request  
 The **Create Function** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
 **Request**  
  
|Method|Request URI|  
|------------|-----------------|  
|**PUT**|https://<endpoint\>/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions/{functionName}?api-version={api-version}|  
  
 **Parameters**  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name that you want to assign to the Stream Analytics job that you are creating. The job name is case insensitive and must be unique among all inputs in the job, containing only numbers, letters, and hyphens. It must be 3 to 63 characters long.  
  
 Replace {functionName} with the name of the user-defined function.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
 **Request Headers**  
  
 Common request headers only.  
  
 **Request Body**  
  
 **JSON**  
  
```  
  
{  
  "properties": {  
    "type": {function type},  
    "properties": {  
      .  
      . function type-specific properties  
      .  
    }  
  }  
}  
  
```  
  
|Property|Required|Description|  
|--------------|--------------|-----------------|  
|**type**|Yes|The function type. String. “Scalar” is the only allowed type.|  
|**properties**|Yes|Collection of function type-specific properties. May be empty.|  
  
> [!NOTE]  
>  Create Function will validate if the binding and input columns specified matches, if it doesn’t it would return an error. Note that this validation will be triggered only if either input or output is specified. For AzureML binding, endpoint and apikey are mandatory properties.  
>   
>  Details on input, output and bindings are found in the [Functions &#40;Azure Stream Analytics&#41;](../StreamAnalyticsREST/Functions--Azure-Stream-Analytics-.md) page.  
  
### Example payloads  
 Example payload to create an Azure Machine learning scalar function  
  
 Function type, Binding type and key properties describing the binding should always be provided. For Azure machine learning scalar function, “endpoint” is the only key property.  
  
 **Response**  
  
 **Status code:**  
  
-   201  (Created) or 200 (OK) if request completed successfully  
  
-   404 (NotFound) if top level resources are not found (subscription, resource group, mdw).  
  
-   409 (Conflict) if job is in a state where updating functions is not allowed  
  
-   412 (Precondition Failed) if failed condition specified by If-Match header.  
  
-   400 (Bad Request) if request body fails validation.  
  
 **Response Headers**  
  
 Common response headers only  
  
 **Response Body**  
  
```  
{  
  "properties": {  
    "type": {function type},  
    "properties": {  
      .  
      . function type-specific properties  
      .  
    }  
  }  
}  
  
```  
  
> [!NOTE]  
>  The Azure Machine Learning RRS apiKey secret is returned in the PUT response, as it was supplied in the PUT request.  
  
|Property|Description|  
|--------------|-----------------|  
|**type**|The function type. String.|  
|**properties**|Collection of function type-specific properties. May be empty.|  
  
 **Example**  
  
```  
  
{  
    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/0c3767c3-b17f-45ba-a306-cd490802f99f/providers/Microsoft.StreamAnalytics/streamingjobs/581ca559-5224-46b6-8668-dae42d0194be/functions/azuremlscalarFunction",  
    "name": "azuremlscalarFunction",  
    "type": "Microsoft.StreamAnalytics/streamingjobs/functions",  
    "properties": {  
        "type": "Scalar",  
        "properties": {  
            "inputs": [  
                {  
                "dataType": "nvarchar(max)",  
                "isConfigurationParameter": false  
                }  
            ],  
            "output": {  
                "dataType": "nvarchar(max)"  
            },  
            "binding": {  
                "type": "Microsoft.MachineLearning/WebService",  
                "properties": {  
                    "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77fa4a46bf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",  
                    "apiKey": null,  
                    "inputs": {  
                        "name": "input1",  
                        "columnNames": [  
                            {  
                                "name": "78f69f41-aab4-43d2-844a-800b116eed3a",  
                                "dataType": "Boolean",  
                                "mapTo": 0  
                            }  
                        ]  
                    },  
                    "outputs": [  
                        {  
                            "name": "output",  
                            "dataType": "String"  
                        }  
                    ],  
                    "batchSize": 100  
                }  
            }  
        }  
    }  
}  
  
```  
  
  
## Delete
Deletes the specified user-defined function.  
  
### Request  
 The **Delete Function** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
 Request  
  
|Method|Request URI|  
|------------|-----------------|  
|**DELETE**|https://<endpoint\>/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/function/{functionName}?api-version={api-version}|  
  
 **Parameters**  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name that you want to assign to the Stream Analytics job that you are creating. The job name is case insensitive and must be unique among all inputs in the job, containing only numbers, letters, and hyphens. It must be 3 to 63 characters long.  
  
 Replace {functionName} with the name of the user-defined function.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
 **Request Headers**  
  
 Common request headers only.  
  
 **Request Body**  
  
 Empty  
  
 **Response**  
  
 Status Code as per RPC  
  
 **Response Headers**  
  
 Common request headers only.  
  
 **Response Body**  
  
 Empty  
  
  

## Get
Gets information about a specific user-defined function.  
  
### Request  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**GET**|https://<endpoint\>/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions/{functionName}?api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name of the Stream Analytics job that you want information about.  
  
 Replace functionName with the name of the user-defined function.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
## Response  
 Status code: 200  
  
 **JSON**  
  
```  
  
{  
  "id": "/subscriptions/{id}/resourceGroups/{group}/providers/microsoft.streamAnalytics/streamingjobs/filterSample/functions/{functionName}",  
  "name": {functionName},  
  "type": "Microsoft.StreamAnalytics/streamingjobs/functions",  
  "properties": {  
    "type": {functionType},  
    "properties": {  
      .  
      . function type-specific properties  
      .  
    }  
  }  
}  
  
```  
  
 Example Azure Machine Learning RRS scalar UDF response.  
  
```  
{  
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/providers/Microsoft.StreamAnalytics/streamingjobs/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/functions/azuremlscalarFunction",  
  "name": "azuremlscalarFunction",  
  "type": "Microsoft.StreamAnalytics/streamingjobs/functions",  
  "properties": {  
    "type": "Scalar",  
    "properties": {  
      "inputs": [  
        {  
          "dataType": "nvarchar(max)",  
          "isConfigurationParameter": false  
        }  
      ],  
      "output": {  
        "dataType": "nvarchar(max)"  
      },  
      "binding": {  
        "type": "Microsoft.MachineLearning/WebService",  
        "properties": {  
          "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx/services/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx/execute",  
          "apiKey": null,  
          "inputs": {  
            "name": "input1",  
            "columnNames": [  
              {  
                "name": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",  
                "dataType": "Boolean",  
                "mapTo": 0  
          }  
            ]  
          },  
          "outputs": [  
            {  
              "name": "output",  
              "dataType": "String"  
            }  
          ],  
          "batchSize": 100  
        }  
      }  
    }  
  }  
}  
  
```  
  
 **Note**: The Azure Machine Learning RRS apiKey secret is not returned in the GET response.  
  
  

## List
Lists all of the functions that are defined in a Stream Analytics job.  
  
### Request  
 The **List Functions** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**GET**|https://managment.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs/{job-name}/functions&api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name of the Stream Analytics job.  
  
 Replace {api-version} with 2015-10-01-preview in the URI.  
  
### Response  
 Status code: 200  
  
 **JSON**  
  
 The example below shows a response from a List Functions  request for an Stream Analytics job with one Azure Machine Learning Function.  
  
```  
  
{   
  "id": "/subscriptions/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx/resourceGroups/0c3767c3-b17f-45ba-a306-cd490802f99f/providers/Microsoft.StreamAnalytics/streamingjobs/581ca559-5224-46b6-8668-dae42d0194be/functions/azuremlscalarFunction",  
  "name": "azuremlscalarFunction",   
  "type": "Microsoft.StreamAnalytics/streamingjobs/functions",   
  "properties": {   
    "type": "Scalar",   
    "properties": {   
      "inputs": [   
        {   
          "dataType": "nvarchar(max)",   
          "isConfigurationParameter": false   
        }   
      ],   
      "output": {   
        "dataType": "nvarchar(max)"   
      },   
      "binding": {   
        "type": "Microsoft.MachineLearning/WebService",   
        "properties": {   
          "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77fa4a46bf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",   
          "apiKey": null,   
          "inputs": {   
            "name": "input1",   
            "columnNames": [   
              {   
                "name": "78f69f41-aab4-43d2-844a-800b116eed3a",   
                "dataType": "Boolean",   
                "mapTo": 0   
       }   
            ]   
          },   
          "outputs": [   
            {   
              "name": "output",   
              "dataType": "String"   
            }   
          ],   
          "batchSize": 100   
        }   
      }   
    }   
  }   
}  
  
```  
  
  

## Test
Tests whether the specified connection information provided for the binding is valid. If the binding exposes a programmatically queryable interface,  test endpoint validates if the UDF definition is compatible with what is returned by the interface. For example, for Azure Machine Learning it uses swagger endpoint to verify if the UDF definition matches swagger definition.  
  
 For Azure Machine Learning RRS service, it queries the swagger endpoint and validates that all the input and output columns described in the binding exists.  
Testing is performed based on the union of the functions current property values as amended by any property values present in the request body. The following are supported scenarios:  
  
|Scenario|Request Body|  
|--------------|------------------|  
|Create new function|All properties specified (like with PUT)|  
|Edit existing function|Modified properties specified (like with PATCH)|  
|Test with current values|No properties specified|  
  
 Testing is asynchronous. When the operation is complete, the entity returned in the Location header of the POST action response includes the full details of the tests run and the results.  
  
### Request  
 The **Test Function** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
 Request  
  
|Method|Request URI|  
|------------|-----------------|  
|**POST**|https://<endpoint\>/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/functions/{functionName}/test?api-version={api-version}|  
  
 **Parameters**  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name that you want to assign to the Stream Analytics job that you are creating. The job name is case insensitive and must be unique among all inputs in the job, containing only numbers, letters, and hyphens. It must be 3 to 63 characters long.  
  
 Replace {functionName} with the name of the user-defined function.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
 **Request Headers**  
  
 Common request headers only.  
  
 **Request Body**  
  
 Any one or more of the input type-specific properties used in PUT may be specified in the request body.  
  
 **Response**  
  
 **Status Code:**  
  
-   202  (Accepted) if the request was accepted to complete asynchronously.  
  
-   404 (NotFound) if top level resources are not found (subscription, resource group, mdw).  
  
-   400 (Bad Reqeust) if Test Function is called with an empty request body or a non-existing source.  
  
-   5xx if the service is unable to run the test due to service or communication issues.  
  
 **Response Headers**  
  
 Common response headers  
  
 **Response Body**  
  
 None from the POST operation itself. Clients should use the Asynchronous Operations pattern to get the results of the test. Results are returned as Test Operation Results.  
  
> [!NOTE]  
>  The Azure Machine Learning RRS apiKey secret is returned in the PUT response, as it was supplied in the PUT request.  
  
 **Examples**  
  
```  
{   
  "id": "/subscriptions/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx/resourceGroups/0c3767c3-b17f-45ba-a306-cd490802f99f/providers/Microsoft.StreamAnalytics/streamingjobs/581ca559-5224-46b6-8668-dae42d0194be/functions/azuremlscalarFunction",  
  "name": "azuremlscalarFunction",   
  "type": "Microsoft.StreamAnalytics/streamingjobs/functions",   
  "properties": {   
    "type": "Scalar",   
    "properties": {   
      "inputs": [   
        {   
          "dataType": "nvarchar(max)",   
          "isConfigurationParameter": false   
        }   
      ],   
      "output": {   
        "dataType": "nvarchar(max)"   
      },   
      "binding": {   
        "type": "Microsoft.MachineLearning/WebService",   
        "properties": {   
          "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77fa4a46bf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",   
          "apiKey": null,   
          "inputs": {   
            "name": "input1",   
            "columnNames": [   
              {   
                "name": "78f69f41-aab4-43d2-844a-800b116eed3a",   
                "dataType": "Boolean",   
                "mapTo": 0   
       }   
            ]   
          },   
          "outputs": [   
            {   
              "name": "output",   
              "dataType": "String"   
            }   
          ],   
          "batchSize": 100   
        }   
      }   
    }   
  }   
}  
```  
  
  
## Update
Updates the specified function to use a different Azure Machine Language RRS endpoint (specified with the API key) that uses the scoring type (same feature vector) as the function.  
  
### Request  
 The **Update Function** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
 **Request**  
  
|Method|Request URI|  
|------------|-----------------|  
|**PATCH**|https://<endpoint\>/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/function/{functionName}?api-version={api-version}|  
  
 **Parameters**  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name that you want to assign to the Stream Analytics job that you are creating. The job name is case insensitive and must be unique among all inputs in the job, containing only numbers, letters, and hyphens. It must be 3 to 63 characters long.  
  
 Replace {functionName} with the name of the user-defined function.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
 **Request Headers**  
  
 Common request headers only.  
  
 **Request Body**  
  
 One or more properties used in the Create Function may be specified in the request body, setting/replacing any existing value for each property specified.  
  
 **JSON**  
  
```  
  
{  
  "properties": {  
    "type": {function type},  
    "properties": {  
      .  
      . function type-specific properties  
      .  
    }  
  }  
}  
  
```  
  
|Property|Required|Description|  
|--------------|--------------|-----------------|  
|**type**|Yes*|The function type. String. “Scalar” is the only allowed type.|  
|**properties**|Yes|Collection of function type-specific properties to change. May be empty.|  
  
 **\***Using PATCH to change the function type is not permitted. Since changing the function type likely would specify a whole new set of function type-specific properties. PUT rather than PATCH should be used to replace the complete entity.  
  
> [!NOTE]  
>  Update Function will validate if the binding and input columns specified matches, if it doesn’t it would return an error. Note that this validation will be triggered only if either input or output is specified. For AzureML binding, endpoint and apikey are mandatory properties.  
  
## Examples  
 Change the function to use a different Azure Machine Learning RRS endpoint (with a corresponding different API key) that does the same kind of scoring (same feature vector) as the old one.  
  
 Function type, Binding type and key properties describing the binding should always be provided. For Azure machine learning scalar function, “endpoint” is the only key property.  
  
 **Response**  
  
 **Status code:**  
  
-   200 (OK) if request completed successfully (or resource does not exist)  
  
-   409 (Conflict) if job is in a state where updating functions is not allowed  
  
-   412 (Precondition Failed) if failed condition specified by If-Match header.  
  
-   400 (Bad Request) if request body fails validation.  
  
 **Response Headers**  
  
 Common response headers only  
  
 **Response Body**  
  
```  
{  
  "properties": {  
    "type": {function type},  
    "properties": {  
      .  
      . function type-specific properties  
      .  
    }  
  }  
}  
  
```  
  
> [!NOTE]  
>  The apiKey secret is not returned in the PATCH response.  
  
  







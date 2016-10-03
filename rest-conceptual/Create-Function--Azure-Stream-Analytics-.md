---
title: "Create Function (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 346b9ceb-23cf-4c62-a056-2d0b6e522b02
caps.latest.revision: 11
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
# Create Function (Azure Stream Analytics)
  Creates a new Stream Analytics user-defined function.  
  
## Request  
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
>  Details on input, output and bindings are found in the [Functions &#40;Azure Stream Analytics&#41;](../rest-conceptual/Functions--Azure-Stream-Analytics-.md) page.  
  
## Example payloads  
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
  
  
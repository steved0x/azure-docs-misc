---
title: "Test Function (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 269335e9-fd48-4d29-bade-90542edb3562
caps.latest.revision: 7
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
# Test Function (Azure Stream Analytics)
  Tests whether the specified connection information provided for the binding is valid. If the binding exposes a programmatically queryable interface,  test endpoint validates if the UDF definition is compatible with what is returned by the interface. For example, for Azure Machine Learning it uses swagger endpoint to verify if the UDF definition matches swagger definition.  
  
 For Azure Machine Learning RRS service, it queries the swagger endpoint and validates that all the input and output columns described in the binding exists.  
Testing is performed based on the union of the functions current property values as amended by any property values present in the request body. The following are supported scenarios:  
  
|Scenario|Request Body|  
|--------------|------------------|  
|Create new function|All properties specified (like with PUT)|  
|Edit existing function|Modified properties specified (like with PATCH)|  
|Test with current values|No properties specified|  
  
 Testing is asynchronous. When the operation is complete, the entity returned in the Location header of the POST action response includes the full details of the tests run and the results.  
  
## Request  
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
  
  
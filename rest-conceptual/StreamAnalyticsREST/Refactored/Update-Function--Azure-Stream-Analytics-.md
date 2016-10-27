---
title: "Update Function (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: a679f85e-c551-4706-9294-93a12729f607
caps.latest.revision: 6
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
# Update Function (Azure Stream Analytics)
  Changes the specified function to use a different Azure Machine Language RRS endpoint (specified with the API key) that uses the scoring type (same feature vector) as the function.  
  
## Request  
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
  
  
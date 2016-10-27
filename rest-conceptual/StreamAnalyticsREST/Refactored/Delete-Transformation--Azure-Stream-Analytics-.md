---
title: "Delete Transformation (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 5df60827-6956-48d0-8c3a-817fc2fcb61a
caps.latest.revision: 18
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
# Delete Transformation (Azure Stream Analytics)
  Deletes a transformation from a Stream Analytics job in Microsoft Azure.  
  
## Request  
 The **Delete Transformation** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**DELETE**|https://managment.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs/{job-name}/transformations/{transformation-name}?api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this transformation belongs to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name of the Stream Analytics job that you are deleting.  
  
 Replace {transformation-name} with the name (or alias) that you want to assign to the transformation that you are creating. The transformation name is case insensitive and must contain only numbers, letters, and hyphens. It must be 3 to 63 characters long.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
## Response  
 Status code: 202  
  
 This is an asynchronous operation that returns a status of 202 until the job is successfully deleted. The **Location** response header contains the URI that is used to obtain the status of the process. While the process is running, a call to the URI in the **Location** header returns a status of 202. When the process finishes, the URI in the **Location** header returns a status of 200.  
  
  
---
title: "Delete Stream Analytics Job (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 70b7d837-4534-46f7-be4c-38da678a5d41
caps.latest.revision: 19
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
# Delete Stream Analytics Job (Azure Stream Analytics)
  Deletes a Stream Analytics job in Microsoft Azure.  
  
 When you delete a Stream Analytics job, all of its associated content will be deleted (inputs, transformation, and output).  
  
## Request  
 The **Delete Stream Analytics Job** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**DELETE**|https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs/{job-name}?api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name of the Stream Analytics job that you are deleting.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
## Response  
 Status code: 202  
  
 This is an asynchronous operation that returns a status of 202 until the job is successfully deleted. The **Location** response header contains the URI that is used to obtain the status of the process. While the process is running, a call to the URI in the **Location** header returns a status of 202. When the process finishes, the URI in the **Location** header returns a status of 200.  
  
  
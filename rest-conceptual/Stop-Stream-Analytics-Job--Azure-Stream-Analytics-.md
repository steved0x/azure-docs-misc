---
title: "Stop Stream Analytics Job (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: a1abb492-8818-403c-a9f0-f74e353697af
caps.latest.revision: 20
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
# Stop Stream Analytics Job (Azure Stream Analytics)
  Stops a Stream Analytics job from running in Microsoft Azure, and deallocates resources that were being used. The job definition and metadata will remain available within your subscription through both the Azure classic portal and management APIs, such that the job can be edited and restarted. You will not be charged for a job in the stopped state.  
  
## Request  
 The **Stop Stream Analytics Job** request is specified as follows.  
  
 For headers and parameters that are used by all requests related to Stream Analytics jobs, see [Common parameters and headers](http://msdn.microsoft.com/library/azure/8d088ecc-26eb-42e9-8acc-fe929ed33563). You must make sure that the request that is made to the management service is secure. For additional details, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
|Method|Request URI|  
|------------|-----------------|  
|**POST**|https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.StreamAnalytics/streamingjobs/{job-name}/stop?api-version={api-version}|  
  
 Replace {subscription-id} with your subscription ID.  
  
 Replace {resource-group-name} with the name of the resource group that this job will belong to. For more information about creating resource groups, see [Using resource groups to manage your Azure resources](http://azure.microsoft.com/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
 Replace {job-name} with the name of the Stream Analytics job that you are stopping.  
  
 Replace {api-version} with 2015-10-01 in the URI.  
  
## Response  
 Status code: 202  
  
 This is an asynchronous operation that returns a status of 202 until the job is successfully deleted. The **Location** response header contains the URI that is used to obtain the status of the process. While the process is running, a call to the URI in the **Location** header returns a status of 202. When the process finishes, the URI in the **Location** header returns a status of 200. To get a more detailed status of the job progress, use the **Get Information about a Stream Analytics Job** operation. The job metadata returned will include a **provisioningStatus** property.  
  
  
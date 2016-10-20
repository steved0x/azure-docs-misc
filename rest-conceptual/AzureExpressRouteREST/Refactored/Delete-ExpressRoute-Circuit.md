---
title: "Delete ExpressRoute Circuit"
ms.custom: na
ms.date: 2015-09-25
ms.prod: azure
ms.reviewer: na
ms.service: expressroute
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: a5cf7b54-c74d-490b-80a1-21e064f4c1b5
caps.latest.revision: 7
author: cherylmc
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
# Delete ExpressRoute Circuit
The DELETE operation deletes an Express Route circuit.  
  
## Request  
 See Common parameters and headers for headers and parameters that are used by all requests related to ExpressRoute.  
  
|Method|Request URI|  
|------------|-----------------|  
|DELETE|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/expressRouteCircuits/{circuitName}?api-version={api-version}`|  
  
## Response  
 Status code: 202  
  
 The response returns 202 Accepted with a ‘Disabling’ provisioningState till the operation completes. The header also contains ‘Azure-AsyncOperation’ header pointing to an operations resource. The URI for Azure-AsyncOperation header is of the form - [https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Network/locations/{location}/operations/{operationId}&api-version={api-version}](https://management.azure.com/subscriptions/%7BsubscriptionId%7D/providers/Microsoft.Network/locations/%7Blocation%7D/operations/%7BoperationId%7D&api-version=%7Bapi-version%7D.).  
  
 The operation URI can be queried to find the current state of the operation.
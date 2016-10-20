---
title: "Delete ExpressRoute Circuit BGP Peering"
ms.custom: na
ms.date: 2015-09-28
ms.prod: azure
ms.reviewer: na
ms.service: expressroute
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 9e8762e5-ad43-4e3b-9153-302df957f952
caps.latest.revision: 5
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
# Delete ExpressRoute Circuit BGP Peering
The DELETE peering operation deletes the specified peering for a given circuit.  
  
## Request  
 See [Common parameters and headers](../AzureExpressRouteREST/ExpressRoute-REST.md#bk_common) for headers and parameters that are used by all requests related to *ExpressRoute*.  
  
|Method|Request URI|  
|------------|-----------------|  
|DELETE|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/expressRouteCircuits/{circuitName}/peerings/{peeringName}?api-version={api-version}`|  
  
## Response  
 **Status code: 202**  
  
 The response returns 202 Accepted with a ‘Deleting’ provisioningState till the operation completes. The header also contains ‘Azure-AsyncOperation’ header pointing to an operations resource. The URI for Azure-AsyncOperation header is of the form - https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Network/locations/{location}/operations/{operationId}&api-version={api-version}.   
The operation URI can be queried to find the current state of the operation.
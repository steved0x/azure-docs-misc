---
title: "List ExpressRoute Circuit BGP Peering"
ms.custom: na
ms.date: 2015-09-28
ms.prod: azure
ms.reviewer: na
ms.service: expressroute
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 9d78b825-8187-4103-8ac0-3ea9eac5faf2
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
# List ExpressRoute Circuit BGP Peering
The List peering operation retrieves all the BGP Peerings for the circuit specified.  
  
## Request  
 See [Common parameters and headers](../AzureExpressRouteREST/ExpressRoute-REST.md#bk_common) for headers and parameters that are used by all requests related to *ExpressRoute*.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/expressRouteCircuits/{circuitName}/peerings?api-version={api-version}`|  
  
 Replace {circuitName} with the name of the ExpressRoute circuit already created.  
  
## Response  
 **Status Code: 200**  
  
```  
[  
        {  
      "name": "AzurePrivatePeering",  
      "id": "/subscriptions/a932c0e6-b5cb-4e68-b23d-5064372c8a3c/resourceGroups/AmitCrkt7/providers/Microsoft.Network/expressRouteCircuits/amittest/peerings/Private",  
      "etag": "W/\"cb87537e-fd92-48c7-905f-2efc95a47c8f\"",  
      "properties": {  
        "provisioningState": "Succeeded",  
        "peeringType": "AzurePrivatePeering",  
        "azureASN": 12076,  
        "peerASN": 100,  
        "primaryPeerAddressPrefix": "192.168.1.0/30",  
        "secondaryPeerAddressPrefix": "192.168.2.0/30",  
        "primaryAzurePort": "BRKAZUREIXP01-BN1-04GMR-CIS-1-PRIMARY",  
        "secondaryAzurePort": "BRKAZUREIXP01-DM2-04GMR-CIS-1-SECONDARY",  
        "state": "Enabled",  
        "vlanId": 200  
      }  
    }  
]  
  
```  
  
 Following additional elements are seen when compared to the request sent in creation of BGP Peering.  
  
|Element Name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|azureASN|No|Integer|Specifies the numeric identifier of the public autonomous system (AS) in which the device is configured.|  
|primaryAzurePort|No|String|Specifies the name of the primary port. Only available when the circuit provisioning state is Provisioning or Provisioned.|  
|secondaryAzurePort|No|String|Specifies the name of the secondary port. Only available when the provisioning state is Provisioning or Provisioned.|  
|state|No|String|State of the BGP Peering in ExpressRoute. Possible values are ‘Enabled’ or ‘Disabled’|
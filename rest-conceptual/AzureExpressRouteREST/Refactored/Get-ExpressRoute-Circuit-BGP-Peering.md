---
title: "Get ExpressRoute Circuit BGP Peering"
ms.custom: na
ms.date: 2015-09-28
ms.prod: azure
ms.reviewer: na
ms.service: expressroute
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: df997501-fe0e-4dd0-9ea9-c7364021b686
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
# Get ExpressRoute Circuit BGP Peering
The Get peering operation retrieves details of a peering for the circuit and peering specified.  
  
## Request  
 See [Common parameters and headers](../AzureExpressRouteREST/ExpressRoute-REST.md#bk_common) for headers and parameters that are used by all requests related to *ExpressRoute*.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/expressRouteCircuits/{circuitName}/peerings/{peeringName}?api-version={api-version}`|  
  
 Replace {circuitName} with the name of the ExpressRoute circuit already created and {peeringName} with the name of BGP Peering whose details are to be retrieved.  
  
## Response  
 **Status Code: 200**  
  
```  
{  
    "name": "<peering name>",  
    "id": "https://<endpoint>/subscriptions/{subscriptionId}/resourceGroups/{ResourceGroupName}providers/Microsoft.Network/expressRouteCircuits/{circuitName}/peerings/{peering name}",  
    "etag": "",  
    "properties": {  
        "provisioningState": "{Succeeded | Failed | Cancelled}",  
        "peeringType": "AzurePublicPeering | AzurePrivatePeering | MicrosoftPeering",  
        "peerASN": "",  
        "primaryPeerAddressPrefix": "",  
        "secondaryPeerAddressPrefix": "",  
        "primaryAzurePort": "",  
        "secondaryAzurePort": "",  
        "state": "Disabled | Enabled",  
        "sharedKey": "",  
        "vlanId": "",  
        "microsoftPeeringConfig": {  
            "advertisedpublicprefixes": [  
                "prefix1",  
                "prefix2"  
            ],  
            "advertisedPublicPrefixState": "NotConfigured | Configuring | Configured | ValidationNeeded",  
            "customerAsn": "",  
            "routingRegistryName": ""  
        }  
    }  
}  
  
```  
  
 Following additional elements are seen when compared to the request sent in creation of BGP Peering.  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|azureASN|No|Integer|Specifies the numeric identifier of the public autonomous system (AS) in which the device is configured.|  
|primaryAzurePort|No|String|Specifies the name of the primary port. Only available when the circuit provisioning state is Provisioning or Provisioned.|  
|secondaryAzurePort|No|String|Specifies the name of the secondary port. Only available when the provisioning state is Provisioning or Provisioned.|  
|state|No|String|State of the BGP Peering in ExpressRoute. Possible values are ‘Enabled’ or ‘Disabled’|
---
title: "Get ExpressRoute Circuit"
ms.custom: na
ms.date: 2015-09-25
ms.prod: azure
ms.reviewer: na
ms.service: expressroute
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: ba245cae-c36f-4a71-ae7e-55406f44a607
caps.latest.revision: 6
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
# Get ExpressRoute Circuit
This operation fetches details of a particular circuit in a Resource Group.  
  
## Request  
 See Common parameters and headers for headers and parameters that are used by all requests related to ExpressRoute.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/expressRouteCircuits/{circuitName}?api-version={api-version}`|  
  
> [!NOTE]
>  If BGP Peerings are defined for the ExpressRoute Circuit, they are also returned as Child objects of the ExpressRoute Circuit. Refer to BGP Peerings section for details on these objects.  
  
## Response  
 Status Code: 200  
  
```  
{  
        "name": "<circuit name>",  
        "id": "/subscriptions/{subscriptionId}/resourceGroup/{resourceGroupName}/providers/Microsoft.Network/expressRouteCircuits/{circuitName}",  
        "etag": " W/\"00000000-0000-0000-0000-000000000000\"",  
        "location": "<location>",  
        "tags": {  
            "key1": "value1",  
            "key2": "value2"  
        },  
        "sku": {  
            "name": "Standard_MeteredData",  
            "tier": "Standard|Premium",  
            "family": "UnlimitedData|MeteredData"  
        },  
        "properties": {  
            "provisioningState": "Succeeded|Failed|Cancelled",  
            "circuitProvisioningState": "Enabled|Disabled|Enabling|Disabling",  
            "serviceProviderProvisioningState": "NotProvisioned|Provisioning|Provisioned|Deprovisioning",  
            "serviceProviderProperties": {  
                "serviceProviderName": "serviceProviderName",  
                "peeringLocation": "<peering location",  
                "bandwidthInMbps": 100  
            }  
        },  
        "serviceKey": "<unique service key for circuit>",  
        "serviceProviderNotes": "<notes set only by ServiceProvider>"  
    }  
  
```  
  
 Following additional elements are seen when compared to the request sent in creation of Circuit.  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|provisioningState|No|String|Specifies the provisioning state of the circuit resource in ARM. This is different from circuit state in ExpressRoute system or circuit state in service provider’s system.Valid values can be ‘Succeeded’, ‘Failed’ or ‘Cancelled’|  
|circuitProvisioningState|No|String|Specifies the provisioning state of the circuit in ExpressRoute. Valid values are ‘Enabling’, ‘Enabled’, ‘Disabling’, ‘Disabled’|  
|serviceProviderProvisioningState|No|String|Specifies the provisioning state of the Circuit in Service Provider’s system. Valid values are ‘NotProvisioned’ , ‘Provisioning’, ‘Provisioned’, ‘Deprovisioning’.|  
|serviceKey|No|String|Specifies the unique key assigned to the ExpressRoute circuit once successfully provisioned.|  
|serviceProviderNote|No|String|Additional read only notes set on this circuit by the service provider.|
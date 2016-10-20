---
title: "List Express Route Service Providers"
ms.custom: na
ms.date: 10/03/2016
ms.prod: azure
ms.reviewer: na
ms.service: expressroute
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: cbdb9707-9718-4904-9680-42d6fddd5a4c
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
# List Express Route Service Providers
This operation lists the currently supported connectivity providers, their peering locations and bandwidths offered.  
  
 *HTTP Request*  
  
|Method|Url|  
|------------|---------|  
|GET|[https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Network/expressRouteServiceProviders?api-version={api-version}](https://management.azure.com/subscriptions/%7bsubscriptionId%7d/providers/Microsoft.Network/expressRouteServiceProviders?api-version=%7bapi-version%7d)|  
  
## Response  
 Status code: 200  
  
## Example Output:  
  
```  
[  
    {  
        "name": "<providername>",  
        "peeringLocations": [  
            "location1",  
            "location2"  
        ],  
        "bandwidthsOffered": [  
            {  
                "offerName": "100Mbps",  
                "valueInMbps": 100  
            }  
        ]  
    }  
]  
  
```
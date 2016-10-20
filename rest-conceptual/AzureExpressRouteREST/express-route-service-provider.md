# Service provider

Express Route Service Providers are telcos and exchange providers who are approved in the system to provide Express Route connectivity.  

## List
Lists the currently supported connectivity providers, their peering locations and bandwidths offered.  
  
 *HTTP Request*  
  
|Method|Url|  
|------------|---------|  
|GET|[https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Network/expressRouteServiceProviders?api-version={api-version}](https://management.azure.com/subscriptions/%7bsubscriptionId%7d/providers/Microsoft.Network/expressRouteServiceProviders?api-version=%7bapi-version%7d)|  
  
### Response  
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
# Circuit

The Circuit represents the entity created by customer to register with an express route service provider with intent to connect to Microsoft. The create circuit operation also creates a unique service key that is used to establish a relationship between the customer and the Microsoft. BGP Peering is part of Express Route circuit and defines the type of connectivity needed with Microsoft. There are three peering models available for each circuit called AzurePublicPeering, AzurePrivatePeering and MicrosoftPeering.  

## Create or update

Creates or updates an ExpressRoute circuit.

### Request  
 See [Common parameters and headers](../AzureExpressRouteREST/ExpressRoute-REST.md#bk_common) for headers and parameters that are used by all requests related to ExpressRoute.  
  
|Method|Request URI|  
|------------|-----------------|  
|PUT|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/expressRouteCircuits/{circuitName}?api-version={api-version}`|  
  
 Replace {circuitName} with the name of the ExpressRoute circuit to be created.  The circuitName must be unique within the resource group.  
  
 ***Circuit without BGP Peerings specified at creation time.***  
  
```  
{  
    "name": "<circuit name>",  
    "location": "<location>",  
    "tags": {  
        "key1": "value1",  
        "key2": "value2"  
    },  
    "sku": {  
        "name": "Standard_MeteredData",  
        "tier": "Standard",  
        "family": "MeteredData"  
    },  
    "properties": {  
        "serviceProviderProperties": {  
            "serviceProviderName": "serviceProviderName",  
            "peeringLocation": "<peering location>",  
            "bandwidthInMbps": 100  
        }  
    }  
}  
  
```  
  
 **Circuit with BGP Peering specified at creation time:**  
  
```  
{  
    "name": "<circuit name>",  
    "location": "<location>",  
    "tags": {  
        "key1": "value1",  
        "key2": "value2"  
    },  
    "sku": {  
        "name": "Standard_MeteredData",  
        "tier": "Standard",  
        "family": "MeteredData"  
    },  
    "properties": {  
        "serviceProviderProperties": {  
            "serviceProviderName": "serviceProviderName",  
            "peeringLocation": "<peering location>",  
            "bandwidthInMbps": 100  
        },  
"peerings": [  
                    {  
                        "name": "AzurePublicPeering",  
                        "properties": {  
                            "peeringType": "AzurePublicPeering",  
                            "peerASN": 100,  
                            "PrimaryPeerAddressPrefix": "192.168.1.0/30",  
                            "SecondaryPeerAddressPrefix": "192.168.2.0/30",  
                            "vlanId": 200  
                        }  
                    }  
                ]  
    }  
}  
  
```  
  
> [!NOTE]
>  Refer to the [Operations on ExpressRoute BGP Peering](../AzureExpressRouteREST/Operations-on-ExpressRoute-BGP-Peering.md) section for more details on the BGP Peering parameters.  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|location|Yes|String|Specifies the geo-location of the resource. This is different from peering location.|  
|tags|Yes|Complex Type|The tags and their values to associate with the ExpressRoute Circuit, see [Using tags to organize your Azure resources](https://azure.microsoft.com/documentation/articles/resource-group-using-tags/)|  
|sku|No|Complex Type|Specifies the SKU of ExpressRoute Circuit|  
|sku:name|No|String|Sku name is concatenation of {tier}_{family}|  
|sku:tier|No|String|ExpressRoute is offered in two tiers – ‘Standard’ or ‘Premium’.|  
|sku:family|No|String|Choose from either ‘UnlimitedData’ or ‘MeteredData’|  
|serviceProviderProperties|Yes|Complex Type|Specifies the service provider details from whom the circuit is to be established.|  
|serviceProviderProperties: serviceProviderName|Yes|String|The name of the service provider. This must match the provider name from List ExpressRoute service providers call.|  
|serviceProviderProperties: peeringLocation|Yes|String|Peering location for the ExpressRoute Circuit. This must match one of the peering location for chosen service provider from List ExpressRoute service provider operation.|  
|serviceProviderProperties: bandwidthInMbps|Yes|Integer|Value of ExpressRoute circuit bandwidth in Mbps. This must match one of the bandwidths offered for the chosen service provider from List ExpressRoute service provider operation.|  
  
### Response  
 **Status code: 202**  
  
 The response returns 202 Accepted with a ‘Enabling’ circuitProvisioningState till the operation completes. The header also contains ‘Azure-AsyncOperation’ header pointing to an operations resource. The URI for Azure-AsyncOperation header is of the form -  `https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Network/locations/{location}/operations/{operationId}&api-version={api-version}`.  
  
 The operation URI can be queried to find the current state of the operation.

## Delete
Deletes an Express Route circuit.  
  
### Request  
 See Common parameters and headers for headers and parameters that are used by all requests related to ExpressRoute.  
  
|Method|Request URI|  
|------------|-----------------|  
|DELETE|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/expressRouteCircuits/{circuitName}?api-version={api-version}`|  
  
### Response  
 Status code: 202  
  
 The response returns 202 Accepted with a ‘Disabling’ provisioningState till the operation completes. The header also contains ‘Azure-AsyncOperation’ header pointing to an operations resource. The URI for Azure-AsyncOperation header is of the form - [https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Network/locations/{location}/operations/{operationId}&api-version={api-version}](https://management.azure.com/subscriptions/%7BsubscriptionId%7D/providers/Microsoft.Network/locations/%7Blocation%7D/operations/%7BoperationId%7D&api-version=%7Bapi-version%7D.).  
  
 The operation URI can be queried to find the current state of the operation.

## Get
Gets details of a particular circuit in a Resource Group.  
  
### Request  
 See Common parameters and headers for headers and parameters that are used by all requests related to ExpressRoute.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/expressRouteCircuits/{circuitName}?api-version={api-version}`|  
  
> [!NOTE]
>  If BGP Peerings are defined for the ExpressRoute Circuit, they are also returned as Child objects of the ExpressRoute Circuit. Refer to BGP Peerings section for details on these objects.  
  
### Response  
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

## List
Lists details of all the circuits, in all states, in a resource group.  
  
### Request  
 See [Common parameters and headers](../AzureExpressRouteREST/ExpressRoute-REST.md#bk_common) for headers and parameters that are used by all requests related to ExpressRoute.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/expressRouteCircuits?api-version={api-version}`|  
  
> [!NOTE]
>  If BGP Peerings are defined for the ExpressRoute Circuit, they are also returned as Child objects of the ExpressRoute Circuit. Refer to BGP Peerings sections for details on these objects.  
  
### Response  
 `Status Code: 200`  
  
```  
[  
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
]  
  
```  
  
 Following additional elements are seen when compared to the request sent in creation of Circuit.  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|provisioningState|No|String|Specifies the provisioning state of the circuit resource in ARM. This is different from circuit state in ExpressRoute system or circuit state in service provider’s system.Valid values are ‘Succeeded’, ‘Failed’ or ‘Cancelled’|  
|circuitProvisioningState|No|String|Specifies the provisioning state of the circuit in ExpressRoute. Valid values are ‘Enabling’, ‘Enabled’, ‘Disabling’, ‘Disabled’|  
|serviceProviderProvisioningState|No|String|Specifies the provisioning state of the Circuit in Service Provider’s system. Valid values are ‘NotProvisioned’ , ‘Provisioning’, ‘Provisioned’, ‘Deprovisioning’.|  
|serviceKey|No|String|Specifies the unique key assigned to the ExpressRoute circuit once successfully provisioned.|  
|serviceProviderNotes|No|String|Additional read only notes set on this circuit by the service provider.|

## Create or update BGP Peering
The create BGP Peering operation creates a new peering for the circuit specified or updates an existing peering. The PUT operation for peering can be performed both at circuit create/update operation and independently on the BGP Peering object. Similarly update to a peering can also be performed by update on parent circuit or on peering object independently  
  
 In the section below a PUT on the peering child object is shown.  
  
### Request  
 See [Common parameters and headers](../AzureExpressRouteREST/ExpressRoute-REST.md#bk_common) for headers and parameters that are used by all requests related to *ExpressRoute*.  
  
|Method|Request URI|  
|------------|-----------------|  
|PUT|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/expressRouteCircuits/{circuitName}/peerings/{peeringName}?api-version={api-version}`|  
  
 Replace {circuitName} with the name of the ExpressRoute circuit already created. Replace {peeringName} with peering to be created. It must be one of AzurePublicPeering, AzurePrivatePeering, and MicrosoftPeering. There can be only one peering of each type in a circuit.  
  
 **AzurePublicPeering:**  
  
```  
  
{  
    "name": "AzurePublicPeering",  
    "properties": {  
        "peeringType": "AzurePublicPeering",  
        "peerASN": 100,   
        "PrimaryPeerAddressPrefix": "192.168.1.0/30",  
        "SecondaryPeerAddressPrefix": "192.168.2.0/30",  
        "vlanId": 200,  
    }  
}  
  
```  
  
 **AzurePrivatePeering:**  
  
```  
  
{  
    "name": "AzurePrivatePeering",   
    "properties": {   
        "peeringType": "AzurePrivatePeering",   
        "peerASN": 100,   
        "PrimaryPeerAddressPrefix": "192.168.1.0/30",   
        "SecondaryPeerAddressPrefix": "192.168.2.0/30",  
        "vlanId": 200,  
    }  
}  
  
```  
  
 **MicrosoftPeering:**  
  
```  
  
{  
    "name": "MicrosoftPeering",  
    "properties": {  
        "peeringType": "MicrosoftPeering",  
        "peerASN": 100,  
        "primaryPeerAddressPrefix": "192.168.1.0/30",  
        "secondaryPeerAddressPrefix": "192.168.2.0/30",  
        "vlanId": 200,  
        "microsoftPeeringConfig": {  
            "advertisedpublicprefixes": [  
                "11.2.3.4/30",  
                "12.2.3.4/30"  
            ],  
            "advertisedPublicPrefixState": "NotConfigured ",  
            "customerAsn": 200,  
            "routingRegistryName": "<name>"  
        }  
    }  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|name|Yes|String|Name of the peering. Must be one of AzurePublicPeering, AzurePrivatePeering, MicrosoftPeering|  
|peeringType|Yes|String|Must be one of AzurePublicPeering, AzurePrivatePeering, MicrosoftPeering|  
|peerAsn|Yes|Integer|The autonomous system number of the customer/connectivity provider.|  
|primaryPeerAddressPrefix|Yes||/30 subnet used to configure IP addresses for interfaces on Link1|  
|secondaryPeerAddressPrefix|Yes||/30 subnet used to configure IP addresses for interfaces on Link2|  
|vlanId|Yes||Specifies the identifier that is used to identify the customer|  
|microsoftPeeringConfig|Yes|Complex Type|Properties applicable only when peering type is chosen as MicrosftPeering. The following properties should not be specified for AzurePublicPeering or AzurePrivatePeering|  
|microsoftPeeringConfig: advertisedpublicprefixes|Yes|String array|Comma separated list of prefixes that will be advertised through the BGP peering. Only routes for these prefixes will be allowed into the VPN.|  
|microsoftPeeringConfig: advertisedPublicPrefixState|No|String|Specifies the configuration state of the BGP session. One of ‘NotConfigured’, ‘Configuring’ ‘Configured’ ‘ValidationNeeded’|  
|microsoftPeeringConfig: customerAsn|||ASN of the customer (if different from peering ASN). This is used to validate the ownership of advertisedpublicprefixes in RIR/IRRs|  
|microsoftPeeringConfig: routingRegistryName|||Internet Routing Registry / Regional Internet Registry to perform a look up for routing object to validate prefixes. Supported list of RIRs / IRRs are:<br /><br /> -   ARIN<br />-   APNIC<br />-   AFRINIC<br />-   LACNIC<br />-   RIPE NCC<br />-   RADB<br />-   ALTDB<br />-   LEVEL3|  
  
### Response  
 **Status Code: 202**  
  
 The response returns 202 Accepted with a ‘Enabling’ provisioningState till the operation completes. The header also contains ‘Azure-AsyncOperation’ header pointing to an operations resource. The URI for Azure-AsyncOperation header is of the form - https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Network/locations/{location}/operations/{operationId}&api-version={api-version}. The operation URI can be queried to find the current state of the operation.

## Delete BGP Peering
Deletes the specified peering for a given circuit.  
  
### Request  
 See [Common parameters and headers](../AzureExpressRouteREST/ExpressRoute-REST.md#bk_common) for headers and parameters that are used by all requests related to *ExpressRoute*.  
  
|Method|Request URI|  
|------------|-----------------|  
|DELETE|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/expressRouteCircuits/{circuitName}/peerings/{peeringName}?api-version={api-version}`|  
  
### Response  
 **Status code: 202**  
  
 The response returns 202 Accepted with a ‘Deleting’ provisioningState till the operation completes. The header also contains ‘Azure-AsyncOperation’ header pointing to an operations resource. The URI for Azure-AsyncOperation header is of the form - https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Network/locations/{location}/operations/{operationId}&api-version={api-version}.   
The operation URI can be queried to find the current state of the operation.

## Get BGP Peering
Gets details of a peering for the circuit and peering specified.  
  
### Request  
 See [Common parameters and headers](../AzureExpressRouteREST/ExpressRoute-REST.md#bk_common) for headers and parameters that are used by all requests related to *ExpressRoute*.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/expressRouteCircuits/{circuitName}/peerings/{peeringName}?api-version={api-version}`|  
  
 Replace {circuitName} with the name of the ExpressRoute circuit already created and {peeringName} with the name of BGP Peering whose details are to be retrieved.  
  
### Response  
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

## List BGP Peering
Lists all the BGP Peerings for the specified circuit.  
  
### Request  
 See [Common parameters and headers](../AzureExpressRouteREST/ExpressRoute-REST.md#bk_common) for headers and parameters that are used by all requests related to *ExpressRoute*.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/expressRouteCircuits/{circuitName}/peerings?api-version={api-version}`|  
  
 Replace {circuitName} with the name of the ExpressRoute circuit already created.  
  
### Response  
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
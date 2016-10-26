# Application

## Create
Creates a new node on the cluster (referred to as an edge node) and installs an application on that node.  
  
### Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|PUT|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/applications/{applicationName}?api-version={api-version}`|  
  
 The following example shows the request body for installing applications on a Linux-based HDInsight cluster.  
  
```  
{  
  
	"name": “clusterName / applicationName”  
		"type": "Microsoft.HDInsight/clusters/applications",  
	"properties": {  
		"computeProfile": {  
			"roles": [  
				{  
					"name": "edgenode",  
					"targetInstanceCount": 1,  
					"hardwareProfile": {  
						"vmSize": "Standard_D3"  
					}  
				}  
			]  
		},  
		"installScriptActions": [  
			{  
				"name": "hue-install",  
				"uri": "https://publicEndpoint-bash-file.sh",  
				“parameters”: “”,  
				"roles": ["edgenode"]  
			}  
		],  
		"uninstallScriptActions": [  
			{  
				"name": "hue-uninstall",  
				"uri": "https://publicEndpoint-bash-file.sh",  
				“parameters”: “”,  
				"roles": ["edgenode"]  
			}  
		],  
		"httpsEndpoints": [  
			{  
				"subDomainSuffix": "abc",  
				"destinationPort": 8888,  
				"accessModes": ["WebPage"]  
			},  
			{  
				"subDomainSuffix": "was",  
				"destinationPort": 50073,  
				"accessModes": ["WebPage"]  
			}  
		],  
		"applicationType": "CustomApplication"  
	}  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|name|Yes|String|Specifies the name of the application. The name must be specified as *clusterName/applicationName.* Application name must be unique per cluster.|  
|type|Yes|String|Specifies the type of the resource.|  
|[Properties](#bk_props)|Yes|Complex Type|Specifies the properties of the cluster.|  
  
####  <a name="bk_props"></a> Properties  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|[computeProfile](#bk_computeprof)|Yes|Complex Type|Describes the VM the application will run on|  
|[InstallScriptActions](#bk_installscriptaction)|Yes|Complex Type|Describes the install script actions for the application. At least one script must be specified and the scripts must be idempotent, which means the scripts can be called repeatedly while producing the same result.|  
|[UninstallScriptActions](#bk_uninstallscriptaction)|No|Complex Type|Describes the uninstall script actions for the application. This is optional, but any uninstall script actions specified must be idempotent (which means the scripts can be called repeatedly while producing the same result).|  
|[HttpEndpoint](#bk_httpendpoint)|No|Complex Type|Describes which endpoints on the application should be Internet addressable.|  
|applicationType|Yes|String|This should always be set to “CustomApplication”|  
  
####  <a name="bk_computeprof"></a> computeProfile  
 This should contain exactly one role  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|[role](#bk_role)|Yes|Complex  Type|Specifies information about roles in the cluster|  
  
#####  <a name="bk_role"></a> role  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|name|Yes|String|The name must be specified as "edgenode"|  
|targetInstanceCount|Yes|Integer|This must be set to 1|  
|[hardwareProfile](#bk_hardwareprof)|Yes|Complex Type|Specifies information about the hardware profile for the edgenode|  
  
#####  <a name="bk_hardwareprof"></a> hardwareProfile  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|vmSize|Yes|String|Specifies the size of the VM. Refer to [HDInsight configuration options](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-provision-linux-clusters/#basic-configuration-options) (once on this link, scroll down to **Node pricing tiers**) for valid sizes|  
  
####  <a name="bk_installscriptaction"></a> InstallScriptActions  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|Name|Yes|String|Specifies the name of the script action. Must be unique across all persisted script actions on cluster|  
|Uri|Yes|String|Publicly accessible location of the script. All scripts specified must be idempotent, which means the scripts can be called repeatedly while producing the same result.|  
|Parameters|No|String|Optional set of parameters to pass to the script|  
|Roles|Yes|Array of Strings|Describes the role for the script to run on. Valid values are: **headnode**, **workernode**, **zookeepernode**, and **edgenode**. edgenode is the role hosting the application and where your application will run.|  
  
####  <a name="bk_uninstallscriptaction"></a> UninstallScriptActions  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|Name|Yes|String|Specifies the name of the script action.|  
|Uri|Yes|String|Publicly accessible location of the script. Any scripts specified must be idempotent, which means the scripts can be called repeatedly while producing the same result.|  
|Parameters|No|String|Optional set of parameters to pass to the script|  
|Roles|Yes|Array of Strings|Describes the role for the script to run on. Valid values are: **headnode**, **workernode**, **zookeepernode**, and **edgenode**. edgenode is the role hosting the application and where your application will run.|  
  
####  <a name="bk_httpendpoint"></a> HttpEndpoint  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|subDomainSuffix|Yes|String|A three-character alphanumeric string used to build the DNS name used to access the application. The DNS name will be of the format: *\*.apps.azurehdinsight.net*. This must be unique per cluster.|  
|destinationPort|Yes|Integer|The port to forward HTTP traffic to on the edgenode hosting your application.|  
|accessModes|No|Array of Strings|Metadata about the endpoint. If the endpoint hosts a Web page, specify **webpage** as an access mode. Otherwise, the array should be empty or not present in the payload. This will enable the Azure Portal to display direct links to your application.|  
  
### Response  
 If validation is complete and the request is accepted, the operation will return 200 (OK).  
  
 **Status code:** 200 OK


## Get
Gets details about an HDInsight application.  
  
### Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/applications/{applicationName}?api-version={api-version}`|  
  
### Response  
 Response body is an array of HDInsight application details or a single HDInsight application detail if applicationName is provided. Below is an example of application detail.  
  
 **Response code**: HTTP 200 (OK) on successful completion of the operation.  
  
 Example response:  
  
```  
{  
	“ value”: [  
		{  
			“			id”: “resourceId”  
				"name": “clusterName / applicationName”  
				"type": "Microsoft.HDInsight/clusters/applications",  
			“etag”: “etagValue”  
			“ tags”: null,  
			"properties": {  
				"computeProfile": {  
					"roles": [  
						{  
							"name": "edgenode",  
							"targetInstanceCount": 1,  
							"hardwareProfile": {  
								"vmSize": "Standard_D3"  
							}  
						}  
					]  
				},  
				"installScriptActions": [  
					{  
						"name": "hue-install",  
						"uri": "https://publicEndpoint-bash-file.sh",  
						“parameters”: “”,  
						"roles": ["edgenode"]  
					}  
				],  
				"uninstallScriptActions": [  
					{  
						"name": "hue-uninstall",  
						"uri": "https://publicEndpoint-bash-file.sh",  
						“parameters”: “”,  
						"roles": ["edgenode"]  
					}  
				],  
				"httpsEndpoints": [  
					{  
						"subDomainSuffix": "abc",  
						"destinationPort": 8888,  
						"accessModes": ["WebPage"]  
					},  
					{  
						"subDomainSuffix": "was",  
						"destinationPort": 50073,  
						"accessModes": ["WebPage"]  
					}  
				],  
				"provisioningState": "Succeeded",  
				"applicationState": "Running",  
				"createdDate": "CreatedDate",  
				"applicationType": "CustomApplication",  
				"marketplaceIdentifier": "HueV1"  
			}  
		]  
	}  
  
```



## Remove
Removes an HDInsight application from the cluster.  
  
### Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|DELETE|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/applications/{applicationName}?api-version={api-version}`|  
  
### Response  
 The operation will return 202 (Accepted) if the request is completed successfully  
  
 **Status code:** 202 Accepted.

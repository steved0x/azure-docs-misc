# Cluster

## Create
Creates a cluster in the specified subscription.  
  
###  <a name="bk_createrequest"></a> Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|PUT|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}?api-version={api-version}`|  
  
 The following example shows the request body for creating a Linux based hadoop cluster. For examples of creating clusters in other ways, see the Examples section below.  
  
```  
{  
    id":"/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.HDInsight/clusters/mycluster",  
  "name":"mycluster",   
  "type":"Microsoft.HDInsight/clusters",  
  
    "location": "location-name",  
    "tags": { "tag1": "value1", "tag2": "value2" },  
    "properties": {  
        "clusterVersion": "3.2",  
        "osType": "Linux",  
        "clusterDefinition": {  
            "kind": "hadoop",  
  
            "configurations": {  
                "gateway": {  
                    "restAuthCredential.isEnabled": true,  
                    "restAuthCredential.username": "http-user",  
                    "restAuthCredential.password": "password"  
                },  
  
                "core-site": {  
                    "fs.defaultFS": "wasb://container@storageaccount.blob.core.windows.net",  
                    "fs.azure.account.key.storageaccount.blob.core.windows.net": storage-account-key"  
                }  
            }  
        },  
  
        "computeProfile": {  
            "roles": [  
                {  
                    "name": "headnode",  
  
                    "targetInstanceCount": 2,  
  
                    "hardwareProfile": {  
                        "vmSize": "Large"  
                    },  
  
                    "osProfile": {  
                        "linuxOperatingSystemProfile": {  
                            "username": "username",  
                            "sshProfile": {  
                                "publicKeys": [   
                                    { "certificateData": "ssh-rsa key" }  
                                ]  
                            }  
                        }  
                    }  
                },  
                {  
                    "name": "workernode",  
  
                    "targetInstanceCount": 1,  
  
                    "hardwareProfile": {  
                        "vmSize": "Large"  
                    },  
  
                    "osProfile": {  
                        "linuxOperatingSystemProfile": {  
                            "username": "username",  
                            "sshProfile": {  
                                "publicKeys": [  
                                    { "certificateData": " ssh-rsa key" }  
                                ]  
                            }  
                        }  
                    }  
                },  
                {  
                    "name": "zookeepernode",  
  
                    "targetInstanceCount": 3,  
  
                    "hardwareProfile": {  
                        "vmSize": "Small"  
                    },  
  
                    "osProfile": {  
                        "linuxOperatingSystemProfile": {  
                            "username": "username",  
                            "sshProfile": {  
                                "publicKeys": [   
                                    { "certificateData": "ssh-rsa key" }  
                                ]  
                            }  
                        }  
                    }  
                }  
            ]  
        }  
    }  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|id|Yes|String|Specifies the resource identifier of the cluster.|  
|name|Yes|String|Specifies the name of the cluster.|  
|type|Yes|String|Specifies the type of the cluster.|  
|location|Yes|String|Specifies the supported Azure location where the cluster should be created. For more information, see [List all of the available geo-locations](https://msdn.microsoft.com/en-us/library/azure/dn790540.aspx).|  
|tags|No|String|Specifies the tags that will be assigned to the cluster. For more information about using tags, see [Using tags to organize your Azure resources](https://azure.microsoft.com/en-us/documentation/articles/resource-group-using-tags/).|  
|[Properties](#bk_props)|Yes|Complex Type|Specifies the properties of the cluster.|  
  
####  <a name="bk_props"></a> Properties  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|clusterVersion|Yes|String|Specifies the cluster version|  
|osType|Yes|String|Specifies the Operating system for the cluster.<br /><br /> Valid values are **Linux** and **Windows**|  
|[clusterDefinition](#bk_clusterdef)|Yes|Complex  Type|Specifies information about the cluster type and configurations|  
|[computeProfile](#bk_computeprof)|Yes|Complex Type|Specifies information about the cluster topology and associated role properties|  
  
####  <a name="bk_clusterdef"></a> clusterDefinition  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|kind|Yes|String|Specifies the cluster type.<br /><br /> Valid values are hadoop, hbase, storm & spark|  
|configurations|Yes|Dictionary|This is a dictionary of configuration type and its associated value dictionary.<br /><br /> gateway configuration type is used to configure the http user used for connecting to web api;s and the ambari portal<br /><br /> core-site configuration type is used to configure the default storage account for the cluster|  
  
####  <a name="bk_computeprof"></a> computeProfile  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|clusterVersion|Yes|String|Specifies the cluster version|  
|[role](#bk_role)|Yes|Array of Complex  Type (role)|Specifies information about roles in the cluster|  
  
####  <a name="bk_role"></a> role  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|name|Yes|String|Specifies the role name|  
|targetInstanceCount|Yes|Integer|Specifies the target instance count for the role|  
|[hardwareProfile](#bk_hardwareprof)|Yes|Complex Type|Specifies information about the hardware profile for the role|  
|[osProfile](#bk_osprof)|Yes|Complex Type|Specifies information about the os profile for the role|  
  
####  <a name="bk_hardwareprof"></a> hardwareProfile  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|vmSize|Yes|String|Specifies the size of the VM. Refer to [HDInsight configuration options](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-provision-linux-clusters/#basic-configuration-options) (once on this link, scroll down to **Node pricing tiers**) for valid sizes|  
  
####  <a name="bk_osprof"></a> osProfile  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|[linuxOperatingSystemProfile](#bk_linuxop)|No|Complex  Type|Specifies the linux OS related settings|  
|[windowsOperatingSystemProfile](#bk_windowsop)|No|Complex Type|Specifies windows OS related settings|  
|[virtualNetworkProfile](#bk_virtualnet)|No|Complex  Type|Specifies virtual network related settings if the cluster is being deployed in a virtual network in the user’s subscription|  
|[scriptActions](#bk_scriptactions)|No|Array of Complex Type|List of script actions to execute on the cluster|  
  
####  <a name="bk_linuxop"></a> linuxOperatingSystemProfile  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|Username|Yes|String|SSH user name|  
|[sshProfile](#bk_sshprofile)|No|Complex Type|Specifies the SSH key.<br /><br /> One of sshProfile or Password is required.|  
|Password|No|String|Specifies the SSH password<br /><br /> One of sshProfile or Password is required.|  
  
####  <a name="bk_sshprofile"></a> sshProfile  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|publicKeys|Yes|Array|Contains a list of certificateData objects. The value is a ssh-rsa public key|  
  
####  <a name="bk_windowsop"></a> windowsOperatingSystemProfile  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|[rdpSettings](#bk_rdpsettings)|No|Complex  Type|Specifies RDP settings for windows clusters|  
  
####  <a name="bk_rdpsettings"></a> rdpSettings  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|username|Yes|String|Specifies the RDP user name|  
|password|Yes|String|Specifies the password for the RDP user|  
|expiryDate|Yes|Date|Expiry date for the RDP credentials|  
  
####  <a name="bk_virtualnet"></a> virtualNetworkProfile  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|id|Yes|String|Virtual Network Resource Id|  
|subnet|Yes|String|Specifies the subnet name|  
  
####  <a name="bk_scriptactions"></a> scriptActions  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|name|Yes|String|Friendly name for the script action|  
|uri|Yes|String|URL to the script action file|  
|parameters|No|String|Arguments to pass when executing the script action file|  
  
### Response  
 If validation is complete and the request is accepted, the operation will return 200 (OK).  
  
 **Status code:** 200 OK  
  
 **Response body for a linux cluster creates using ssh key:**  
  
```  
{  
    id":"/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.HDInsight/clusters/mycluster",  
  "name":"mycluster",   
  "type":"Microsoft.HDInsight/clusters",  
  
    "location": "location-name",  
    "tags": { "tag1": "value1", "tag2": "value2" },  
    "properties": {  
        "clusterVersion": "3.2",  
        "osType": "Linux",  
		“provisioningState”: “InProgress”,  
		“clusterState”: “Accepted”,  
		“createdDate”: “2015-09-23”,  
		“quotaInfo”: {  
			“coresUsed”: 20  
}  
        "clusterDefinition": {  
            "kind": "hadoop"  
        },  
  
        "computeProfile": {  
            "roles": [  
                {  
                    "name": "headnode",  
  
                    "targetInstanceCount": 2,  
  
                    "hardwareProfile": {  
                        "vmSize": "Large"  
                    }  
  
                },  
                {  
                    "name": "workernode",  
  
                    "targetInstanceCount": 1,  
  
                    "hardwareProfile": {  
                        "vmSize": "Large"  
                    }  
                },  
                {  
                    "name": "zookeepernode",  
  
                    "targetInstanceCount": 3,  
  
                    "hardwareProfile": {  
                        "vmSize": "Small"  
                    }  
                }  
            ]  
        }  
    }  
}  
  
```  
  
|Element name|Type|Description|  
|------------------|----------|-----------------|  
|provisioningState|String|Indicates the current provisioning state.|  
|clusterState|String|Indicates the more detailed HDInsight cluster state while provisioning is in progress.|  
|createdDate|Date|Datetime when the cluster create request was received|  
|quotaInfo|Complex  Type|Specifies the coresUsed by the cluster|  
|errors|Array of error messgaes|Contains the error message if provisioningState = ‘failed”|  
|[connectivityEndpoints](#bk_conend)|Complex Type|Specifies the public endpoints for the cluster|  
  
####  <a name="bk_conend"></a> connectivityEndpoints  
  
|Element name|Type|Description|  
|------------------|----------|-----------------|  
|name|String|Friendly name for the connectivity endpoint|  
|protocol|String|Specifies the Protocol to use (example: HTTPS, SSH)|  
|location|String|Specifies the URL to connect|  
|port|int|Specifies the port to connect|


## Delete
Deletes an HDInsight cluster.  
  
### Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|DELETE|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}?api-version={api-version}`|  
  
### Response  
 HTTP 202 (Accepted) to indicate that the operation will complete asynchronously. Async polling will return a 204 (NoContent) once the operation completes successfully.  
  
### Remarks  
 To track progress of a delete cluster request, see [Asynchronous Operations (202 Accepted and Location header)](../HDInsightREST/asynchronous-operations--202-accepted-and-location-header-.md)


## Get
Gets the details/properties of the specified cluster.  
  
### Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}?api-version={api-version}`|  
  
###  <a name="bk_response"></a> Response  
 The operation will return 200 (OK) if the request is completed successfully  
  
 **Status code:** 200 OK  
  
 Response body is the same as create cluster.  
  
 **Response body for linux cluster details**  
  
```  
{  
    id":"/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.HDInsight/clusters/mycluster",  
  "name":"mycluster",   
  "type":"Microsoft.HDInsight/clusters",  
  
    "location": "location-name",  
    "tags": { "tag1": "value1", "tag2": "value2" },  
    "properties": {  
        "clusterVersion": "3.2",  
        "osType": "Linux",  
		“provisioningState”: “InProgress”,  
		“clusterState”: “Accepted”,  
		“createdDate”: “2015-09-23”,  
		“quotaInfo”: {  
			“coresUsed”: 20  
}  
        "clusterDefinition": {  
            "kind": "hadoop"  
        },  
  
        "computeProfile": {  
            "roles": [  
                {  
                    "name": "headnode",  
  
                    "targetInstanceCount": 2,  
  
                    "hardwareProfile": {  
                        "vmSize": "Large"  
                    },  
                    "osProfile": {  
                       "linuxOperatingSystemProfile": {  
                          "username": "sshuser"  
                       }  
                     }  
  
                },  
                {  
                    "name": "workernode",  
  
                    "targetInstanceCount": 1,  
  
                    "hardwareProfile": {  
                        "vmSize": "Large"  
                    },  
  
                    "osProfile": {  
                       "linuxOperatingSystemProfile": {  
                          "username": "sshuser"  
                       }  
                     }  
  
                },  
                {  
                    "name": "zookeepernode",  
  
                    "targetInstanceCount": 3,  
  
                    "hardwareProfile": {  
                        "vmSize": "Small"  
                    },  
  
                    "osProfile": {  
                       "linuxOperatingSystemProfile": {  
                          "username": "sshuser"  
                       }  
                     }  
                }  
            ]  
        }  
    }  
}  
  
```  
  
|Element name|Type|Description|  
|------------------|----------|-----------------|  
|provisioningState|String|Indicates the current provisioning state.|  
|clusterState|String|Indicates the more detailed HDInsight cluster state while provisioning is in progress.|  
|createdDate|Date|Datetime when the cluster create request was received|  
|quotaInfo|Complex  Type|Specifies the coresUsed by the cluster|  
|errors|Array of error messgaes|Contains the error message if provisioningState = ‘failed”|  
|[connectivityEndpoints](#connectivityEndpoints)|Complex Type|Specifies the public endpoints for the cluster|  
  
####  <a name="connectivityEndpoints"></a> connectivityEndpoints  
  
|Element name|Type|Description|  
|------------------|----------|-----------------|  
|name|String|Friendly name for the connectivity endpoint|  
|protocol|String|Specifies the Protocol to use (example: HTTPS, SSH)|  
|location|String|Specifies the URL to connect|  
|port|int|Specifies the port to connect|


## Get configurations
Gets cluster configuration details.  
  
### Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/configurations?api-version={api-version}`|  
  
### Response  
 HTTP 200 (OK) on successful completion of the operation.  
  
 Example response:  
  
```  
"configurations":   
{  
   “gateway”: {  
     “restAuthCredential.isEnabled”: true,  
     "restAuthCredential.username": "user",  
     "restAuthCredential.password": "password here"     
   },  
  
   "core-site": {  
	   “key1”: “value1”  
   }  
}  
  
```  
  
|Element name|Type|Description|  
|------------------|----------|-----------------|  
|configurations|Dictionary|This is a dictionary of configuration type and its associated value dictionary.  <br />gateway configuration type is used to configure the http user used for connecting to web api;s and the ambari portal  <br />core-site configuration type is used to configure the default storage account for the cluster|


## Get configuration
Gets details about a single configuration type.  
  
### Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/configurations/{configurationType}?api-version={api-version}`|  
  
### Response  
 HTTP 200 (OK) on successful completion of the operation.  
  
 Example response:  
  
```  
“gateway”: {  
     “restAuthCredential.isEnabled”: true,  
     "restAuthCredential.username": "user",  
     "restAuthCredential.password": "password here"     
   }  
  
```






# List by resource group
Lists all the clusters in the user’s subscription in the specified resource group.  
  
### Request  
 See  [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://management.azure.com/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupId}/providers/Microsoft.HDInsight/clusters?api-version={api-version}`|  
  
### Response  
 The operation will return 200 (OK) if the request is completed successfully.  
  
 **Status code**: 200 OK  
  
 Response body is an array of cluster details. For more information, see [Get cluster properties](../HDInsightREST/get-cluster-properties.md).  
  
```  
{  
  “value”: [  
		{ Cluster details }  
    ]  
}  
  
```


## List by subscription
Lists all the clusters in the user’s subscription.  
  
### Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.HDInsight/clusters?api-version={api-version}`|  
  
### Response  
 The operation will return 200 (OK) if the request is completed successfully.  
  
 **Status code:** 200 OK  
  
 Response body is an array of cluster details.  
  
```  
{  
  “value”: [  
		{ Cluster details }  
    ]  
}  
```


## Change connectivity settings
This operation allows users to enable/disable the HTTPS connectivity to the cluster.  
  
### Request  
 See [Common parameters and headers](../HDInsightREST/clusters.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|POST|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/configurations/{configurationType}?api-version={api-version}`|  
  
 **To enable connectivity**  
  
```  
{  
   "restAuthCredential.isEnabled": true,  
   "restAuthCredential.username": "user",  
   "restAuthCredential.password": "password here"  
}  
  
```  
  
 **To disable connectivity**  
  
```  
{  
   "restAuthCredential.isEnabled": false  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|restAuthCredential.isEnabled|Yes|Boolean|Specifies if connectivity should be enabled or disabled|  
|restAuthCredential.username|No|String|Required if isEnabled=true <br />Specifies the username for connectivity settings|  
|restAuthCredential.password|No|String|Required if isEnabled=true <br />Specifies the password for connectivity settings|  
  
### Response  
 HTTP 202 (Accepted) to indicate that the operation will complete asynchronously. Async polling will return a 204 (NoContent) once the operation completes successfully.  
  
### Remarks  
 To track progress of a delete cluster request, see [Asynchronous Operations (202 Accepted and Location header)](../HDInsightREST/asynchronous-operations--202-accepted-and-location-header-.md)


## Change RDP settings (Windows cluster only)
This operation allows a user to enable/disable RDP. It applies to Windows based clusters.  
  
### Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|POST|https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/changerdpsetting?api-version={api-version}|  
  
 **Request Body**  
  
 **To enable RDP**  
  
```  
{  
	"osProfile": {  
        "windowsOperatingSystemProfile": {  
        	"rdpSettings": {  
        	      "username": "username",  
            	      "password": "password here",  
            	      "expiryDate": "YYYY-MM-DD"  
        	}  
        }  
    }  
}  
```  
  
 **To disable RDP**  
  
```  
{  
	"osProfile": {  
        "windowsOperatingSystemProfile": {  
        	"rdpSettings": null  
        }  
    }  
}  
```  
  
#### osProfile  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|[windowsOperatingSystemProfile](#windowsOperatingSystemProfile)|No|Complex Type|Specifies windows OS related settings|  
  
####  <a name="windowsOperatingSystemProfile"></a> windowsOperatingSystemProfile  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|[rdpSettings](#rdpSettings)|No|Complex Type|Specifies RDP settings for windows clusters|  
  
####  <a name="rdpSettings"></a> rdpSettings  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|username|Yes|String|Specifies the RDP user name|  
|password|Yes|String|Specifies the password for the RDP user|  
|expiryDate|Yes|Date|Expiry date for the RDP credentials|  
  
### Response  
 The operation will return 200 (OK) if the request is completed successfully  
  
 **Status code:** 200 OK  
  
 Response body is the same as [Create a cluster](../HDInsightREST/create-a-cluster.md).


## Run Script Actions on a running cluster (Linux cluster only)
Execute Script action on a running cluster.  
  
### Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|POST|https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/executeScriptActions?api-version={api-version}|  
  
 **Request Body**  
  
```  
{  
  "scriptActions": [  
    {  
      "name": "script-name",  
      "uri": "script-uri",  
      "parameters": "script-parameters",  
      "roles": [  
        "headnode",  
        "workernode"  
      ]  
    },  
    ...  
  ],  
  "persistOnSuccess": true  
}  
  
```  
  
####  <a name="rdpSettings"></a> scriptActions  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|name|Yes|String|Specifies the name of the script action|  
|uri|Yes|String|Specifies the URI of the script action|  
|parameters|Yes|String|Specifies the parameters required by the script ation|  
|roles|Yes|Array of String|Specifies the target roles that the script action executes on|  
|persistOnSuccess|Yes|Boolean|Specifies whether the script actions will be persisted after successful executions|  
  
### Response  
 If validation is complete and the request is accepted, the operation will return 202 (Accepted).  
  
 **Status code:** 202 (Accepted)


## List all persisted Script Actions for a cluster (Linux cluster only)
This operation returns all the persisted scripts actions of the specified cluster.  
  
### Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/scriptActions?api-version={api-version}|  
  
### Response  
 HTTP 200 (OK) on successful completion of the operation.  
  
 **Status code:** 200 OK  
  
 Example response:  
  
```  
{  
"value":  
[  
  {  
    "name":"script-name",  
    "uri":"script-uri",  
    "parameters":"script-parameters",  
    "roles":["headnode","workernode"],  
    "applicationName":null  
  },  
  ...  
]  
}  
```  
  
|Element name|Type|Description|  
|------------------|----------|-----------------|  
|name|String|Specifies the name of the script action.|  
|uri|String|Specifies the URI of the script action.|  
|parameters|String|Specifies the parameters required by the script action|  
|roles|Array of String|Specifies the targeted roles that the script action executes on.|  
|applicationName|String|Specifies the corresponding application that the script is associated with. applicationName is null if the script is provided by users|


## Remove a persisted Script Action for a cluster (Linux cluster only)
This operation removes an HDInsight persisted script action for a cluster.  
  
### Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|DELETE|https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/scriptActions/{scriptName}?api-version={api-version}|  
  
### Response  
  
-   HTTP 200 (OK) to indicate that the script action has been removed from the list of persisted script actions.  
  
-   HTTP 404 (NotFound) to indicate that there is no existing persisted script action with corresponding scriptName.


## Get Script Action execution from history (Linux clusters only)
This operation returns latest scripts action execution of the specified cluster or execution details for an individual script execution.  
  
### Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/scriptExecutionHistory/{scriptExecutionId}?api-version={api-version}|  
  
### Response  
 The operation will return 200 (OK) if the request is completed successfully. Response body is an array of script execution details or a single script execution details if scriptExecutionId is provided. Below is an example of a script execution detail.  
  
 **Status code:** 200 (OK)  
  
 Example response:  
  
```  
{  
  "scriptExecutionId":script-execution-id,  
  "name":"script-name",  
  "applicationName":null,  
  "uri":"script-uri",  
  "parameters":"script-parameters",  
  "roles":["headnode","workernode"],  
  "startTime":"2016-02-26T23:49:13.0773637Z",  
  "endTime":"2016-02-26T23:49:33.4964725Z",  
  "status":"Succeeded",  
  "operation":"PostClusterCreateScriptActionRequest",  
  "executionSummary":  
	[{"status":"COMPLETED",  
	 "instanceCount":4}],  
  "debugInformation": "debug-information"  
}  
  
```  
  
|Element name|Type|Description|  
|------------------|----------|-----------------|  
|scriptExecutionId|Long|Specifies the execution id of the script action.|  
|name|String|Specifies the name of the script action.|  
|applicationName|String|Specifies the corresponding application that the script is associated with. applicationName is null if the script is provided by users|  
|uri|String|Specifies the URI of the script action.|  
|parameters|String|Specifies the parameters required by the script action|  
|roles|Array of String|Specifies the targeted roles that the script action executes on.|  
|startTime|DateTime|Specifies the start time of the script action execution|  
|endTime|DateTime|Specifies the end time of the script action execution|  
|status|String|Specifies the status of the script action execution|  
|operation|String|Specifies the reason why the script action was executed. E.g: ScaleUp means that the script action was executed during cluster scale up.|  
|executionSummary|Array of complex type|Specifies the summary of execution in terms of how many hosts succeeded and how many hosts failed to execute the script.|  
|debugInformation|String|Specifies detailed debug information for the script. debugInformation is returned only when a scriptExecutionId is provided in the request.|  
  
#### executionSummary  
  
|Element name|Type|Description|  
|------------------|----------|-----------------|  
|status|String|Specifies the status of the execution on individual hosts.|  
|instanceCount|Int|Specifies the number of executions with corresponding status.|


## Promote a script from Script Action execution history to be persisted (Linux cluster only)
This operation promotes an HDInsight script from script execution history to be persisted.  
  
### Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|POST|https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/scriptExecutionHistory/{scriptExecutionId}/promote?api-version={api-version}|  
  
### Response  
  
-   HTTP 200 (OK) to indicate that the script action has been promoted.  
  
-   HTTP 404 (NotFound) to indicate that there is no existing script action execution with corresponding scriptExecutionId.


## Resize
Resizes an existing HDInsight cluster.  
  
### Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|POST|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/roles/{rolename}/resize?api-version={api-version}`|  
  
 Following shows an example request to update tags for a cluster  
  
```  
{  
    "targetInstanceCount": 10  
}  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|targetInstanceCount|Yes|Int|Specifies the new instance count for the role|  
  
### Response  
 HTTP 202 (Accepted) to indicate that the operation will complete asynchronously. Async polling will return a 204 (NoContent) once the operation completes successfully.  
  
### Remarks  
 To track progress of a delete cluster request, see [Asynchronous Operations (202 Accepted and Location header)](../HDInsightREST/asynchronous-operations--202-accepted-and-location-header-.md)


## Update
Updates tags for a cluster.  
  
 All other updates are separate actions described separately.  
  
### Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|PATCH|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}?api-version={api-version}`|  
  
 Following shows an example request to update tags for a cluster  
  
```  
{   
    "tags": {"department": "finance"}  
}  
  
```  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|tags|Yes|String|Specifies the tags that will be assigned to the cluster. For more information about using tags, see [Using tags to organize your Azure resources](https://azure.microsoft.com/en-us/documentation/articles/resource-group-using-tags/).|  
  
### Response  
 The operation will return 200 (OK) if the request is completed successfully.  
  
 **Status code:** 200 OK  
  
 Response body is the same as [Create a cluster](../HDInsightREST/create-a-cluster.md).


## Validate creation request
This operation allows users to validate the request to create a cluster. If the submitted request has some errors, the API returns an error information about properties that have invalid or missing values.  
  
### Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|PUT|`https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.HDInsight/locations/{location}/validateCreateRequest?api-version={api-version}`|  
  
 The request body for this operation will be the same as that for [Request](../HDInsightREST/create-a-cluster.md#bk_createrequest).  If any of the required properties is null or missing, the API still tries to validate the remaining properties and provide actionable error messages. Below is an example of the request body of a cluster creation request with some missing and invalid fields:  
  
```  
{  
	"name": "testcluster",  
	"location": "East Asia",  
	"tags": null,  
	"properties": {  
		"computeProfile": {  
			"roles": [  
				{  
					"osProfile": {  
						"linuxOperatingSystemProfile": {  
							"username": "newuser",  
							"password": null,  
							"sshProfile": {  
								"publicKeys": [  
									{  
										"certificateData": "ssh-rsaf8qHAOW8N75K11VVL/RiOuPkMEfHULlgzK "  
									}  
								]  
							}  
						}  
					}  
				}  
			]  
		}  
	}  
}  
  
```  
  
 In the above request, several required fields such as `clusterVersion`, `clusterDefinition`, `roleName`, and `hardwareProfile` are empty. Also, the SSH public key is invalid. The API will report all the invalid properties.  
  
### Response  
 **Status code:** 200 OK to indicate that the request is valid.  
  
 The response can contain validation warnings even if the return code is 200. In case there are any validation errors, HTTP 400 (Bad Request) is returned.  
  
```  
{  
  
	"validationErrors": [  
  
		{  
  
			"errorSource": "$.properties.clusterVersion",  
  
			"code": "ClusterVersionRequired",  
  
			"message": "'clusterVersion' cannot be null or empty"  
  
		},  
  
		{  
  
			"errorSource": "$.properties.clusterDefinition",  
  
			"code": "ClusterDefinitionRequired",  
  
			"message": "'clusterDefinition' cannot be null"  
  
		},  
  
		{  
  
			"errorSource": "$.properties.computeProfile.roles[0].name",  
  
			"code": "RoleNameRequired",  
  
			"message": "Role 'name' cannot be null or empty"  
  
		},  
  
		{  
  
			"errorSource": "$.properties.computeProfile.roles[0].hardwareProfile",  
  
			"code": "HardwareProfileRequired",  
  
			"message": "'hardwareProfile' cannot be null"  
  
		},  
  
		{  
  
			"errorSource": "$.properties.computeProfile.roles[0].osProfile.linuxOperatingSystemProfile.sshProfile",  
  
			"code": "InvalidSshPublicKey",  
  
			"message": "ssh-rsaf8qHAOW8N75K11VVL/RiOuPkMEfHULlgzK is not a valid SSH public key",  
  
			"messageArguments": ["ssh-rsaf8qHAOW8N75K11VVL/RiOuPkMEfHULlgz"]  
  
		},  
  
		{  
  
			"errorSource": "$.properties.computeProfile.roles[0].targetInstanceCount",  
  
			"code": "InvalidTargetInstanceCountValue",  
  
			"message": "'targetInstanceCount' has an invalid value. It must be greater than zero"  
  
		}  
  
	],  
  
	"validationWarnings": [  
  
		{  
  
			"errorSource": "$.properties.clusterVersion",  
  
			"code": "ClusterVersionDeprecated",  
  
			"message": "'clusterVersion' 2.0 is deprecated and will be removed in future ",  
  
			"messageArguments": ["2.0"]  
  
		}  
  
	]  
  
}  
  
```  
  
|Element name||Description|  
|------------------|-|-----------------|  
|validationErrors|Array of complex Type [validationError](#bk_validationError)|List of validation errors|  
|validationWarnings|Array of complex Type [validationError](#bk_validationError)|List of validation warnings|  
  
####  <a name="bk_validationError"></a> validationError  
  
|Element name|Type|Description|  
|------------------|----------|-----------------|  
|code|String|Error code for the particular message|  
|errorSource|String|JsonPath of the property that caused this error.|  
|message|String|Error message|  
|messageArguments|String[]|List of arguments for this error message code. This can be used where we want to show a localized message based on the error code. This field is optional.|



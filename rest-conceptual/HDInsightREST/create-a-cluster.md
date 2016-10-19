---
title: "Create a cluster"
ms.custom: ""
ms.date: "2016-11-16"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 059254c8-c6e6-4183-b92b-ad7a7378b485
caps.latest.revision: 9
author: "nitinme"
ms.author: "nitinme"
manager: "jhubbard"
translation.priority.mt: 
  - "de-de"
  - "es-es"
  - "fr-fr"
  - "it-it"
  - "ja-jp"
  - "ko-kr"
  - "pt-br"
  - "ru-ru"
  - "zh-cn"
  - "zh-tw"
---
# Create a cluster
Create a cluster in the specified subscription.  
  
##  <a name="bk_createrequest"></a> Request  
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
  
###  <a name="bk_props"></a> Properties  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|clusterVersion|Yes|String|Specifies the cluster version|  
|osType|Yes|String|Specifies the Operating system for the cluster.<br /><br /> Valid values are **Linux** and **Windows**|  
|[clusterDefinition](#bk_clusterdef)|Yes|Complex  Type|Specifies information about the cluster type and configurations|  
|[computeProfile](#bk_computeprof)|Yes|Complex Type|Specifies information about the cluster topology and associated role properties|  
  
###  <a name="bk_clusterdef"></a> clusterDefinition  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|kind|Yes|String|Specifies the cluster type.<br /><br /> Valid values are hadoop, hbase, storm & spark|  
|configurations|Yes|Dictionary|This is a dictionary of configuration type and its associated value dictionary.<br /><br /> gateway configuration type is used to configure the http user used for connecting to web api;s and the ambari portal<br /><br /> core-site configuration type is used to configure the default storage account for the cluster|  
  
###  <a name="bk_computeprof"></a> computeProfile  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|clusterVersion|Yes|String|Specifies the cluster version|  
|[role](#bk_role)|Yes|Array of Complex  Type (role)|Specifies information about roles in the cluster|  
  
###  <a name="bk_role"></a> role  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|name|Yes|String|Specifies the role name|  
|targetInstanceCount|Yes|Integer|Specifies the target instance count for the role|  
|[hardwareProfile](#bk_hardwareprof)|Yes|Complex Type|Specifies information about the hardware profile for the role|  
|[osProfile](#bk_osprof)|Yes|Complex Type|Specifies information about the os profile for the role|  
  
###  <a name="bk_hardwareprof"></a> hardwareProfile  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|vmSize|Yes|String|Specifies the size of the VM. Refer to [HDInsight configuration options](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-provision-linux-clusters/#basic-configuration-options) (once on this link, scroll down to **Node pricing tiers**) for valid sizes|  
  
###  <a name="bk_osprof"></a> osProfile  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|[linuxOperatingSystemProfile](#bk_linuxop)|No|Complex  Type|Specifies the linux OS related settings|  
|[windowsOperatingSystemProfile](#bk_windowsop)|No|Complex Type|Specifies windows OS related settings|  
|[virtualNetworkProfile](#bk_virtualnet)|No|Complex  Type|Specifies virtual network related settings if the cluster is being deployed in a virtual network in the user’s subscription|  
|[scriptActions](#bk_scriptactions)|No|Array of Complex Type|List of script actions to execute on the cluster|  
  
###  <a name="bk_linuxop"></a> linuxOperatingSystemProfile  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|Username|Yes|String|SSH user name|  
|[sshProfile](#bk_sshprofile)|No|Complex Type|Specifies the SSH key.<br /><br /> One of sshProfile or Password is required.|  
|Password|No|String|Specifies the SSH password<br /><br /> One of sshProfile or Password is required.|  
  
###  <a name="bk_sshprofile"></a> sshProfile  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|publicKeys|Yes|Array|Contains a list of certificateData objects. The value is a ssh-rsa public key|  
  
###  <a name="bk_windowsop"></a> windowsOperatingSystemProfile  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|[rdpSettings](#bk_rdpsettings)|No|Complex  Type|Specifies RDP settings for windows clusters|  
  
###  <a name="bk_rdpsettings"></a> rdpSettings  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|username|Yes|String|Specifies the RDP user name|  
|password|Yes|String|Specifies the password for the RDP user|  
|expiryDate|Yes|Date|Expiry date for the RDP credentials|  
  
###  <a name="bk_virtualnet"></a> virtualNetworkProfile  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|id|Yes|String|Virtual Network Resource Id|  
|subnet|Yes|String|Specifies the subnet name|  
  
###  <a name="bk_scriptactions"></a> scriptActions  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|name|Yes|String|Friendly name for the script action|  
|uri|Yes|String|URL to the script action file|  
|parameters|No|String|Arguments to pass when executing the script action file|  
  
## Response  
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
  
###  <a name="bk_conend"></a> connectivityEndpoints  
  
|Element name|Type|Description|  
|------------------|----------|-----------------|  
|name|String|Friendly name for the connectivity endpoint|  
|protocol|String|Specifies the Protocol to use (example: HTTPS, SSH)|  
|location|String|Specifies the URL to connect|  
|port|int|Specifies the port to connect|
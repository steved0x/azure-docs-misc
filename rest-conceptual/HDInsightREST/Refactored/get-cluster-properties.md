---
title: "Get cluster properties"
ms.custom: ""
ms.date: "2015-11-05"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 17069c42-c33f-4787-b283-8a4960950613
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
# Get cluster properties
This operation returns the details/properties of the specified cluster.  
  
## Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}?api-version={api-version}`|  
  
##  <a name="bk_response"></a> Response  
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
  
###  <a name="connectivityEndpoints"></a> connectivityEndpoints  
  
|Element name|Type|Description|  
|------------------|----------|-----------------|  
|name|String|Friendly name for the connectivity endpoint|  
|protocol|String|Specifies the Protocol to use (example: HTTPS, SSH)|  
|location|String|Specifies the URL to connect|  
|port|int|Specifies the port to connect|
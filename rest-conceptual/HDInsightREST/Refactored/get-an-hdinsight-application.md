---
title: "Get an HDInsight application"
ms.custom: ""
ms.date: "2016-11-16"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 71415482-2a70-4669-8c5b-db1608719a00
caps.latest.revision: 5
author: "nitinme"
ms.author: "nitinme"
manager: "jhubbard"
---
# Get an HDInsight application
This operation retrieves details about an HDInsight application.  
  
## Request  
 See [Common parameters and headers](../HDInsightREST/hdinsight-resource-provider-rest.md#bk_common) for headers and parameters that are used by clusters.  
  
|Method|Request URI|  
|------------|-----------------|  
|GET|`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.HDInsight/clusters/{clustername}/applications/{applicationName}?api-version={api-version}`|  
  
## Response  
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
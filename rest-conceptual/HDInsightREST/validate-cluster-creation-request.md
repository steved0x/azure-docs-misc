---
title: "Validate cluster creation request"
ms.custom: ""
ms.date: "2016-11-16"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 04e2c316-881c-4a3b-b1a5-209fdda43e3e
caps.latest.revision: 3
author: "nitinme"
ms.author: "nitinme"
manager: "jhubbard"
---
# Validate cluster creation request
This operation allows users to validate the request to create a cluster. If the submitted request has some errors, the API returns an error information about properties that have invalid or missing values.  
  
## Request  
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
  
## Response  
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
  
###  <a name="bk_validationError"></a> validationError  
  
|Element name|Type|Description|  
|------------------|----------|-----------------|  
|code|String|Error code for the particular message|  
|errorSource|String|JsonPath of the property that caused this error.|  
|message|String|Error message|  
|messageArguments|String[]|List of arguments for this error message code. This can be used where we want to show a localized message based on the error code. This field is optional.|
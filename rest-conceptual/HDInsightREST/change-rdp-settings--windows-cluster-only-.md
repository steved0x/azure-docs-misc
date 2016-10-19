---
title: "Change RDP settings (Windows cluster only)"
ms.custom: ""
ms.date: "2015-11-05"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 65da86d9-7ad5-4e26-9c84-e4878e3f9309
caps.latest.revision: 7
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
# Change RDP settings (Windows cluster only)
This operation allows a user to enable/disable RDP. It applies to Windows based clusters.  
  
## Request  
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
  
### osProfile  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|[windowsOperatingSystemProfile](#windowsOperatingSystemProfile)|No|Complex Type|Specifies windows OS related settings|  
  
###  <a name="windowsOperatingSystemProfile"></a> windowsOperatingSystemProfile  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|[rdpSettings](#rdpSettings)|No|Complex Type|Specifies RDP settings for windows clusters|  
  
###  <a name="rdpSettings"></a> rdpSettings  
  
|Element name|Required|Type|Description|  
|------------------|--------------|----------|-----------------|  
|username|Yes|String|Specifies the RDP user name|  
|password|Yes|String|Specifies the password for the RDP user|  
|expiryDate|Yes|Date|Expiry date for the RDP credentials|  
  
## Response  
 The operation will return 200 (OK) if the request is completed successfully  
  
 **Status code:** 200 OK  
  
 Response body is the same as [Create a cluster](../HDInsightREST/create-a-cluster.md).
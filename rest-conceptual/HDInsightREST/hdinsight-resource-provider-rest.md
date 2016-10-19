---
title: "HDInsight Resource Provider REST"
ms.custom: ""
ms.date: "2015-11-17"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
applies_to: 
  - "Azure"
ms.assetid: 0a3e4947-0fa0-4d6e-8ba6-c7a4834a74b5
caps.latest.revision: 19
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
# HDInsight Resource Provider REST
Use these APIs to create and manage HDInsight resources through Azure Resource Manager. All task operations conform to the HTTP/1.1 protocol specification and each operation returns an x-ms-request-id header that can be used to obtain information about the request. You must make sure that requests made to these resources are secure. For more information, see [Authenticating Azure Resource Manager requests](https://msdn.microsoft.com/en-us/library/azure/dn790557.aspx).  
  
 These APIs allow you to create and manage an HDInsight cluster.  
  
##  <a name="bk_common"></a> Common parameters and headers  
 The following information is common to all tasks that you might do related to clusters:  
  
-   Replace {api-version} with 2015-03-01-preview  
  
-   Replace {subscription-id} with your subscription identifier in the URI.  
  
-   Replace {resource-group-name} with the resource group. For more information, see [Using Resource groups to manage your Azure resources](http://azure.microsoft.com/en-us/documentation/articles/azure-preview-portal-using-resource-groups/).  
  
-   Replace {cluster-name} with your HDInsight cluster name in the URI.  
  
-   Set the Content-Type header to **application/json**.  
  
-   Set the Authorization header to a JSON Web Token that you obtain from Azure Active Directory. For more information, see [Authenticating Azure Resource Manager requests](https://msdn.microsoft.com/en-us/library/azure/dn790557.aspx).  
  
## Tasks  
 You can do the following with resources:  
  
-   [Create a cluster](../HDInsightREST/create-a-cluster.md)  
  
-   [Validate cluster creation request](../HDInsightREST/validate-cluster-creation-request.md)  
  
-   [Get cluster configurations](../HDInsightREST/get-cluster-configurations.md)  
  
-   [Get cluster configuration type details](../HDInsightREST/get-cluster-configuration-type-details.md)  
  
-   [Get cluster properties](../HDInsightREST/get-cluster-properties.md)  
  
-   [List clusters in a resource group](../HDInsightREST/list-clusters-in-a-resource-group.md)  
  
-   [List clusters in a subscription](../HDInsightREST/list-clusters-in-a-subscription3.md)  
  
-   [Change connectivity settings](../HDInsightREST/change-connectivity-settings.md)  
  
-   [Change RDP settings (Windows cluster only)](../HDInsightREST/change-rdp-settings--windows-cluster-only-.md)  
  
-   [Run Script Actions on a running cluster (Linux cluster only)](../HDInsightREST/run-script-actions-on-a-running-cluster--linux-cluster-only-.md)  
  
-   [List all persisted Script Actions for a cluster (Linux cluster only)](../HDInsightREST/list-all-persisted-script-actions-for-a-cluster--linux-cluster-only-.md)  
  
-   [Remove a persisted Script Action for a cluster (Linux cluster only)](../HDInsightREST/remove-a-persisted-script-action-for-a-cluster--linux-cluster-only-.md)  
  
-   [Get Script Action execution from history (Linux clusters only)](../HDInsightREST/get-script-action-execution-from-history--linux-clusters-only-.md)  
  
-   [Promote a script from Script Action execution history to be persisted (Linux cluster only)](../HDInsightREST/41313b17-787f-4768-8e61-40b492452c02.md)  
  
-   [Install an HDInsight application](../HDInsightREST/install-an-hdinsight-application.md)  
  
-   [Get an HDInsight application](../HDInsightREST/get-an-hdinsight-application.md)  
  
-   [Remove an HDInsight application](../HDInsightREST/remove-an-hdinsight-application.md)  
  
-   [Update a cluster](../HDInsightREST/update-a-cluster2.md)  
  
-   [Resize cluster](../HDInsightREST/resize-cluster.md)  
  
-   [Delete a cluster](../HDInsightREST/delete-a-cluster.md)
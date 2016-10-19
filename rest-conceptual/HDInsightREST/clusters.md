---
title: "Clusters"
ms.custom: ""
ms.date: "2016-11-16"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: d89e2179-207b-44ac-abe8-d84f214781c4
caps.latest.revision: 4
author: "nitinme"
ms.author: "nitinme"
manager: "jhubbard"
---
# Clusters
These APIs allow you to create and manage an HDInsight cluster  
  
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
  
-   [Delete a cluster](../HDInsightREST/delete-a-cluster.md)  
  
-   Get information about a cluster  
  
-   Get cluster configurations  
  
-   Get cluster configuration type  
  
-   List all clusters in a resource group  
  
-   List all clusters in a region  
  
-   Get connectivity settings  
  
-   Check cluster name availability  
  
-   [Resize cluster](../HDInsightREST/resize-cluster.md)  
  
-   [Change connectivity settings](../HDInsightREST/change-connectivity-settings.md)  
  
-   [Change RDP settings (Windows cluster only)](../HDInsightREST/change-rdp-settings--windows-cluster-only-.md)  
  
-   Get capabilities
---
title: "Batch jobs"
ms.custom: ""
ms.date: "2016-11-16"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: dc047a30-9e82-46e0-af8c-ef8d60ba0d08
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
# Batch jobs
These APIs allow you to run and manage batch jobs.  
  
##  <a name="bk_common"></a> Common parameters and headers  
 The following information is common to all tasks that you might do related to clusters:  
  
-   Replace {cluster-endpoint} with the url of your cluster’s management endpoint. (e.g. foobar.azurehdinsight.net)  
  
-   Replace {batch-id} with the batch id returned on job submission.  
  
-   Set the Content-Type header to **application/json**.  
  
-   Authenticate with the endpoint using HTTP basic authentication.  
  
## Tasks  
 You can do the following with batch jobs:  
  
-   [Return all active batch jobs](../HDInsightSparkREST/return-all-active-batch-jobs.md)  
  
-   [Create a new batch job](../HDInsightSparkREST/create-a-new-batch-job2.md)  
  
-   [Get the state of a batch job](../HDInsightSparkREST/get-the-state-of-a-batch-job.md)  
  
-   [Get the full log of a batch job](../HDInsightSparkREST/get-the-full-log-of-a-batch-job.md)  
  
-   [Kill the batch job](../HDInsightSparkREST/kill-a-batch-job.md)
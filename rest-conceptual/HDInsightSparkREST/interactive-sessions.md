---
title: "Interactive sessions"
ms.custom: ""
ms.date: "2015-12-02"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "hdinsight"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 26b7ad36-07fb-4751-b589-a88889d1de5b
caps.latest.revision: 3
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
# Interactive sessions
These APIs allow you to run and manage interactive sessions.  
  
##  <a name="bk_common"></a> Common parameters and headers  
 The following information is common to all tasks that you might do related to clusters:  
  
-   Replace {cluster-endpoint} with the url of your cluster’s management endpoint. (e.g. foobar.azurehdinsight.net)  
  
-   Replace {session-id} with the session id returned on session startup.  
  
-   Set the Content-Type header to **application/json**.  
  
-   Authenticate with the endpoint using HTTP basic authentication.  
  
## Tasks  
 You can do the following with interactive sessions:  
  
-   [Return all active interactive sessions](../HDInsightSparkREST/return-all-active-interactive-sessions.md)  
  
-   [Create a new interactive session](../HDInsightSparkREST/create-a-new-interactive-session.md)  
  
-   [Get the state of an interactive session](../HDInsightSparkREST/get-the-state-of-an-interactive-session.md)  
  
-   [Submit statement(s) to an interactive session](../HDInsightSparkREST/submit-statement-s--to-an-interactive-session1.md)  
  
-   [Retrieve statement results of an interactive session](../HDInsightSparkREST/retrieve-statement-results-of-an-interactive-session.md)  
  
-   [Terminate an interactive session](../HDInsightSparkREST/terminate-an-interactive-session.md)
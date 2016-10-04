---
title: "Using Storage Analytics"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 8f0fc6bf-99ca-4343-8b19-265ff1f46a47
caps.latest.revision: 8
author: tamram
manager: carolz
translation.priority.mt: 
  - de-de
  - es-es
  - fr-fr
  - it-it
  - ja-jp
  - ko-kr
  - pt-br
  - ru-ru
  - zh-cn
  - zh-tw
---
# Using Storage Analytics
## Using Storage Analytics  
 Azure Storage Analytics enables you to collect metrics (Storage Metrics) from your Azure storage accounts and log data (Storage Logging) about requests sent to your storage account. You can use Storage Metrics to monitor the health of a storage account, and Storage Logging to diagnose and troubleshoot issues with your storage account.  
  
> [!NOTE]
>  Storage Analytics metrics are available for the Blob, Queue, Table, and File services.  
>   
>  Storage Analytics logging is available for the Blob, Queue, and Table services.  
>   
>  Storage accounts with a replication type of Zone-Redundant Storage (ZRS) do not have the metrics or logging capability enabled at this time.  
  
 Storage Analytics has a 20TB limit on the amount of stored data that is independent of the total limit for your storage account. For more information on billing and data retention policies, see [Storage Analytics and Billing](http://msdn.microsoft.com/library/hh360997.aspx). For more information on storage account limits, see [Azure Storage Scalability and Performance Targets](http://msdn.microsoft.com/library/dn249410.aspx).  
  
 For information about how to enable and view Storage Metrics data, see the topic [Enabling Storage Metrics and Viewing Metrics Data](../StorageServicesREST/Enabling-Storage-Metrics-and-Viewing-Metrics-Data.md).  
  
 For information about how to enable and access Storage Logging data, see the topic [Enabling Storage Logging and Accessing Log Data](../StorageServicesREST/Enabling-Storage-Logging-and-Accessing-Log-Data.md).  
  
 For guidance on using Storage Metrics and Storage Logging to troubleshoot storage issues, see the guide [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](http://go.microsoft.com/fwlink/?LinkID=510535).
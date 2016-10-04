---
title: "Storage Analytics and Billing"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 26c306dd-7188-4d72-a5da-33173c364ac9
caps.latest.revision: 11
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
# Storage Analytics and Billing
This topic discusses the cost of Storage Analytics and how to use metrics and logging data to understand your storage services bill.  
  
## Cost of Storage Analytics  
 Storage Analytics is enabled by a storage account owner; it is not enabled by default. All metrics data is written by the services of a storage account. As a result, each write operation performed by Storage Analytics is billable. Additionally, the amount of storage used by metrics data is also billable.  
  
 The following actions performed by Storage Analytics are billable:  
  
-   Requests to create blobs for logging  
  
-   Requests to create table entities for metrics  
  
 If you have configured a data retention policy, you are not charged for delete transactions when Storage Analytics deletes old logging and metrics data. However, delete transactions from a client are billable. For more information about retention policies, see [Setting a Storage Analytics Data Retention Policy](../StorageServicesREST/Setting-a-Storage-Analytics-Data-Retention-Policy.md).  
  
## Understanding Billable Requests  
 Every request made to an account’s storage service is either billable or non-billable. Storage Analytics logs each individual request made to a service, including a status message that indicates how the request was handled. Similarly, Storage Analytics stores metrics for both a service and the API operations of that service, including the percentages and count of certain status messages. Together, these features can help you analyze your billable requests, make improvements on your application, and diagnose issues with requests to your services. For more information about billing, see [Understanding Azure Storage Billing - Bandwidth, Transactions, and Capacity](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx).  
  
 When looking at Storage Analytics data, you can use the tables in the [Storage Analytics Logged Operations and Status Messages](../StorageServicesREST/Storage-Analytics-Logged-Operations-and-Status-Messages.md) topic to determine what requests are billable. Then you can compare your logs and metrics data to the status messages to see if you were charged for a particular request. You can also use the tables in the above topic to investigate availability for a storage service or individual API operation.  
  
## See Also  
 [Storage Analytics Logged Operations and Status Messages](../StorageServicesREST/Storage-Analytics-Logged-Operations-and-Status-Messages.md)   
 [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md)   
 [About Storage Analytics Metrics](../StorageServicesREST/About-Storage-Analytics-Metrics.md)
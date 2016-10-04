---
title: "About Storage Analytics Metrics"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: c944c107-684c-47bf-92bf-5ce32689b7ae
caps.latest.revision: 20
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
# About Storage Analytics Metrics
Storage Analytics can store metrics that include aggregated transaction statistics and capacity data about requests to a storage service. Transactions are reported at both the API operation level as well as at the storage service level, and capacity is reported at the storage service level. Metrics data can be used to analyze storage service usage, diagnose issues with requests made against the storage service, and to improve the performance of applications that use a service.  
  
 To use Storage Analytics, you must enable it individually for each service you want to monitor. You can enable it from the [Azure Management Portal](https://manage.windowsazure.com/); for details, see [How To Monitor a Storage Account](http://www.windowsazure.com/manage/services/storage/how-to-monitor-a-storage-account/). You can also enable Storage Analytics programmatically via the REST API or the client library. Use the Set Service Properties operations to enable Storage Analytics for each service.  
  
> [!NOTE]
>  Storage Analytics metrics are available for the Blob, Queue, Table, and File services.  
  
## Transaction Metrics  
 A robust set of data is recorded at hourly or minute intervals for each storage service and requested API operation, including ingress/egress, availability, errors, and categorized request percentages. You can see a complete list of the transaction details in the [Storage Analytics Metrics Table Schema](../StorageServicesREST/Storage-Analytics-Metrics-Table-Schema.md) topic.  
  
 Transaction data is recorded at two levels – the service level and the API operation level. At the service level, statistics summarizing all requested API operations are written to a table entity every hour even if no requests were made to the service. At the API operation level, statistics are only written to an entity if the operation was requested within that hour.  
  
 For example, if you perform a **GetBlob** operation on your Blob service, Storage Analytics Metrics will log the request and include it in the aggregated data for both the Blob service as well as the **GetBlob** operation. However, if no **GetBlob** operation is requested during the hour, an entity will not be written to the *$MetricsTransactionsBlob* for that operation.  
  
 Transaction metrics are recorded for both user requests and requests made by Storage Analytics itself. For example, requests by Storage Analytics to write logs and table entities are recorded. For more information on how these requests are billed, see [Storage Analytics and Billing](../StorageServicesREST/Storage-Analytics-and-Billing.md)  
  
## Capacity Metrics  
  
> [!NOTE]
>  Currently, capacity metrics are only available for the Blob service. Capacity metrics for the Table, Queue, and File services will be available in future versions of Storage Analytics.  
  
 Capacity data is recorded daily for a storage account’s Blob service, and two table entities are written. One entity provides statistics for user data, and the other provides statistics about the `$logs` blob container used by Storage Analytics. The *$MetricsCapacityBlob* table includes the following statistics:  
  
-   **Capacity**: The amount of storage used by the storage account’s Blob service, in bytes.  
  
-   **ContainerCount**: The number of blob containers in the storage account’s Blob service.  
  
-   **ObjectCount**: The number of committed and uncommitted block or page blobs in the storage account’s Blob service.  
  
 For more information about the capacity metrics, see [Storage Analytics Metrics Table Schema](../StorageServicesREST/Storage-Analytics-Metrics-Table-Schema.md).  
  
## How Metrics Are Stored  
 All metrics data for each of the storage services is stored in three tables reserved for that service: one table for transaction information, one table for minute transaction information, and another table for capacity information. Transaction and minute transaction information consists of request and response data, and capacity information consists of storage usage data. Hour metrics, minute metrics, and capacity for a storage account’s Blob service is can be accessed in tables that are named as described in the following table.  
  
|Metrics Level|Table Names|Supported for Versions|  
|-------------------|-----------------|----------------------------|  
|Hourly metrics, primary location|-   $MetricsTransactionsBlob<br />-   $MetricsTransactionsTable<br />-   $MetricsTransactionsQueue|Versions prior to 2013-08-15 only. While these names are still supported, it’s recommended that you switch to using the tables listed below.|  
|Hourly metrics, primary location|-   $MetricsHourPrimaryTransactionsBlob<br />-   $MetricsHourPrimaryTransactionsTable<br />-   $MetricsHourPrimaryTransactionsQueue<br />-   $MetricsHourPrimaryTransactionsFile|All versions. Support for File service metrics is available only in version 2015-04-05 and later.|  
|Minute metrics, primary location|-   $MetricsMinutePrimaryTransactionsBlob<br />-   $MetricsMinutePrimaryTransactionsTable<br />-   $MetricsMinutePrimaryTransactionsQueue<br />-   $MetricsMinutePrimaryTransactionsFile|All versions. Support for File service metrics is available only in version 2015-04-05 and later.|  
|Hourly metrics, secondary location|-   $MetricsHourSecondaryTransactionsBlob<br />-   $MetricsHourSecondaryTransactionsTable<br />-   $MetricsHourSecondaryTransactionsQueue|All versions. Read-access geo-redundant replication must be enabled.|  
|Minute metrics, secondary location|-   $MetricsMinuteSecondaryTransactionsBlob<br />-   $MetricsMinuteSecondaryTransactionsTable<br />-   $MetricsMinuteSecondaryTransactionsQueue|All versions. Read-access geo-redundant replication must be enabled.|  
|Capacity (Blob service only)|$MetricsCapacityBlob|All versions.|  
  
 These tables are automatically created when Storage Analytics is enabled for a storage service endpoint. They are accessed via the namespace of the storage account, for example: `https://<accountname>.table.core.windows.net/Tables("$MetricsTransactionsBlob")`. The metrics tables do not appear in a listing operation, and must be accessed directly via the table name.  
  
## Accessing Metrics Data  
 All data in the metrics tables can be accessed by using the Table service APIs, including the .NET APIs provided by the Azure managed library. The storage account administrator can read and delete table entities, but cannot create or update them.  
  
## See Also  
 [How To Monitor a Storage Account](http://www.windowsazure.com/manage/services/storage/how-to-monitor-a-storage-account/)   
 [Enabling and Configuring Storage Analytics](../StorageServicesREST/Enabling-and-Configuring-Storage-Analytics.md)   
 [Storage Analytics Metrics Table Schema](../StorageServicesREST/Storage-Analytics-Metrics-Table-Schema.md)   
 [Storage Analytics Logged Operations and Status Messages](../StorageServicesREST/Storage-Analytics-Logged-Operations-and-Status-Messages.md)   
 [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md)
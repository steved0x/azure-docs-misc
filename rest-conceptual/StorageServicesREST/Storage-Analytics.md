---
title: "Storage Analytics"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: f6481e74-78db-4964-b149-16e09173f5e1
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
# Storage Analytics
Azure Storage Analytics performs logging and provides metrics data for a storage account. You can use this data to trace requests, analyze usage trends, and diagnose issues with your storage account.  
  
 To use Storage Analytics, you must enable it individually for each service you want to monitor. You can enable it from the [Azure Management Portal](https://manage.windowsazure.com/); for details, see [How To Monitor a Storage Account](http://www.windowsazure.com/manage/services/storage/how-to-monitor-a-storage-account/). You can also enable Storage Analytics programmatically via the REST API or the client library. Use the `Set Service Properties` operation  to enable Storage Analytics individually for each service.  
  
> [!NOTE]
>  Storage Analytics metrics are available for the Blob, Queue, Table, and File services.  
>   
>  Storage Analytics logging is available for the Blob, Queue, and Table services.  
>   
>  Storage accounts with a replication type of Zone-Redundant Storage (ZRS) do not have the metrics or logging capability enabled at this time.  
  
 The aggregated data is stored in a well-known blob (for logging) and in well-known tables (for metrics), which may be accessed using the Blob service and Table service APIs.  
  
 Storage Analytics has a 20TB limit on the amount of stored data that is independent of the total limit for your storage account. For more information on billing and data retention policies, see [Storage Analytics and Billing](../StorageServicesREST/Storage-Analytics-and-Billing.md). For more information on storage account limits, see [Azure Storage Scalability and Performance Targets](assetId:///26df4d89-8289-4b31-aaa0-df971cab9b52).  
  
 For an in-depth guide on using Storage Analytics and other tools to identify, diagnose, and troubleshoot Azure Storage-related issues, see [Monitor, diagnose, and troubleshoot Microsoft Azure Storage](http://azure.microsoft.com/documentation/articles/storage-monitoring-diagnosing-troubleshooting/).  
  
## In This Section  
 [Using Storage Analytics](../StorageServicesREST/Using-Storage-Analytics.md)  
  
 [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md)  
  
 [About Storage Analytics Metrics](../StorageServicesREST/About-Storage-Analytics-Metrics.md)  
  
 [Storage Analytics Log Format](../StorageServicesREST/Storage-Analytics-Log-Format.md)  
  
 [Storage Analytics Metrics Table Schema](../StorageServicesREST/Storage-Analytics-Metrics-Table-Schema.md)  
  
 [Storage Analytics Logged Operations and Status Messages](../StorageServicesREST/Storage-Analytics-Logged-Operations-and-Status-Messages.md)  
  
 [Storage Analytics and Billing](../StorageServicesREST/Storage-Analytics-and-Billing.md)  
  
 [Setting a Storage Analytics Data Retention Policy](../StorageServicesREST/Setting-a-Storage-Analytics-Data-Retention-Policy.md)  
  
 [Enabling and Configuring Storage Analytics](../StorageServicesREST/Enabling-and-Configuring-Storage-Analytics.md)  
  
 [Client-side Logging with the .NET Storage Client Library](../StorageServicesREST/Client-side-Logging-with-the-.NET-Storage-Client-Library.md)  
  
 [Client-side Logging with the Microsoft Azure Storage SDK for Java](../StorageServicesREST/Client-side-Logging-with-the-Microsoft-Azure-Storage-SDK-for-Java.md)  
  
## Operations on Storage Service Properties  
 Storage Analytics is enabled and configured by using the Set/Get Storage Service Properties operations. These operations are listed in the following table.  
  
|Operation|Description|  
|---------------|-----------------|  
|[Set Blob Service Properties](../StorageServicesREST/Set-Blob-Service-Properties.md)|Sets or updates the properties of the Blob service, including Storage Analytics and the default request version.|  
|[Get Blob Service Properties](../StorageServicesREST/Get-Blob-Service-Properties.md)|Gets the properties of the Blob service, including Storage Analytics and the default request version.|  
|[Set Table Service Properties](../StorageServicesREST/Set-Table-Service-Properties.md)|Sets or updates the properties of the Table service, including Storage Analytics.|  
|[Get Table Service Properties](../StorageServicesREST/Get-Table-Service-Properties.md)|Gets the properties of the Table service, including Storage Analytics.|  
|[Set Queue Service Properties](../StorageServicesREST/Set-Queue-Service-Properties.md)|Sets or updates the properties of the Queue service, including Storage Analytics.|  
|[Get Queue Service Properties](../StorageServicesREST/Get-Queue-Service-Properties.md)|Gets the properties of the Queue service, including Storage Analytics.|  
|[Set File Service Properties](../StorageServicesREST/Set-File-Service-Properties.md)|Sets or updates the properties of the File service, including Storage Analytics metrics.|  
|[Get File Service Properties](../StorageServicesREST/Get-File-Service-Properties.md)|Gets the properties of the File service, including Storage Analytics metrics.|  
  
## See Also  
 [Storage Services REST](../StorageServicesREST/Azure-Storage-Services-REST-API-Reference.md)
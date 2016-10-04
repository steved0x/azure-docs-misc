---
title: "About Storage Analytics Logging"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 1727932c-8a3b-4502-86ac-c89931d54bac
caps.latest.revision: 24
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
# About Storage Analytics Logging
Storage Analytics logs detailed information about successful and failed requests to a storage service. This information can be used to monitor individual requests and to diagnose issues with a storage service. Requests are logged on a best-effort basis.  
  
 To use Storage Analytics, you must enable it individually for each service you want to monitor. You can enable it from the [Azure Management Portal](https://manage.windowsazure.com/); for details, see [How To Monitor a Storage Account](http://www.windowsazure.com/manage/services/storage/how-to-monitor-a-storage-account/). You can also enable Storage Analytics programmatically via the REST API or the client library. Use the [Get Blob Service Properties](../StorageServicesREST/Get-Blob-Service-Properties.md), [Get Queue Service Properties](../StorageServicesREST/Get-Queue-Service-Properties.md), and [Get Table Service Properties](../StorageServicesREST/Get-Table-Service-Properties.md) operations to enable Storage Analytics for each service.  
  
 Log entries are created only if there are requests made against the service endpoint. For example, if a storage account has activity in its Blob endpoint but not in its Table or Queue endpoints, only logs pertaining to the Blob service will be created.  
  
> [!NOTE]
>  Storage Analytics logging is currently available only for the Blob, Queue, and Table services.  
  
## Logging Authenticated Requests  
 The following types of authenticated requests are logged:  
  
-   Successful requests  
  
-   Failed requests, including timeout, throttling, network, authorization, and other errors  
  
-   Requests using a Shared Access Signature (SAS), including failed and successful requests  
  
-   Requests to analytics data  
  
 Requests made by Storage Analytics itself, such as log creation or deletion, are not logged. A full list of the logged data is documented in the [Storage Analytics Logged Operations and Status Messages](../StorageServicesREST/Storage-Analytics-Logged-Operations-and-Status-Messages.md) and [Storage Analytics Log Format](../StorageServicesREST/Storage-Analytics-Log-Format.md) topics.  
  
## Logging Anonymous Requests  
 The following types of anonymous requests are logged:  
  
-   Successful requests  
  
-   Server errors  
  
-   Timeout errors for both client and server  
  
-   Failed GET requests with error code 304 (Not Modified)  
  
 All other failed anonymous requests are not logged. A full list of the logged data is documented in the [Storage Analytics Logged Operations and Status Messages](../StorageServicesREST/Storage-Analytics-Logged-Operations-and-Status-Messages.md) and [Storage Analytics Log Format](../StorageServicesREST/Storage-Analytics-Log-Format.md) topics.  
  
## How Logs are Stored  
 All logs are stored in block blobs in a container named `$logs`, which is automatically created when Storage Analytics is enabled for a storage account. The `$logs` container is located in the blob namespace of the storage account, for example: `http://<accountname>.blob.core.windows.net/$logs`. This container cannot be deleted once Storage Analytics has been enabled, though its contents can be deleted.  
  
> [!NOTE]
>  The `$logs` container is not displayed when a container listing operation is performed, such as the List Containers operation. It must be accessed directly. For example, you can use the List Blobs operation to access the blobs in the `$logs` container.  
>   
>  As requests are logged, Storage Analytics will upload intermediate results as blocks. Periodically, Storage Analytics will commit these blocks and make them available as a blob.  
  
 Duplicate records may exist for logs created in the same hour. You can determine if a record is a duplicate by checking the **RequestId** and **Operation** number.  
  
### Log Naming Conventions  
 Each log will be written in the following format:  
  
 `<service-name>/YYYY/MM/DD/hhmm/<counter>.log`  
  
 The following table describes each attribute in the log name:  
  
|Attribute|Description|  
|---------------|-----------------|  
|`<service-name>`|The name of the storage service. For example: `blob`, `table`, or `queue`|  
|`YYYY`|The four digit year for the log. For example: `2011`|  
|`MM`|The two digit month for the log. For example: `07`|  
|`DD`|The two digit day for the log. For example: `31`|  
|`hh`|The two digit hour that indicates the starting hour for the logs, in 24 hour UTC format. For example: `18`|  
|`mm`|The two digit number that indicates the starting minute for the logs. **Note:**  This value is unsupported in the current version of Storage Analytics, and its value will always be `00`.|  
|`<counter>`|A zero-based counter with six digits that indicates the number of log blobs generated for the storage service in an hour time period. This counter starts at `000000`. For example: `000001`|  
  
 The following is a complete sample log name that combines the above examples:  
  
 `blob/2011/07/31/1800/000001.log`  
  
 The following is a sample URI that can be used to access the above log:  
  
 `https://<accountname>.blob.core.windows.net/$logs/blob/2011/07/31/1800/000001.log`  
  
 When a storage request is logged, the resulting log name correlates to the hour when the requested operation completed. For example, if a GetBlob request was completed at 6:30PM on 7/31/2011, the log would be written with the following prefix: `blob/2011/07/31/1800/`  
  
### Log Metadata  
 All log blobs are stored with metadata that can be used to identify what logging data the blob contains. The following table describes each metadata attribute:  
  
|Attribute|Description|  
|---------------|-----------------|  
|`LogType`|Describes whether the log contains information pertaining to read, write, or delete operations. This value can include one type or a combination of all three, separated by commas.<br /><br /> Example 1: `write`<br /><br /> Example 2: `read,write`<br /><br /> Example 3: `read,write,delete`|  
|`StartTime`|The earliest time of an entry in the log, in the form of `YYYY-MM-DDThh:mm:ssZ`. For example: `2011-07-31T18:21:46Z`|  
|`EndTime`|The latest time of an entry in the log, in the form of `YYYY-MM-DDThh:mm:ssZ`. For example: `2011-07-31T18:22:09Z`|  
|`LogVersion`|The version of the log format. Currently the only supported value is: `1.0`|  
  
 The following list displays complete sample metadata using the above examples:  
  
-   `LogType=write`  
  
-   `StartTime=2011-07-31T18:21:46Z`  
  
-   `EndTime=2011-07-31T18:22:09Z`  
  
-   `LogVersion=1.0`  
  
## Accessing Logging Data  
 All data in the `$logs` container can be accessed by using the Blob service APIs, including the .NET APIs provided by the Azure managed library. The storage account administrator can read and delete logs, but cannot create or update them. Both the log’s metadata and log name can be used when querying for a log. It is possible for a given hour’s logs to appear out of order, but the metadata always specifies the timespan of log entries in a log. Therefore, you can use a combination of log names and metadata when searching for a particular log.  
  
## See Also  
 [Storage Analytics Log Format](../StorageServicesREST/Storage-Analytics-Log-Format.md)   
 [Storage Analytics Logged Operations and Status Messages](../StorageServicesREST/Storage-Analytics-Logged-Operations-and-Status-Messages.md)   
 [About Storage Analytics Metrics](../StorageServicesREST/About-Storage-Analytics-Metrics.md)
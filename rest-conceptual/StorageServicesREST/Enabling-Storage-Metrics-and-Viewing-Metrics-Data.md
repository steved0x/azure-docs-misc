---
title: "Enabling Storage Metrics and Viewing Metrics Data"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: f3d15d3a-e898-4c6f-911d-3a936810c7b3
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
# Enabling Storage Metrics and Viewing Metrics Data
By default, Storage Metrics is not enabled for your storage endpoints. You can enable monitoring using either the Azure classic portal or Azure PowerShell, or programmatically via the storage client library.  
  
> [!NOTE]
>  Storage Analytics metrics is available for the Blob, Queue, Table, and File services.  
  
 When you enable Storage Metrics, you must choose a retention period for the data: this period determines for how long the storage service keeps the metrics and charges you for the space required to store them. Typically, you should use a shorter retention period for minute metrics than hourly metrics because of the significant extra space required for minute metrics. You should choose a retention period such that you have sufficient time to analyze the data and download any metrics you wish to keep for off-line analysis or reporting purposes. Remember that you will also be billed for downloading metrics data from your storage account.  
  
 In this section:  
  
 [How to enable Storage Metrics using the Azure classic portal](#HowtoenableStorageMetricsusingtheWindowsAzureManagementPortal)  
  
 [How to enable Storage Metrics using PowerShell](#HowtoenableStorageMetricsusingPowerShell)  
  
 [How to enable Storage Metrics programmatically](#HowtoenableStorageMetricsprogrammatically)  
  
 [Viewing Storage Metrics](#ViewingStorageMetrics)  
  
 [Accessing metrics data programmatically](#Accessingmetricsdataprogrammatically)  
  
 [What charges do you incur when you enable storage metrics?](#Whatchargesdoyouincurwhenyouenablestoragemetrics)  
  
##  <a name="HowtoenableStorageMetricsusingtheWindowsAzureManagementPortal"></a> How to enable Storage Metrics using the Azure classic portal  
 In the Azure classic portal, you use the Configure page for a storage account to control Storage Analytics metrics. For monitoring, you can set a level and a retention period in days for each service. In each case, the level is one of the following:  
  
-   **Off** — this means no metrics are collected.  
  
-   **Minimal** — Storage Metrics collects a basic set of metrics such as ingress/egress, availability, latency, and success percentages, which are aggregated for the Blob, Table, Queue, and File services.  
  
-   **Verbose** — Storage Metrics collects a full set of metrics that includes the same metrics for each storage API operation, in addition to the service-level metrics. Verbose metrics enable closer analysis of issues that occur during application operations.  
  
> [!NOTE]
>  Note that the Azure classic portal does not currently enable you to configure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.  
  
 For more information, see [About Storage Analytics Metrics](http://msdn.microsoft.com/library/azure/hh343258.aspx).  
  
##  <a name="HowtoenableStorageMetricsusingPowerShell"></a> How to enable Storage Metrics using PowerShell  
 You can use PowerShell on your local machine to configure Storage Metrics in your storage account by using the Azure PowerShell cmdlet **Get-AzureStorageServiceMetricsProperty** to retrieve the current settings, and the cmdlet **Set-AzureStorageServiceMetricsProperty** to change the current settings.  
  
 The cmdlets that control Storage Metrics use the following parameters:  
  
-   **MetricsType** possible values are **Hour** and **Minute**.  
  
-   **ServiceType** possible value are **Blob**,  **Queue**, **Table**, and **File**.  
  
-   **MetricsLevel** possible values are **None** (equivalent to Off in the classic portal),  **Service** (equivalent to Minimal in the classic portal), and **ServiceAndApi** (equivalent to Verbose in the classic portal).  
  
 For example, the following command switches on minute metrics for the blob service in your default storage account with the retention period set to five days:  
  
```  
Set-AzureStorageServiceMetricsProperty -MetricsType Minute   
-ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5  
```  
  
 The following command retrieves the current hourly metrics level and retention days for the blob service in your default storage account:  
  
```  
Get-AzureStorageServiceMetricsProperty -MetricsType Hour   
-ServiceType Blob  
```  
  
 For information about how to configure the Azure PowerShell cmdlets to work with your Azure subscription and how to select the default storage account to use, see: [How to install and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/install-configure-powershell/).  
  
##  <a name="HowtoenableStorageMetricsprogrammatically"></a> How to enable Storage Metrics programmatically  
 In addition to using the Azure classic portal or the Azure PowerShell cmdlets to control Storage Metrics, you can also use one of the Azure Storage APIs. For example, if you are using a .NET language you can use the Storage Client Library.  
  
 The classes **CloudBlobClient**, **CloudQueueClient**, **CloudTableClient**, and **CloudFileClient** all have methods such as **SetServiceProperties** and **SetServicePropertiesAsync** that take a **ServiceProperties** object as a parameter. You can use the **ServiceProperties** object to configure Storage Metrics. For example, the following C# snippet shows how to change the metrics level and retention days for the hourly queue metrics:  
  
```  
var storageAccount = CloudStorageAccount.Parse(connStr);  
var queueClient = storageAccount.CreateCloudQueueClient();  
var serviceProperties = queueClient.GetServiceProperties();  
  
serviceProperties.HourMetrics.MetricsLevel = MetricsLevel.Service;  
serviceProperties.HourMetrics.RetentionDays = 10;  
  
queueClient.SetServiceProperties(serviceProperties);  
```  
  
 For more information about using a .NET language to configure Storage Metrics, see [Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).  
  
 For general information about configuring Storage Metrics using the REST API, see [Enabling and Configuring Storage Analytics](http://msdn.microsoft.com/en-us/library/azure/hh360996.aspx).  
  
##  <a name="ViewingStorageMetrics"></a> Viewing Storage Metrics  
 When you have configured Storage Metrics to monitor your storage account, it records the metrics in a set of well-known tables in your storage account. You can use the **Monitor** page for your storage account in the classic portal to view the hourly metrics as they become available on a chart. On this page in the classic portal, you can:  
  
-   Select which metrics to plot on the chart (the choice of available metrics will depend on whether you chose verbose or minimal monitoring for the service on the **Configure** page).  
  
-   Select the time range for the metrics displayed on the chart.  
  
-   Choose to use an absolute or relative scale to plot the metrics.  
  
-   Configure email alerts to notify you when a specific metric reaches a certain value.  
  
 If you want to download the metrics for long-term storage or to analyze them locally, you will need to use a tool or write some code to read the tables. You must download the minute metrics for analysis. The tables do not appear if you list all the tables in your storage account, but you can access them directly by name. Many third-party storage-browsing tools are aware of these tables and enable you to view them directly (see the blog post [Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available tools).  
  
||||  
|-|-|-|  
|**Metrics**|**Table names**|**Notes**|  
|Hourly metrics|$MetricsHourPrimaryTransactionsBlob<br /><br /> $MetricsHourPrimaryTransactionsTable<br /><br /> $MetricsHourPrimaryTransactionsQueue<br /><br /> $MetricsHourPrimaryTransactionsFile|In versions prior to 2013-08-15, these tables were known as:<br /><br /> $MetricsTransactionsBlob<br /><br /> $MetricsTransactionsTable<br /><br /> $MetricsTransactionsQueue<br /><br /> Metrics for the File service are available beginning with version 2015-04-05.|  
|Minute metrics|$MetricsMinutePrimaryTransactionsBlob<br /><br /> $MetricsMinutePrimaryTransactionsTable<br /><br /> $MetricsMinutePrimaryTransactionsQueue<br /><br /> $MetricsMinutePrimaryTransactionsFile|Can only be enabled using PowerShell or programmatically.<br /><br /> Metrics for the File service are available beginning with version 2015-04-05.|  
|Capacity|$MetricsCapacityBlob|Blob service only.|  
  
 You can find full details of the schemas for these tables at [Storage Analytics Metrics Table Schema](http://msdn.microsoft.com/library/azure/hh343264.aspx). The sample rows below show only a subset of the columns available, but illustrate some important features of the way Storage Metrics saves these metrics:  
  
||||||||||||  
|-|-|-|-|-|-|-|-|-|-|-|  
|**PartitionKey**|**RowKey**|**Timestamp**|**TotalRequests**|**TotalBillableRequests**|**TotalIngress**|**TotalEgress**|**Availability**|**AverageE2ELatency**|**AverageServerLatency**|**PercentSuccess**|  
|20140522T1100|user;All|2014-05-22T11:01:16.7650250Z|7|7|4003|46801|100|104.4286|6.857143|100|  
|20140522T1100|user;QueryEntities|2014-05-22T11:01:16.7640250Z|5|5|2694|45951|100|143.8|7.8|100|  
|20140522T1100|user;QueryEntity|2014-05-22T11:01:16.7650250Z|1|1|538|633|100|3|3|100|  
|20140522T1100|user;UpdateEntity|2014-05-22T11:01:16.7650250Z|1|1|771|217|100|9|6|100|  
  
 In this example minute metrics data, the partition key uses the time at minute resolution. The row key identifies the type of information that is stored in the row and this is composed of two pieces of information, the access type, and the request type:  
  
-   The access type is either **user** or **system**, where **user** refers to all user requests to the storage service, and **system** refers to requests made by Storage Analytics.  
  
-   The request type is either **all** in which case it is a summary line, or it identifies the specific API such as **QueryEntity** or **UpdateEntity**.  
  
 The sample data above shows all the records for a single minute (starting at 11:00AM), so the number of **QueryEntities** requests plus the number of **QueryEntity** requests plus the number of **UpdateEntity** requests add up to seven, which is the total shown on the **user:All** row. Similarly, you can derive the average end-to-end latency 104.4286 on the **user:All** row by calculating ((143.8 * 5) + 3 + 9)/7.  
  
 You should consider setting up alerts in the classic portal on the **Monitor** page so that Storage Metrics can automatically notify you of any important changes in the behavior of your storage services.If you use a storage explorer tool to download this metrics data in a delimited format, you can use Microsoft Excel to analyze the data. See the blog post [Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available storage explorer tools.  
  
##  <a name="Accessingmetricsdataprogrammatically"></a> Accessing metrics data programmatically  
 The following listing shows sample C# code that accesses the minute metrics for a range of minutes and displays the results in a console Window. The code sample uses the Azure Storage Client Library version 4.x or later, which includes the **CloudAnalyticsClient** class that simplifies accessing the metrics tables in storage.  
  
```  
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)  
{  
    // Convert the dates to the format used in the PartitionKey  
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");  
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");  
  
    var services = Enum.GetValues(typeof(StorageService));  
    foreach (StorageService service in services)  
    {  
        Console.WriteLine("Minute Metrics for Service {0} from {1} to {2} UTC", service, start, end);  
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);  
        var t = analyticsClient.GetMinuteMetricsTable(service);  
        var opContext = new OperationContext();  
        var query =  
                from entity in metricsQuery  
                // Note, you can't filter using the entity properties Time, AccessType, or TransactionType  
                // because they are calculated fields in the MetricsEntity class.  
                // The PartitionKey identifies the DataTime of the metrics.  
                where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0   
                select entity;  
  
        // Filter on "user" transactions after fetching the metrics from Table Storage.  
        // (StartsWith is not supported using LINQ with Azure Table storage)  
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));  
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();  
        Console.WriteLine(resultString);  
    }  
}  
  
private static string MetricsString(MetricsEntity entity, OperationContext opContext)  
{  
    var entityProperties = entity.WriteEntity(opContext);  
    var entityString =  
            string.Format("Time: {0}, ", entity.Time) +  
            string.Format("AccessType: {0}, ", entity.AccessType) +  
            string.Format("TransactionType: {0}, ", entity.TransactionType) +  
            string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));  
    return entityString;  
  
}  
```  
  
##  <a name="Whatchargesdoyouincurwhenyouenablestoragemetrics"></a> What charges do you incur when you enable storage metrics?  
 Write requests to create table entities for metrics are charged at the standard rates applicable to all Azure Storage operations.  
  
 Read and delete requests by a client to metrics data are also billable at standard rates. If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data. However, if you delete analytics data, your account is charged for the delete operations.  
  
 The capacity used by the metrics tables is also billable: you can use the following to estimate the amount of capacity used for storing metrics data:  
  
-   If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in the metrics transaction tables if you have enabled both service and API level summary.  
  
-   If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in the metrics transaction tables if you have enabled just service level summary.  
  
-   The capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day the size of this table increases by up to approximately 300 bytes.
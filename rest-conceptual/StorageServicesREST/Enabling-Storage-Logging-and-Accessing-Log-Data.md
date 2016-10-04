---
title: "Enabling Storage Logging and Accessing Log Data"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 7edfcd7b-26ce-405c-bfb6-87e52930c344
caps.latest.revision: 9
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
# Enabling Storage Logging and Accessing Log Data
Storage Logging happens server-side and enables you to record details for both successful and failed requests in your storage account. These logs enable you to see details of read, write, and delete operations against your Azure tables, queues, and blobs. They also enable you to see the reasons for failed requests such as timeouts, throttling, and authorization errors.  
  
> [!NOTE]
>  Storage Analytics logging is currently available only for the Blob, Queue, and Table services.  
  
 Storage Logging log entries contain the following information about individual requests:  
  
-   Timing information such as start time, end-to-end latency, and server latency.  
  
-   Details of the storage operation such as the operation type, the key of the storage object the client is accessing, success or failure, and the HTTP status code returned to the client.  
  
-   Authentication details such as the type of authentication the client used.  
  
-   Concurrency information such as the ETag value and last modified timestamp.  
  
-   The sizes of the request and response messages.  
  
 For detailed information about the format of log entries that Storage Logging writes, see [Storage Analytics Log Format](http://msdn.microsoft.com/library/hh343259.aspx).  
  
 In this section:  
  
 [How to enable Storage Logging using the Azure classic portal](#HowtoenableStorageLoggingusingtheWindowsAzureManagementPortal)  
  
 [How to enable Storage Logging using PowerShell](#HowtoenableStorageLoggingusingPowerShell)  
  
 [How to enable Storage Logging programmatically](#HowtoenableStorageLoggingprogrammatically)  
  
 [Finding your Storage Logging log data](#FindingyourStorageLogginglogdata)  
  
 [Downloading Storage Logging log data](#DownloadingStorageLogginglogdata)  
  
 Storage Logging logs request data in a set of blobs in a blob container named **$logs** in your storage account. This container does not show up if you list all the blob containers in your account but you can see its contents if you access it directly. For example the Windows Azure classic portal does not show the **$logs** container and neither does the PowerShell cmdlet **Get-AzureStorageContainer** if you execute it without any parameters.  
  
 You should collect logging information from your storage account to enable you to diagnose and troubleshoot issues that users report or that monitoring metrics reveals. You can use the log data to determine information such as when a client updated an object or who deleted a specific object. You should set the retention period long enough to allow you time to identify a potential issue through monitoring or from user reports, and then to download the relevant log data for analysis. You should include some extra time in the retention period as a buffer to ensure you do not lose log data before you have had a chance to download it.  
  
 There are some additional considerations to bear in mind when working with Storage Logging log data:  
  
-   There may be some clock skew between information recorded by Storage Metrics and StorageLogging: if you are searching for log entries that relate to metrics data, you may need to search up to 15 minutes either side of the time recorded for the metrics data.  
  
-   You can correlate the server-side log data with other log sources: for more information, see the guide [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](http://go.microsoft.com/fwlink/?LinkID=510535).  
  
-   You can automate downloading log data. For example, you can use PowerShell and the **AzCopy** tool to download the blobs containing your log data. For more information, see [Downloading Storage Logging log data](#DownloadingStorageLogginglogdata).  
  
-   Because Storage Logging stores log data in your Azure Storage account, you must be aware of the potential cost implications of enabling logging. You will be charged for the storage you use for this log data and for transferring this data out of your storage account. By setting a retention period, you can ensure that the storage service deletes old log data from your account automatically.  
  
 For more information, see [About Storage Analytics Logging](http://msdn.microsoft.com/library/azure/hh343262.aspx).  
  
 Storage Logging is not enabled by default for your storage services. You can enable logging using either the Windows Azure classic portal, Windows PowerShell, or programmatically through a storage API.  
  
##  <a name="HowtoenableStorageLoggingusingtheWindowsAzureManagementPortal"></a> How to enable Storage Logging using the Azure classic portal  
 In the Azure classic portal, you use the Configure page for a storage account to control Storage Logging. For logging, you can specify the types of request (read, write, delete) that you want to log and retention period in days for the logged data for each Azure storage service.  
  
##  <a name="HowtoenableStorageLoggingusingPowerShell"></a> How to enable Storage Logging using PowerShell  
 You can use PowerShell on your local machine to configure Storage Logging in your storage account by using the Azure PowerShell cmdlet **Get-AzureStorageServiceLoggingProperty** to retrieve the current settings, and the cmdlet **Set-AzureStorageServiceLoggingProperty** to change the current settings.  
  
 The cmdlets that control Storage Logging use a **LoggingOperations** parameter that is a string containing a comma-separated list of request types to log. The three possible request types are **read**, **write**, and **delete**. To switch off logging, use the value **none** for the **LoggingOperations** parameter.  
  
 The following command switches on logging for read, write, and delete requests in the Queue service in your default storage account with retention set to five days:  
  
```  
Set-AzureStorageServiceLoggingProperty -ServiceType Queue   
-LoggingOperations read,write,delete -RetentionDays 5  
```  
  
 The following command switches off logging for the table service in your default storage account:  
  
```  
Set-AzureStorageServiceLoggingProperty -ServiceType Table   
-LoggingOperations none  
```  
  
 For information about how to configure the Azure PowerShell cmdlets to work with your Azure subscription and how to select the default storage account to use, see: [How to install and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/install-configure-powershell/).  
  
##  <a name="HowtoenableStorageLoggingprogrammatically"></a> How to enable Storage Logging programmatically  
 In addition to using the Windows Azure classic portal or the Azure PowerShell cmdlets to control Storage Logging, you can also use one of the Azure Storage APIs. For example, if you are using a .NET language you can use the Storage Client Library.  
  
 The classes **CloudBlobClient**, **CloudQueueClient**, and **CloudTableClient** all have methods such as **SetServiceProperties** and **SetServicePropertiesAsync** that take a **ServiceProperties** object as a parameter. You can use the **ServiceProperties** object to configure Storage Logging. For example, the following C# snippet shows how to change what is logged and the retention period for queue logging:  
  
```  
var storageAccount = CloudStorageAccount.Parse(connStr);  
var queueClient = storageAccount.CreateCloudQueueClient();  
var serviceProperties = queueClient.GetServiceProperties();  
  
serviceProperties.Logging.LoggingOperations = LoggingOperations.All;  
serviceProperties.Logging.RetentionDays = 2;  
  
queueClient.SetServiceProperties(serviceProperties);  
```  
  
 For more information about using a .NET language to configure Storage Logging, see [Storage Client Library Reference](http://msdn.microsoft.com/library/azure/dn261237.aspx).  
  
 For general information about configuring Storage Logging using the REST API, see [Enabling and Configuring Storage Analytics](http://msdn.microsoft.com/library/azure/hh360996.aspx).  
  
##  <a name="FindingyourStorageLogginglogdata"></a> Finding your Storage Logging log data  
 When you have configured Storage Logging to log request data from your storage account, it saves the log data to blobs in a container named **$logs** in your storage account. This container does not show up if you list all the containers in your account, but if you use your storage-browsing tool to navigate to the container directly, you will see all the blobs that contain your logging data. Storage Logging uses a naming convention for the blobs to make it easy to identify the blob in which you are interested. Within your **$logs** container, the blobs are named as follows:  
  
```  
<servicetype>/YYYY/MM/DD/HHMM/<counter>.log  
```  
  
 The value of the service name is **blob**, **table**, or **queue**. Therefore, a blob named **table/2014/05/20/0900/000002.log** in your **$logs** container is the second log file of Table service request data created in the hour after 09:00 AM on 20th May 2014.  
  
> [!NOTE]
>  Note that it can take up to an hour for log data to appear in the blobs in the **$logs** container because the frequency at which the storage service flushes the log writers.  
  
 If you have a high volume of log data with multiple files for each hour, then you can use the blob metadata to determine what data the log contains by examining the blob metadata fields. This is also useful because there can sometimes be a delay while data is written to the log files: the blob metadata gives a more accurate indication of the blob content than the blob name. Blobs containing log data have the following metadata fields:  
  
-   **StartTime** is a UST timestamp that records the time of the earliest log entry in the blob.  
  
-   **EndTime** is a UST timestamp that records the time of the latest log entry in the blob.  
  
-   **LogType** records the type of log entries contained in the blob as one or more of: read, write, delete.  
  
 Most storage browsing tools enable you to view the metadata of blobs; you can also read this information using PowerShell or programmatically. The following PowerShell snippet is an example of filtering the list of log blobs by name to specify a time, and by metadata to identify just those logs that contain **write** operations.  
  
```  
Get-AzureStorageBlob -Container '$logs' |  
where {  
    $_.Name -match 'table/2014/05/21/05' -and   
    $_.ICloudBlob.Metadata.LogType -match 'write'  
} |  
foreach {  
    "{0}  {1}  {2}  {3}" –f $_.Name,   
    $_.ICloudBlob.Metadata.StartTime,   
    $_.ICloudBlob.Metadata.EndTime,   
    $_.ICloudBlob.Metadata.LogType  
}  
```  
  
 For information about listing blobs programmatically, see [Enumerating Blob Resources](http://msdn.microsoft.com/library/azure/hh452233.aspx) and [Setting and Retrieving Properties and Metadata for Blob Resources](http://msdn.microsoft.com/library/azure/dd179404.aspx).  
  
##  <a name="DownloadingStorageLogginglogdata"></a> Downloading Storage Logging log data  
 To view and analyze your log data, you should download the blobs that contain the log data you are interested in to a local machine. Many storage-browsing tools enable you to download blobs from your storage account; you can also use the Azure Storage team provided command-line Azure Copy Tool (**AzCopy**) to download your log data.  
  
 To make sure you download the log data you are interested in and to avoid downloading the same log data more than once:  
  
-   Use the date and time naming convention for blobs containing log data to track which blobs you have already downloaded for analysis to avoid re-downloading the same data more than once.  
  
-   Use the metadata on the blobs containing log data to identify the specific period for which the blob holds log data to identify the exact blob you need to download.  
  
> [!NOTE]
>  AzCopy is part of the Azure SDK, but you can always download the latest version from [http://aka.ms/AzCopy](http://aka.ms/AzCopy). By default, AzCopy is installed in the folder **C:\Program Files (x86)\Microsoft SDKs\Windows Azure\AzCopy**, and you should add this folder to your path before you try to run the tool in a command prompt or PowerShell window.  
  
 The following example shows how you can download the log data for the queue service for the hours starting at 09 AM, 10 AM, and 11 AM on 20th May, 2014. The **/S** parameter causes AzCopy to build a local folder structure based on the dates and times in the log file names; the **/V** parameter causes AzCopy to produce verbose output; the **/Y** parameter causes AzCopy to overwrite any local files. Replace **<yourstorageaccount\>** with the name of your storage account and replace **<yourstoragekey\>** with your storage account key.  
  
```  
AzCopy 'http://<yourstorageaccount>.blob.core.windows.net/$logs/queue'  'C:\Logs\Storage' '2014/05/20/09' '2014/05/20/10' '2014/05/20/11' /sourceKey:<yourstoragekey> /S /V /Y  
```  
  
 AzCopy also has some useful parameters that control how it sets the last modified time on the files it downloads, and whether it will attempt to download files that are older or newer than any files that already exist on your local machine. You can also run it in restartable mode. For full details, view the help by running the **AzCopy /?** command.  
  
 For an example of how to download your log data programmatically, see the blog post [Windows Azure Storage Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx) and search for the word "DumpLogs" on the page.  
  
 When you have downloaded your log data, you can view the log entries in the files. These log files use a delimited text format that many log reading tools are able to parse, including Microsoft Message Analyzer (for more information, see the guide [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](http://go.microsoft.com/fwlink/?LinkID=510535)). Different tools have different facilities for formatting, filtering, sorting, ad searching the contents of your log files. For more information about the Storage Logging log file format and content, see [Storage Analytics Log Format](http://msdn.microsoft.com/library/azure/hh343259.aspx) and [Storage Analytics Logged Operations and Status Messages](http://msdn.microsoft.com/library/azure/hh343260.aspx).
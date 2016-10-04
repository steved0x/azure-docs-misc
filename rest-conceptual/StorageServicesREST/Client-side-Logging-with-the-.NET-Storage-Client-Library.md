---
title: "Client-side Logging with the .NET Storage Client Library"
ms.custom: na
ms.date: 2016-10-03
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 068eaab9-da89-4107-b73e-6da25eb04bcb
caps.latest.revision: 10
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
# Client-side Logging with the .NET Storage Client Library
The storage client Library (from version 2.1 onwards) enables you to log Azure Storage requests client-side from within your .NET client application using the standard .NET diagnostics infrastructure. This enables you to see details of the requests your client sends to the Azure Storage services and the responses it receives.  
  
 The Storage Client Library gives you control over which storage requests you want to log on the client (Azure web or worker role, or an on-premises application) and the .NET diagnostics infrastructure gives you full control over the log data, such as where to send it. For example, you could choose to send the log data to a file, or send it to an application for processing. In combination with Azure Storage Analytics and network monitoring, Storage Client Library logging enables you to build up a detailed picture of how your application interacts with Azure Storage services. For more information, see the guide [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](http://go.microsoft.com/fwlink/?LinkID=510535).  
  
## How to enable Storage Client Library logging  
 The following example shows the system.diagnostics configuration necessary to collect and persist storage log messages to a text file. This configuration section can be added to either app.config or web.config files.  
  
```  
<system.diagnostics>  
     <!—In a dev/test environment you can set autoflush to true in order to autoflush to the log file. -->  
  <trace autoflush="false">  
    <listeners>  
      ...   
      <add name="storageListener" />  
    </listeners>  
  </trace>  
  <sources>  
    <source name="Microsoft.WindowsAzure.Storage">  
      <listeners>  
        <add name="storageListener"/>  
      </listeners>  
    </source>  
  </sources>  
  <switches>  
    <add name="Microsoft.WindowsAzure.Storage" value="Verbose" />  
  </switches>  
  <sharedListeners>  
    <add name="storageListener"  
      type="System.Diagnostics.TextWriterTraceListener"  
      initializeData="C:\logs\WebRole.log"
      traceOutputOptions="DateTime" />  
  </sharedListeners>  
</system.diagnostics>  
  
```  
  
 This particular example configures the Storage Client Library to write log messages to the physical file C:\logs\WebRole.log, but you could use other trace listeners such as the **EventLogTraceListener** to write to the Windows Event Log, or the **EventProviderTraceListener** to write trace data to the ETW subsystem. In addition, this example you can also configure **autoflush** to true in order to write the log entries to the file immediately instead of buffering them; this may be useful in a dev/test environment with low volumes of trace messages, but in a production environment you may want to set **autoflush** to false. You use the configuration settings to enable client tracing (and specify the level such as **Verbose** for all messages) for all storage operations in the client.  
  
||||  
|-|-|-|  
|Id|Log Level|Events|  
|0|Off|Nothing will be logged.|  
|1|Error|If an exception cannot or will not be handled internally and will be thrown to the user; it will be logged as an error.|  
|2|Warning|If an exception is caught and handled internally, it will be logged as a warning. Primary use case for this is the retry scenario, where an exception is not thrown back to the user to be able to retry. It can also happen in operations such as CreateIfNotExists, where we handle the 404 error silently.|  
|3|Informational|The following info will be logged:<br /><br /> •Right after the user calls a method to start an operation, request details such as URI and client request ID will be logged.<br /><br /> •Important milestones such as Sending Request Start/End, Upload Data Start/End, Receive Response Start/End, Download Data Start/End will be logged to mark the timestamps.<br /><br /> •Right after the headers are received, response details such as request ID and HTTP status code will be logged.<br /><br /> •If an operation fails and the storage client decides to retry, the reason for that decision will be logged along with when the next retry is going to happen.<br /><br /> •All client-side timeouts will be logged when storage client decides to abort a pending request.|  
|4|Verbose|Following info will be logged:<br /><br /> •String-to-sign for each request<br /><br /> •Any extra details specific to operations (this is up to each operation to define and use)|  
  
 By default, the Storage Client Library logs details of all storage operations at the verbosity level you specify in the configuration file. It is also possible to limit the logging to specific areas of your client application: this can reduce the amount of data logged and help you find the information you need. TO do this, you need to add some code to your client application. Typically, after enabling client-side tracing in the configuration file, you then switch it off again globally in code by using the **OperationContext** class. For example, in an ASP.NET MVC application in the **Application_Start** method before your application performs any storage operations:  
  
```  
protected void Application_Start()  
{  
    ...  
  
    // Disable Default Logging for Windows Azure Storage  
    OperationContext.DefaultLogLevel = LogLevel.Off;  
  
    // Verify that all of the tables, queues, and blob containers used in this application  
    // exist, and create any that don't already exist.  
    CreateTablesQueuesBlobContainers();  
}  
```  
  
 Then you can enable tracing for the specific operations you are interested in by creating a custom **OperationContext** object that defines the logging level. Then pass the **OperationContext** object as a parameter to the **Execute** method you use to invoke a storage operation as shown in the following example:  
  
```  
[HttpPost]  
[ValidateAntiForgeryToken]  
public ActionResult Create(Subscriber subscriber)  
{  
    if (ModelState.IsValid)  
    {  
       ...  
        var insertOperation = TableOperation.Insert(subscriber);  
        OperationContext verboseLoggingContext = new OperationContext() { LogLevel = LogLevel.Verbose };  
        mailingListTable.Execute(insertOperation, null, verboseLoggingContext);  
        return RedirectToAction("Index");  
    }  
  
    ...  
    return View(subscriber);  
}  
  
```  
  
## Client-side log schema and sample  
 The following is an extract from the client-side log generated by the Storage Client Library for an operation with a Client Request ID including c3aa328b. The Client Request Id is a correlation identifier that allows messages logged client side to be correlated with network traces and storage logs. For more information on correlation see Monitoring, Diagnosing and Troubleshooting Azure Storage. The extract includes commentary (indented and italicized) on some key information that can be observed from within the log files.  
  
 To illustrate this using the first row of the log file shown below, the fields are  
  
|||  
|-|-|  
|**Source**|Microsoft.WindowsAzure.Storage|  
|**Verbosity**|Information|  
|**Verbosity No**|3|  
|**Client Request ID**|c3aa328b...|  
|**Operation Text**|Starting operation with location Primary per location mode PrimaryOnly.|  
  
 `Microsoft.WindowsAzure.Storage Information: 3 : c3aa328b...: Starting operation with location Primary per location mode PrimaryOnly.`   
 *The trace message above shows that the [location mode](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.retrypolicies.locationmode.aspx) is set to primary only, meaning that a failed request will not be sent to a secondary location.*   
 `Microsoft.WindowsAzure.Storage Information: 3 : c3aa328b...: Starting synchronous request to https://storageaccountname.table.core.windows.net/mailinglist.`   
 *The trace message above shows that the request is synchronous.*   
 `Microsoft.WindowsAzure.Storage Information: 3 : c3aa328b...: Setting payload format for the request to 'Json'.`   
 *The trace message above shows that the response should be return formatted as JSON.*   
 `Microsoft.WindowsAzure.Storage Verbose: 4 : c3aa328b...: StringToSign = GET...Fri, 23 May 2014 06:19:48 GMT./storageaccountname/mailinglist.`   
 *The trace message above includes the StringToSign information which is useful for debugging auth failures. Verbose messages also contain full request details  including operation type and request parameters.*   
 `Microsoft.WindowsAzure.Storage Information: 3 : c3aa328b...: Waiting for response.`   
 *The trace message above shows that the request has been sent and the client is awaiting a response.*   
 `Microsoft.WindowsAzure.Storage Information: 3 : c3aa328b...: Response received. Status code = 200, Request ID = 417db530-853d-48a7-a23c-0c8d5f728178, Content-MD5 = , ETag =`   
 *The trace message above shows that the response has been received and its http status code.*   
 `Microsoft.WindowsAzure.Storage Information: 3 : c3aa328b...: Response headers were processed successfully, proceeding with the rest of the operation.`   
 `Microsoft.WindowsAzure.Storage Information: 3 : c3aa328b...: Processing response body.`   
 `Microsoft.WindowsAzure.Storage Information: 3 : c3aa328b...: Retrieved '8' results with continuation token ''.`   
 *The trace message above shows that 8 results were retrieved and no continuation token was provided meaning no more results exist for this query.*   
 `Microsoft.WindowsAzure.Storage Information: 3 : c3aa328b...: Operation completed successfully.`   
 *The trace message above shows that the operation completed successfully.*  
  
 The following two verbose (level 4) log entries show a HEAD and a DELETE request and illustrate the detailed information that the **Operation Text** field contains:   
`Microsoft.WindowsAzure.Storage Verbose: 4 : 07b26a5d...: StringToSign = HEAD............x-ms-client-request-id:07b26a5d....x-ms-date:Tue, 03 Jun 2014 10:33:11 GMT.x-ms-version:2014-02-14./storageaccountname/azuremmblobcontainer.restype:container.`  
`Microsoft.WindowsAzure.Storage Verbose: 4 : 07b26a5d...: StringToSign = DELETE............x-ms-client-request-id:07b26a5d....x-ms-date:Tue, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./storageaccountname/azuremmblobcontainer.restype:container.`  
*The trace message above shows the OperationText field within verbose trace messages including detailed information related to a specific request including HTTP operation type (HEAD, DELETE, POST etc), the client request id, the timestamp, SDK version and additional operation specific data.*
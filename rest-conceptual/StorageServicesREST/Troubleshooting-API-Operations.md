---
title: "Troubleshooting API Operations"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: b20a45d8-7453-487c-b492-69dc5a5b6d2d
caps.latest.revision: 17
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
# Troubleshooting API Operations
The following sections offer troubleshooting tips for API operations:  
  
 [Failed Request Tracing](#Failedrequesttracing)  
  
 [The x-ms-request-id Header](#Thex-ms-request-idheader)  
  
##  <a name="FailedRequestTracing"></a> Failed Request Tracing  
 The development environment supports the use of the Internet Information Services (IIS) 7.0 Failed Request Tracing feature to log information about requests. Failed Request Tracing produces detailed trace logs according to filters established within a web role’s configuration.  
  
### Logging Destination  
 Windows Azure outputs trace log files to the default IIS directory for failed request logs. This directory by default is %SystemDrive%\inetpub\logs\FailedReqLogFiles.  
  
### Enabling Tracing  
 Each web role must enable tracing by using rules placed in the project's web.config file. To enable tracing, place the following in the `system.webServer` section of your web.config file:  
  
```  
<tracing>  
  <traceFailedRequests>  
    <add path="*">  
      <traceAreas>  
        <add provider="ASP" verbosity="Verbose" />  
        <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />  
        <add provider="ISAPI Extension" verbosity="Verbose" />  
        <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression,Cache,RequestNotifications,Module" verbosity="Verbose" />  
      </traceAreas>  
      <failureDefinitions statusCodes="400-599" />  
    </add>  
  </traceFailedRequests>  
</tracing>  
```  
  
 To disable tracing, remove this section from the web.config file.  
  
##  <a name="Thex-ms-request-idheader"></a> The x-ms-request-id Header  
 Every request made against the storage services returns a response header named `x-ms-request-id`. This header contains an opaque value that uniquely identifies the request.  
  
 If a request is consistently failing and you have verified that the request is properly formulated, you may use this value to report the error to Microsoft. In your report, include the value of `x-ms-request-id`, the approximate time that the request was made, the storage service against which the request was made, and the type of operation that the request attempted.  
  
## See Also  
 [Storage Services REST](../StorageServicesREST/Azure-Storage-Services-REST-API-Reference.md)
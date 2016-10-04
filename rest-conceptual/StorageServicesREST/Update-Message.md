---
title: "Update Message"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 5f574ef2-2371-4336-94de-c2cef61edb6f
caps.latest.revision: 19
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
# Update Message
This operation was introduced with version 2011-08-18 of the Queue service API. The `Update Message` operation updates the visibility timeout of a message. You can also use this operation to update the contents of a message. A message must be in a format that can be included in an XML request with UTF-8 encoding, and the encoded message can be up to 64KB in size.  
  
## Request  
 The `Update Message` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account, and `myqueue` with the name of your queue:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`PUT`|`https://myaccount.queue.core.windows.net/myqueue/messages/messageid?popreceipt=<string-value>&visibilitytimeout=<int-seconds>`|HTTP/1.1|  
  
### Emulated Storage Service  
 This operation is supported for SDK 1.6 and newer versions.  
  
 When making a request against the emulated storage service, specify the emulator hostname and Queue service port as `127.0.0.1:10001`, followed by the emulated storage account name:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`PUT`|`http://127.0.0.1:10001/devstoreaccount1/myqueue/messages/messageid?popreceipt=<string-value>&visibilitytimeout=<int-seconds>`|HTTP/1.1|  
  
### URI Parameters  
 The following parameters may be specified on the request URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`popreceipt`|Required. Specifies the valid pop receipt value returned from an earlier call to the [Get Messages](../StorageServicesREST/Get-Messages.md) or [Update Message](../StorageServicesREST/Update-Message.md) operation.|  
|`visibilitytimeout`|Required. Specifies the new visibility timeout value, in seconds, relative to server time. The new value must be larger than or equal to 0, and cannot be larger than 7 days. The visibility timeout of a message cannot be set to a value later than the expiry time. A message can be updated until it has been deleted or has expired.|  
|`timeout`|Optional. The `timeout` parameter is expressed in seconds. For more information, see [Setting Timeouts for Queue Service Operations](../StorageServicesREST/Setting-Timeouts-for-Queue-Service-Operations.md).|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` `or x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Requires 2011-08-18 or newer. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
### Request Body  
 The body of the request contains the message data in the following XML format. Note that the message content must be in a format that may be encoded with UTF-8.  
  
```  
<QueueMessage>  
    <MessageText>message-content</MessageText>  
</QueueMessage>  
```  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 204 (No Content).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Queue service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
|`x-ms-popreceipt`|The pop receipt of the queue message.|  
|`x-ms-time-next-visible`|A UTC date/time value that represents when the message will be visible on the queue.|  
  
### Response Body  
 None.  
  
## Authorization  
 This operation can be performed by the account owner and by anyone with a shared access signature that has permission to perform this operation.  
  
## Sample Request and Response  
 The following request extends the visibility of a queue message by 30 seconds and updates its content.  
  
```  
PUT https://myaccount.queue.core.windows.net/myqueue/messages/663d89aa-d1d9-42a2-9a6a-fcf822a97d2c?popreceipt=AgAAAAEAAAApAAAAGIw6Q29bzAE%3d&visibilitytimeout=30&timeout=30 HTTP/1.1  
  
```  
  
 The request is sent with the following headers:  
  
```  
x-ms-version: 2011-08-18  
x-ms-date: Mon, 29 Aug 2011 17:17:21 GMT  
Authorization: SharedKey myaccount:batcrWZ35InGCZeTUFWMdIQiOZPCW7UEyeGdDOg7WW4=  
Content-Length: 75  
```  
  
 The request is sent with the following XML body:  
  
```  
<QueueMessage>  
    <MessageText>new-message-content</MessageText>  
</QueueMessage>  
```  
  
 After the request has been sent, the following response is returned:  
  
```  
HTTP/1.1 204 No Content  
Content-Length: 0  
Server: Windows-Azure-Queue/1.0 Microsoft-HTTPAPI/2.0  
x-ms-request-id: df34a7dd-3cbe-4206-a586-d6de3cf225a7  
x-ms-version: 2011-08-18  
x-ms-popreceipt: AwAAAAIAAAApAAAAINtMQ29bzAEBAAAA  
x-ms-time-next-visible: Mon, 29 Aug 2011 17:17:51 GMT  
Date: Mon, 29 Aug 2011 17:17:21 GMT  
```  
  
## Remarks  
 An `Update Message` operation will fail if the specified message does not exist in the queue, or if the specified pop receipt does not match the message.  
  
 A pop receipt is returned by the `Get Messages` operation or the `Update Message` operation. Pop receipts remain valid until one of the following events occurs:  
  
1.  The message has expired.  
  
2.  The message has been deleted using the last pop receipt received either from `Get Messages` or `Update Message`.  
  
3.  The invisibility time has elapsed and the message has been dequeued by a `Get Messages` request. When the invisibility time elapses, the message becomes visible again. If it is retrieved by another `Get Messages` request, the returned pop receipt can be used to delete or update the message.  
  
4.  The message has been updated with a new visibility timeout. When the message is updated, a new pop receipt will be returned.  
  
 The `Update Message` operation can be used to continually extend the invisibility of a queue message. This functionality can be useful if you want a worker role to “lease” a queue message. For example, if a worker role calls [Get Messages](../StorageServicesREST/Get-Messages.md) and recognizes that it needs more time to process a message, it can continually extend the message’s invisibility until it is processed. If the worker role were to fail during processing, eventually the message would become visible again and another worker role could process it.  
  
## See Also  
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Queue Service Error Codes](../StorageServicesREST/Queue-Service-Error-Codes.md)
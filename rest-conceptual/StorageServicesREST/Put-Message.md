---
title: "Put Message"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 0a3c4fcc-0b0b-4331-87a1-01d13f3de86e
caps.latest.revision: 54
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
# Put Message
The `Put Message` operation adds a new message to the back of the message queue. A visibility timeout can also be specified to make the message invisible until the visibility timeout expires. A message must be in a format that can be included in an XML request with UTF-8 encoding. The encoded message can be up to 64 KB in size for versions 2011-08-18 and newer, or 8 KB in size for previous versions.  
  
## Request  
 The `Put Message` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account, and `myqueue` with the name of your queue:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`POST`|`https://myaccount.queue.core.windows.net/myqueue/messages?visibilitytimeout=<int-seconds>&messagettl=<int-seconds>`|HTTP/1.1|  
  
### Emulated Storage Service  
 This operation and the optional `visibilitytimeout` parameter are supported for SDK 1.6 and newer versions.  
  
 When making a request against the emulated storage service, specify the emulator hostname and Queue service port as `127.0.0.1:10001`, followed by the emulated storage account name:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`POST`|`http://127.0.0.1:10001/devstoreaccount1/myqueue/messages?visibilitytimeout=<int-seconds>&messagettl=<int-seconds>`|HTTP/1.1|  
  
### URI Parameters  
 The following parameters may be specified on the request URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`visibilitytimeout=<int=seconds>`|Optional. If specified, the request must be made using an `x-ms-version` of 2011-08-18 or newer. If not specified, the default value is 0. Specifies the new visibility timeout value, in seconds, relative to server time. The new value must be larger than or equal to 0, and cannot be larger than 7 days. The visibility timeout of a message cannot be set to a value later than the expiry time. `visibilitytimeout` should be set to a value smaller than the time-to-live value.|  
|`messagettl=<int-seconds>`|Optional. Specifies the time-to-live interval for the message, in seconds. The maximum time-to-live allowed is 7 days. If this parameter is omitted, the default time-to-live is 7 days.|  
|`timeout`|Optional. The `timeout` parameter is expressed in seconds. For more information, see [Setting Timeouts for Queue Service Operations](../StorageServicesREST/Setting-Timeouts-for-Queue-Service-Operations.md).|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` `or x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Optional. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
### Request Body  
 The body of the request contains the message data in the following XML format. Note that the message content must be in a format that may be encoded with UTF-8.  
  
```  
<QueueMessage>  
    <MessageText>message-content</MessageText>  
</QueueMessage>  
```  
  
### Sample Request  
  
```  
Request:  
POST https://myaccount.queue.core.windows.net/messages?visibilitytimeout=30&timeout=30 HTTP/1.1  
  
Headers:  
x-ms-version: 2011-08-18  
x-ms-date: Tue, 30 Aug 2011 01:03:21 GMT  
Authorization: SharedKey myaccount:sr8rIheJmCd6npMSx7DfAY3L//V3uWvSXOzUBCV9wnk=  
Content-Length: 100  
  
Body:  
<QueueMessage>  
<MessageText>PHNhbXBsZT5zYW1wbGUgbWVzc2FnZTwvc2FtcGxlPg==</MessageText>  
</QueueMessage>  
```  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 201 (Created).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Queue service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
### Response Body  
 None.  
  
## Authorization  
 This operation can be performed by the account owner and by anyone with a shared access signature that has permission to perform this operation.  
  
## Remarks  
 The optional visibility timeout specifies the time that the message will be invisible. After the timeout expires, the message will become visible. If a visibility timeout is not specified, the default value of 0 is used.  
  
 The optional message time-to-live specifies how long a message will remain in the queue. The message will be deleted from the queue when the time-to-live period expires.  
  
 A message must be in a format that can be included in an XML request with UTF-8 encoding. To include markup in the message, the contents of the message must either be XML-escaped or Base64-encode. Any XML markup in the message that is not escaped or encoded will be removed before the message is added to the queue.  
  
 If the message is too large, the service returns status code 400 (Bad Request).  
  
## See Also  
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Queue Service Error Codes](../StorageServicesREST/Queue-Service-Error-Codes.md)
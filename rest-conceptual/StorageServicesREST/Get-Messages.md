---
title: "Get Messages"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: d4c13c95-acaa-47ff-940e-f8038da44fad
caps.latest.revision: 62
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
# Get Messages
The `Get Messages` operation retrieves one or more messages from the front of the queue.  
  
## Request  
 The `Get Messages` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account, and `myqueue` with the name of your queue:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`GET`|`https://myaccount.queue.core.windows.net/myqueue/messages`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Queue service port as `127.0.0.1:10001`, followed by the emulated storage account name:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`GET`|`http://127.0.0.1:10001/devstoreaccount1/myqueue/messages`|HTTP/1.1|  
  
### URI Parameters  
 The following additional parameters may be specified on the request URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`numofmessages`|Optional. A nonzero integer value that specifies the number of messages to retrieve from the queue, up to a maximum of 32. If fewer are visible, the visible messages are returned. By default, a single message is retrieved from the queue with this operation.|  
|`visibilitytimeout`|Optional. Specifies the new visibility timeout value, in seconds, relative to server time. The default value is 30 seconds.<br /><br /> A specified value must be larger than or equal to 1 second, and cannot be larger than 7 days, or larger than 2 hours on REST protocol versions prior to version 2011-08-18. The visibility timeout of a message can be set to a value later than the expiry time.|  
|`timeout`|Optional. The `timeout` parameter is expressed in seconds. For more information, see [Setting Timeouts for Queue Service Operations](../StorageServicesREST/Setting-Timeouts-for-Queue-Service-Operations.md).|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Optional. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
### Request Body  
 None.  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 200 (OK).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Queue service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
### Response Body  
 The response XML for the `Get Messages` operation is returned in the following format.  
  
 The `MessageID` element is a GUID value that identifies the message in the queue. This value is assigned to the message by the Queue service and is opaque to the client. This value may be used together with the value of the `PopReceipt` element to delete a message from the queue after it has been retrieved with the `Get Messages` operation. The value of `PopReceipt` is also opaque to the client; its only purpose is to ensure that a message may be deleted with the [Delete Message](../StorageServicesREST/Delete-Message2.md) operation.  
  
 The `InsertionTime`, `ExpirationTime`, and `TimeNextVisible` elements are represented as UTC values and formatted as described in RFC 1123.  
  
 The `DequeueCount` element has a value of 1 the first time the message is dequeued. This value is incremented each time the message is subsequently dequeued.  
  
> [!NOTE]
>  The `DequeueCount` element is returned in the response body only if the queue was created with version 2009-09-19 of the Queue service.  
  
```xml  
<QueueMessagesList>  
    <QueueMessage>  
      <MessageId>string-message-id</MessageId>  
      <InsertionTime>insertion-time</InsertionTime>  
      <ExpirationTime>expiration-time</ExpirationTime>  
      <PopReceipt>opaque-string-receipt-data</PopReceipt>  
      <TimeNextVisible>time-next-visible</TimeNextVisible>  
      <DequeueCount>integer</DequeueCount>  
      <MessageText>message-body</MessageText>  
    </QueueMessage>  
</QueueMessagesList>  
```  
  
### Sample Response  
  
```  
Response Status:  
HTTP/1.1 200 OK  
Response Headers:  
Transfer-Encoding: chunked  
Content-Type: application/xml  
Date: Fri, 16 Sep 2011 21:04:30 GMT  
Server: Windows-Azure-Queue/1.0 Microsoft-HTTPAPI/2.0  
  
Response Body:  
﻿<?xml version="1.0" encoding="utf-8"?>  
<QueueMessagesList>  
  <QueueMessage>  
    <MessageId>5974b586-0df3-4e2d-ad0c-18e3892bfca2</MessageId>  
    <InsertionTime>Fri, 09 Oct 2009 21:04:30 GMT</InsertionTime>  
    <ExpirationTime>Fri, 16 Oct 2009 21:04:30 GMT</ExpirationTime>  
    <PopReceipt>YzQ4Yzg1MDItYTc0Ny00OWNjLTkxYTUtZGM0MDFiZDAwYzEw</PopReceipt>  
    <TimeNextVisible>Fri, 09 Oct 2009 23:29:20 GMT</TimeNextVisible>  
    <DequeueCount>1</DequeueCount>  
    <MessageText>PHRlc3Q+dGhpcyBpcyBhIHRlc3QgbWVzc2FnZTwvdGVzdD4=</MessageText>  
  </QueueMessage>  
</QueueMessagesList>  
```  
  
## Authorization  
 This operation can be performed by the account owner and by anyone with a shared access signature that has permission to perform this operation.  
  
## Remarks  
 The message content is retrieved in whatever format was used for the [Put Message](../StorageServicesREST/Put-Message.md) operation.  
  
 When a message is retrieved from the queue, the response includes the message and a pop receipt value, which is required to delete the message. The message is not automatically deleted from the queue, but after it has been retrieved, it is not visible to other clients for the time interval specified by the `visibilitytimeout` parameter.  
  
 If multiple messages are retrieved, each message has an associated pop receipt. The maximum number of messages that may be retrieved at a time is 32.  
  
 The client that retrieves the message is expected to delete the message after it has been processed, and before the time specified by the `TimeNextVisible` element of the response, which is calculated based on the value of the `visibilitytimeout` parameter. The value of `visibilitytimeout` is added to the time at which the message is retrieved to determine the value of `TimeNextVisible`.  
  
 A message that is retrieved with a certain `visibilitytimeout` can reappear again before that specified timeout has elapsed, due to clock skew. Note that a client could infer that a message has already been dequeued by a different client based on the pop receipt, which is unique for each dequeueing of a message. If a client’s pop receipt no longer works to delete or update a message, and the client receives a 404 (Not Found) error, then the message has been dequeued by another client.  
  
 Typically, when a consumer retrieves a message via `Get Messages`, that message is usually reserved for deletion until the *visibilitytimeout* interval expires, but this behavior is not guaranteed. After the *visibilitytimeout* interval expires, the message again becomes visible to other consumers. If the message is not subsequently retrieved and deleted by another consumer, the original consumer can delete the message using the original pop receipt.  
  
 When a message is retrieved for the first time, its `DequeueCount` property is set to 1. If it is not deleted and is subsequently retrieved again, the `DequeueCount` property is incremented. The client may use this value to determine how many times a message has been retrieved.  
  
 If the *visiblitytimeout* or *numofmessages* parameter is out of range, the service returns status code 400 (Bad Request), along with additional error information, as shown in the following example.  
  
```  
  
HTTP/1.1 400 One of the query parameters specified in the request URI is outside the permissible range.  
Connection: Keep-Alive  
Content-Length: 455  
Via: 1.1 TK5-PRXY-22  
Date: Wed, 02 May 2012 19:37:23 GMT  
Content-Type: application/xml  
Server: Windows-Azure-Queue/1.0 Microsoft-HTTPAPI/2.0  
x-ms-request-id: 6a03526c-ca2c-4358-a63a-b5d096988533  
x-ms-version: 2011-08-18  
  
<?xml version="1.0" encoding="utf-8"?>  
   <Error>  
      <Code>OutOfRangeQueryParameterValue</Code>  
      <Message>One of the query parameters specified in the request URI is outside the permissible range.  
               RequestId:6a03526c-ca2c-4358-a63a-b5d096988533  
               Time:2012-05-02T19:37:24.2438463Z  
      </Message>  
     <QueryParameterName>numofmessages</QueryParameterName>  
     <QueryParameterValue>0</QueryParameterValue>  
     <MinimumAllowed>1</MinimumAllowed>  
     <MaximumAllowed>32</MaximumAllowed>  
   </Error>  
  
```  
  
## See Also  
 [Queue Service Error Codes](../StorageServicesREST/Queue-Service-Error-Codes.md)   
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)
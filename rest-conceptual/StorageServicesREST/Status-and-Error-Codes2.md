---
title: "Status and Error Codes2"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
H1: Status and Error Codes
ms.assetid: 4421ac96-38eb-4ea3-8104-f9975c3bf153
caps.latest.revision: 31
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
# Status and Error Codes2
REST API operations for Azure storage services return standard HTTP status codes, as defined in the [HTTP/1.1 Status Code Definitions](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html).  
  
 API operations may also return additional error information that is defined by the storage service. This additional error information is returned in the response body.  
  
 The body of the error response follows the basic format shown here. The `code` element indicates the storage service error code string, whereas the `message` element indicates the error message string.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<Error>  
  <Code>string-value</Code>  
  <Message>string-value</Message>  
</Error>  
```  
  
 A given error response may also include additional error information to provide the developer with more information about the error. For example, the following error response indicates that a query parameter specified on the request URI was invalid, and provides additional information about the invalid parameter's name and value and the reason for the error.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<Error>  
  <Code>InvalidQueryParameterValue</Code>  
  <Message>Value for one of the query parameters specified in the request URI is invalid.</Message>  
  <QueryParameterName>popreceipt</QueryParameterName>  
  <QueryParameterValue>33537277-6a52-4a2b-b4eb-0f905051827b</QueryParameterValue>  
  <Reason>invalid receipt format</Reason>  
</Error>  
```  
  
 The following topics provide lists of error codes for the Blob, Queue, Table, and File services:  
  
-   [Common REST API Error Codes](../StorageServicesREST/Common-REST-API-Error-Codes.md)  
  
-   [Blob Service Error Codes](../StorageServicesREST/Blob-Service-Error-Codes.md)  
  
-   [Queue Service Error Codes](../StorageServicesREST/Queue-Service-Error-Codes.md)  
  
-   [Table Service Error Codes](../StorageServicesREST/Table-Service-Error-Codes.md)  
  
-   [File Service Error Codes](../StorageServicesREST/File-Service-Error-Codes.md)  
  
## Error Responses for the Table Service  
 Error responses for the Table service include the storage services error code and message elements, as shown above, but are also compliant with the error format described in section 19 of the [OData specification](http://go.microsoft.com/fwlink/?LinkId=301473). Additional error information may be included in the response in addition to the storage services error code and message, but the error response will always comply with the OData spec.  
  
 Batch error responses are similar to standard Table service error responses and are described in detail in [Performing Entity Group Transactions](../StorageServicesREST/Performing-Entity-Group-Transactions.md).  
  
> [!NOTE]
>  JSON is the recommended payload format for Table service operations, and is the only format supported for versions 2015-12-11 and later.  
  
 **Basic Error Body in JSON Format (versions 2013-08-15 and later)**  
  
```  
{"odata.error":{"code":"ResourceNotFound","message":{"lang":"en-US","value":"The specified resource does not exist.\nRequestId:102a2b55-eb35-4254-9daf-854db78a47bd\nTime:2014-06-04T16:18:20.4307735Z"}}}  
  
```  
  
 **Basic Error Body in Atom Format (versions prior to 2015-12-11)**  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<error xmlns="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">  
  <code>ResourceNotFound</code>  
  <message xml:lang="en-US">The specified resource does not exist.  
RequestId:e288ba1e-f5dd-4014-9e09-f1263d223dec  
Time:2014-06-04T16:18:20.7088013Z</message>  
</error>  
  
```  
  
## See Also  
 [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md)   
 [HttpStatusCode Enumeration](http://go.microsoft.com/fwlink/?LinkId=152845)   
 [Storage Services REST](../StorageServicesREST/Azure-Storage-Services-REST-API-Reference.md)
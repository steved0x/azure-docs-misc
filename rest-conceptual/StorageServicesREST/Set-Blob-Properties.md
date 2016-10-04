---
title: "Set Blob Properties"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 6e063a14-8ed5-4401-bd3b-ec3de4f7d74c
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
# Set Blob Properties
The `Set Blob Properties` operation sets system properties on the blob.  
  
## Request  
 The `Set Blob Properties` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
||PUT Method Request URI|HTTP Version|  
|-|----------------------------|------------------|  
||`https://myaccount.blob.core.windows.net/mycontainer/myblob?comp=properties`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Blob service port as `127.0.0.1:10000`, followed by the emulated storage account name:  
  
||PUT Method Request URI|HTTP Version|  
|-|----------------------------|------------------|  
||`http://127.0.0.1:10000/ devstoreaccount1/mycontainer/myblob?comp=properties`|HTTP/1.1|  
  
 For more information, see [Using the Azure Storage Emulator for Development and Testing](assetId:///f0e3acde-f019-4148-9544-34cf2ff27211).  
  
### URI Parameters  
 The following additional parameters may be specified on the request URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`timeout`|Optional. The `timeout` parameter is expressed in seconds. For more information, see [Setting Timeouts for Blob Service Operations](../StorageServicesREST/Setting-Timeouts-for-Blob-Service-Operations.md).|  
  
### Request Headers (All Blob Types)  
 The following table describes required and optional request headers for all blob types.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Required for all authenticated requests. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-blob-cache-control`|Optional. Modifies the cache control string for the blob.<br /><br /> If this property is not specified on the request, then the property will be cleared for the blob. Subsequent calls to [Get Blob Properties](../StorageServicesREST/Get-Blob-Properties.md) will not return this property, unless it is explicitly set on the blob again.|  
|`x-ms-blob-content-type`|Optional. Sets the blob’s content type.<br /><br /> If this property is not specified on the request, then the property will be cleared for the blob. Subsequent calls to [Get Blob Properties](../StorageServicesREST/Get-Blob-Properties.md) will not return this property, unless it is explicitly set on the blob again.|  
|`x-ms-blob-content-md5`|Optional. Sets the blob's MD5 hash.<br /><br /> If this property is not specified on the request, then the property will be cleared for the blob. Subsequent calls to [Get Blob Properties](../StorageServicesREST/Get-Blob-Properties.md) will not return this property, unless it is explicitly set on the blob again.|  
|`x-ms-blob-content-encoding`|Optional. Sets the blob's content encoding.<br /><br /> If this property is not specified on the request, then the property will be cleared for the blob. Subsequent calls to [Get Blob Properties](../StorageServicesREST/Get-Blob-Properties.md) will not return this property, unless it is explicitly set on the blob again.|  
|`x-ms-blob-content-language`|Optional. Sets the blob's content language.<br /><br /> If this property is not specified on the request, then the property will be cleared for the blob. Subsequent calls to [Get Blob Properties](../StorageServicesREST/Get-Blob-Properties.md) will not return this property, unless it is explicitly set on the blob again.|  
|`x-ms-lease-id:<ID>`|Required if the blob has an active lease. To perform this operation on a blob with an active lease, specify the valid lease ID for this header.|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
|`x-ms-blob-content-disposition`|Optional. Sets the blob’s `Content-Disposition` header. Available for versions 2013-08-15 and later.<br /><br /> The `Content-Disposition` response header field conveys additional information about how to process the response payload, and also can be used to attach additional metadata. For example, if set to `attachment`, it indicates that the user-agent should not display the response, but instead show a **Save As** dialog with a filename other than the blob name specified.<br /><br /> The response from the [Get Blob](../StorageServicesREST/Get-Blob.md) and [Get Blob Properties](../StorageServicesREST/Get-Blob-Properties.md) operations includes the `content-disposition` header.|  
|`Origin`|Optional. Specifies the origin from which the request is issued. The presence of this header results in cross-origin resource sharing headers on the response. See [CORS Support for the Storage Services](../StorageServicesREST/Cross-Origin-Resource-Sharing--CORS--Support-for-the-Azure-Storage-Services.md) for details.|  
  
 This operation also supports the use of conditional headers to set blob properties only if a specified condition is met. For more information, see [Specifying Conditional Headers for Blob Service Operations](../StorageServicesREST/Specifying-Conditional-Headers-for-Blob-Service-Operations.md).  
  
### Request Headers (Page Blobs Only)  
 The following table describes request headers applicable only for operations on page blobs.  
  
|Request header|Description|  
|--------------------|-----------------|  
|`x-ms-blob-content-length: byte value`|Optional. Resizes a page blob to the specified size. If the specified value is less than the current size of the blob, then all pages above the specified value are cleared.<br /><br /> This property cannot be used to change the size of a block blob or an append blob. Setting this property for a block blob or an append blob returns status code 400 (Bad Request).|  
|`x-ms-sequence-number-action: {max, update, increment}`|Optional, but required if the `x-ms-blob-sequence-number` header is set for the request. This property applies to page blobs only.<br /><br /> This property indicates how the service should modify the blob's sequence number. Specify one of the following options for this property:<br /><br /> -   `max`: Sets the sequence number to be the higher of the value included with the request and the value currently stored for the blob.<br />-   `update`: Sets the sequence number to the value included with the request.<br />-   `increment`: Increments the value of the sequence number by 1. If specifying this option, do not include the `x-ms-blob-sequence-number header`; doing so will return status code 400 (Bad Request).|  
|`x-ms-blob-sequence-number: <num>`|Optional, but required if the `x-ms-sequence-number-action` property is set to `max` or `update`. This property applies to page blobs only.<br /><br /> This property sets the blob's sequence number. The sequence number is a user-controlled property that you can use to track requests and manage concurrency issues. For more information, see the [Put Page](../StorageServicesREST/Put-Page.md) operation.<br /><br /> Use this property together with the `x-ms-sequence-number-action` to update the blob's sequence number, either to the specified value or to the higher of the values specified with the request or currently stored with the blob. This header should not be specified if `x-ms-sequence-number-action` is set to `increment`; in this case the service automatically increments the sequence number by one.<br /><br /> To set the sequence number to a value of your choosing, this property must be specified on the request together with `x-ms-sequence-number-action`.|  
  
### Request Body  
 None.  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 200 (OK).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Syntax|Description|  
|------------|-----------------|  
|`ETag`|The ETag contains a value that you can use to perform operations conditionally. See [Specifying Conditional Headers for Blob Service Operations](../StorageServicesREST/Specifying-Conditional-Headers-for-Blob-Service-Operations.md) for more information. If the request version is 2011-08-18 or newer, the ETag value will be in quotes.|  
|`Last-Modified`|The date/time that the blob was last modified. The date format follows RFC 1123. For more information, see [Representation of Date-Time Values in Headers](../StorageServicesREST/Representation-of-Date-Time-Values-in-Headers.md).<br /><br /> Any write operation on the blob (including updates on the blob's metadata or properties) changes the last modified time of the blob.|  
|`x-ms-blob-sequence-number`|If the blob is a page blob, the blob's current sequence number is returned with this header.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Blob service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
|`Access-Control-Allow-Origin`|Returned if the request includes an `Origin` header and CORS is enabled with a matching rule. This header returns the value of the origin request header in case of a match.|  
|`Access-Control-Expose-Headers`|Returned if the request includes an `Origin` header and CORS is enabled with a matching rule. Returns the list of response headers that are to be exposed to the client or issuer of the request.|  
|`Access-Control-Allow-Credentials`|Returned if the request includes an `Origin` header and CORS is enabled with a matching rule that does not allow all origins. This header will be set to true.|  
  
### Response Body  
 None.  
  
## Authorization  
 This operation can only be called by the account owner and by anyone with a Shared Access Signature that has permission to write to this blob or its container.  
  
## Remarks  
 The semantics for updating a blob's properties are as follows:  
  
-   A page blob's sequence number is updated only if the request meets either of the following conditions:  
  
    -   The request sets the `x-ms-sequence-number-action` to `max` or `update`, and also specifies a value for the `x-ms-blob-sequence-number` header.  
  
    -   The request sets the `x-ms-sequence-number-action` to `increment`, indicating that the service should increment the sequence number by one.  
  
-   A page blob's size is modified only if the request specifies a value for the `x-ms-content-length` header.  
  
-   If a request sets only `x-ms-blob-sequence-number` and/or `x-ms-content-length`, and no other properties, then none of the blob's other properties are modified.  
  
-   If any one or more of the following properties is set in the request, then all of these properties are set together. If a value is not provided for a given property when at least one of the properties listed below is set, then that property will be cleared for the blob.  
  
    -   `x-ms-blob-cache-control`  
  
    -   `x-ms-blob-content-type`  
  
    -   `x-ms-blob-content-md5`  
  
    -   `x-ms-blob-content-encoding`  
  
    -   `x-ms-blob-content-language`  
  
    -   `x-ms-blob-content-disposition`  
  
 Note that for a shared access signature, you can override certain properties stored for the blob by specifying query parameters as part of the shared access signature. These properties include the `cache-control`, `content-type`, `content-encoding`, `content-language`, and `content-disposition` properties. For more information, see [Constructing a Service SAS](../StorageServicesREST/Constructing-a-Service-SAS.md).  
  
## See Also  
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)
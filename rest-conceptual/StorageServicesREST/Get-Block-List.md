---
title: "Get Block List"
ms.custom: na
ms.date: 2016-08-03
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 608f2eb2-c3b6-4c23-98d2-64c99f5a3c98
caps.latest.revision: 71
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
# Get Block List
The `Get Block List` operation retrieves the list of blocks that have been uploaded as part of a block blob.  
  
 There are two block lists maintained for a blob:  
  
-   **Committed Block List:** The list of blocks that have been successfully committed to a given blob with [Put Block List](../StorageServicesREST/Put-Block-List.md).  
  
-   **Uncommitted Block List:** The list of blocks that have been uploaded for a blob using [Put Block](../StorageServicesREST/Put-Block.md), but that have not yet been committed. These blocks are stored in Azure in association with a blob, but do not yet form part of the blob.  
  
 You can call `Get Block List` to return the committed block list, the uncommitted block list, or both lists. You can also call this operation to retrieve the committed block list for a snapshot.  
  
## Request  
 The `Get Block List` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
|GET Method Request URI|HTTP Version|  
|----------------------------|------------------|  
|`https://myaccount.blob.core.windows.net/mycontainer/myblob?comp=blocklist`<br /><br /> `https://myaccount.blob.core.windows.net/mycontainer/myblob?comp=blocklist&snapshot=<DateTime>`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Blob service port as `127.0.0.1:10000`, followed by the emulated storage account name:  
  
|GET Method Request URI|HTTP Version|  
|----------------------------|------------------|  
|`http://127.0.0.1:10000/devstoreaccount1/mycontainer/myblob?comp=blocklist`|HTTP/1.1|  
  
 For more information, see [Using the Azure Storage Emulator for Development and Testing](assetId:///f0e3acde-f019-4148-9544-34cf2ff27211).  
  
### URI Parameters  
 The following additional parameters may be specified on the request URI.  
  
|URI Parameter|Description|  
|-------------------|-----------------|  
|`snapshot`|Optional. The snapshot parameter is an opaque `DateTime` value that, when present, specifies the blob list to retrieve. For more information on working with blob snapshots, see [Creating a Snapshot of a Blob](../StorageServicesREST/Creating-a-Snapshot-of-a-Blob.md).|  
|`blocklisttype`|Specifies whether to return the list of committed blocks, the list of uncommitted blocks, or both lists together. Valid values are `committed`, `uncommitted`, or `all`. If you omit this parameter, `Get Block List` returns the list of committed blocks.|  
|`timeout`|Optional. The `timeout` parameter is expressed in seconds. For more information, see [Setting Timeouts for Blob Service Operations](../StorageServicesREST/Setting-Timeouts-for-Blob-Service-Operations.md).|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Required for all authenticated requests, optional for anonymous requests. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-lease-id:<ID>`|Optional. If this header is specified, the operation will be performed only if both of the following conditions are met:<br /><br /> -   The blob's lease is currently active.<br />-   The lease ID specified in the request matches that of the blob.<br /><br /> If this header is specified and both of these conditions are not met, the request will fail and the operation will fail with status code 412 (Precondition Failed).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
### Request Body  
 None.  
  
### Sample Request  
 The following sample request URI returns the committed block list for a blob named MOV1.avi:  
  
```  
GET http://myaccount.blob.core.windows.net/movies/MOV1.avi?comp=blocklist&blocklisttype=committed HTTP/1.1  
```  
  
 The following sample request URI returns both the committed and the uncommitted block list:  
  
```  
GET http://myaccount.blob.core.windows.net/movies/MOV1.avi?comp=blocklist&blocklisttype=all HTTP/1.1  
```  
  
 The following sample request URI returns the committed block list for a snapshot. Note that a snapshot consists only of committed blocks, so there are no uncommitted blocks associated with it.  
  
```  
GET http://myaccount.blob.core.windows.net/mycontainer/myblob?comp=blocklist&snapshot=2009-09-30T20%3a11%3a15.2735974Z  
```  
  
## Response  
 The response includes an HTTP status code, a set of response headers, and a response body containing the list of blocks.  
  
### Status Code  
 A successful operation returns status code 200 (OK).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`Last-Modified`|The date/time that the blob was last modified. The date format follows RFC 1123. See [Representation of Date-Time Values in Headers](../StorageServicesREST/Representation-of-Date-Time-Values-in-Headers.md) for more information. This header is returned only if the blob has committed blocks.<br /><br /> Any operation that modifies the blob, including updates to the blob's metadata or properties, changes the last modified time of the blob.|  
|`ETag`|The ETag for the blob. This header is returned only if the blob has committed blocks.|  
|`Content-Type`|The MIME content type of the blob. The default value is `application/xml`.|  
|`x-ms-blob-content-length`|The size of the blob in bytes.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Blob service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.<br /><br /> This header is also returned for anonymous requests without a version specified if the container was marked for public access using the 2009-09-19 version of the Blob service. Note that only the committed block list can be returned via an anonymous request.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
 This operation also supports the use of conditional headers to get the block list only if a specified condition is met. For more information, see [Specifying Conditional Headers for Blob Service Operations](../StorageServicesREST/Specifying-Conditional-Headers-for-Blob-Service-Operations.md).  
  
### Response Body  
 The format of the response body for a request that returns only committed blocks is as follows:  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<BlockList>  
  <CommittedBlocks>  
    <Block>  
      <Name>base64-encoded-block-id</Name>  
      <Size>size-in-bytes</Size>  
    </Block>  
  <CommittedBlocks>  
</BlockList>  
```  
  
 The format of the response body for a request that returns both committed and uncommitted blocks is as follows:  
  
```  
  
<?xml version="1.0" encoding="utf-8"?>  
<BlockList>  
  <CommittedBlocks>  
     <Block>  
        <Name>base64-encoded-block-id</Name>  
        <Size>size-in-bytes</Size>  
     </Block>  
  </CommittedBlocks>  
  <UncommittedBlocks>  
    <Block>  
      <Name>base64-encoded-block-id</Name>  
      <Size>size-in-bytes</Size>  
    </Block>  
  </UncommittedBlocks>  
 </BlockList>  
  
```  
  
### Sample Response  
 In the following example, the `blocklisttype` parameter was set to `committed`, so only the blob's committed blocks are returned in the response.  
  
```  
HTTP/1.1 200 OK  
Transfer-Encoding: chunked  
Content-Type: application/xml  
Server: Windows-Azure-Blob/1.0 Microsoft-HTTPAPI/2.0  
x-ms-request-id: 42da571d-34f4-4d3e-b53e-59a66cb36f23  
Date: Sun, 25 Sep 2011 00:33:19 GMT  
  
<?xml version="1.0" encoding="utf-8"?>  
<BlockList>  
  <CommittedBlocks>  
    <Block>  
      <Name>BlockId001</Name>  
      <Size>4194304</Size>  
    </Block>  
    <Block>  
      <Name>BlockId002</Name>  
      <Size>4194304</Size>  
    </Block>  
  </CommittedBlocks>  
</BlockList>  
```  
  
 In this example, the `blocklisttype` parameter was set to `all`, and both the blob's committed and uncommitted blocks are returned in the response.  
  
```  
HTTP/1.1 200 OK  
Transfer-Encoding: chunked  
Content-Type: application/xml  
Server: Windows-Azure-Blob/1.0 Microsoft-HTTPAPI/2.0  
x-ms-request-id: 42da571d-34f4-4d3e-b53e-59a66cb36f23  
Date: Sun, 25 Sep 2011 00:35:56 GMT  
  
<?xml version="1.0" encoding="utf-8"?>  
<BlockList>  
  <CommittedBlocks>  
    <Block>  
      <Name>BlockId001</Name>  
      <Size>4194304</Size>  
    </Block>  
    <Block>  
      <Name>BlockId002</Name>  
      <Size>4194304</Size>  
    </Block>  
  </CommittedBlocks>  
  <UncommittedBlocks>  
    <Block>  
      <Name>BlockId003</Name>  
      <Size>4194304</Size>  
    </Block>  
    <Block>  
      <Name>BlockId004</Name>  
      <Size>1024000</Size>  
    </Block>  
  </UncommittedBlocks>  
</BlockList>  
```  
  
 In this next example, the `blocklisttype` parameter was set to `all`, but the blob has not yet been committed, so the `CommittedBlocks` element is empty.  
  
```  
HTTP/1.1 200 OK  
Transfer-Encoding: chunked  
Content-Type: application/xml  
Server: Windows-Azure-Blob/1.0 Microsoft-HTTPAPI/2.0  
x-ms-request-id: 42da571d-34f4-4d3e-b53e-59a66cb36f23  
Date: Wed, 14 Sep 2011 00:40:22 GMT  
  
<?xml version="1.0" encoding="utf-8"?>  
<BlockList>  
  <CommittedBlocks />  
  <UncommittedBlocks>  
    <Block>  
      <Name>BlockId001</Name>  
      <Size>1024</Size>  
    </Block>  
    <Block>  
      <Name>BlockId002</Name>  
      <Size>1024</Size>  
    </Block>  
    <Block>  
      <Name>BlockId003</Name>  
      <Size>1024</Size>  
    </Block>  
    <Block>  
      <Name>BlockId004</Name>  
      <Size>1024</Size>  
    </Block>  
  </UncommittedBlocks>  
</BlockList>  
```  
  
## Authorization  
 If the container's ACL is set to allow anonymous access, any client may call `Get Block List`; however, only committed blocks can be accessed publicly. Access to the uncommitted block list is restricted to the account owner and to anyone using a Shared Access Signature that has permission to read this blob or its container.  
  
## Remarks  
 Call `Get Block List` to return the list of blocks that have been committed to a block blob, the list of blocks that have not yet been committed, or both lists. Use the `blocklisttype` parameter to specify which list of blocks to return.  
  
 The list of committed blocks is returned in the same order that they were committed by the [Put Block List](../StorageServicesREST/Put-Block-List.md) operation. No block may appear more than once in the committed block list.  
  
 You can use the uncommitted block list to determine which blocks are missing from the blob in cases where calls to `Put Block` or `Put Block List` have failed. The list of uncommitted blocks is returned in alphabetical order. If a block ID has been uploaded more than once, only the most recently uploaded block appears in the list.  
  
 Note that when a blob has not yet been committed, calling `Get Block List` with `blocklisttype=all` returns the uncommitted blocks, and the `CommittedBlocks` element is empty.  
  
 `Get Block List` does not support concurrency when reading the list of uncommitted blocks.  Calls to `Get Block List` where `blocklisttype=uncommitted` or `blocklisttype=all` have a lower maximum request rate than other read operations. For details on target throughput for read operations, see [Azure Storage Scalability and Performance Targets](https://azure.microsoft.com/en-us/documentation/articles/storage-scalability-targets/).  
  
 `Get Block List` applies only to block blobs. Calling `Get Block List` on a page blob results in status code 400 (Bad Request).  
  
## See Also  
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Blob Service Error Codes](../StorageServicesREST/Blob-Service-Error-Codes.md)   
 [Setting Timeouts for Blob Service Operations](../StorageServicesREST/Setting-Timeouts-for-Blob-Service-Operations.md)
---
title: "List Blobs"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: fa4760a6-5343-4aa1-b484-df823ce817e7
caps.latest.revision: 88
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
# List Blobs
The `List Blobs` operation enumerates the list of blobs under the specified container.  
  
## Request  
 The `List Blobs` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`GET`|`https://myaccount.blob.core.windows.net/mycontainer?restype=container&comp=list`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Blob service port as `127.0.0.1:10000`, followed by the emulated storage account name:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`GET`|`http://127.0.0.1:10000/devstoreaccount1/mycontainer?restype=container&comp=list`|HTTP/1.1|  
  
 For more information, see [Using the Azure Storage Emulator for Development and Testing](assetId:///f0e3acde-f019-4148-9544-34cf2ff27211).  
  
### URI Parameters  
 The following additional parameters may be specified on the URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`prefix`|Optional. Filters the results to return only blobs whose names begin with the specified prefix.|  
|`delimiter`|Optional. When the request includes this parameter, the operation returns a `BlobPrefix` element in the response body that acts as a placeholder for all blobs whose names begin with the same substring up to the appearance of the delimiter character. The delimiter may be a single character or a string.|  
|`marker`|Optional. A string value that identifies the portion of the list to be returned with the next list operation. The operation returns a marker value within the response body if the list returned was not complete. The marker value may then be used in a subsequent call to request the next set of list items.<br /><br /> The marker value is opaque to the client.|  
|`maxresults`|Optional. Specifies the maximum number of blobs to return, including all `BlobPrefix` elements. If the request does not specify `maxresults` or specifies a value greater than 5,000, the server will return up to 5,000 items.<br /><br /> Setting `maxresults` to a value less than or equal to zero results in error response code 400 (Bad Request).|  
|`include={snapshots,metadata,uncommittedblobs,copy}`|Optional. Specifies one or more datasets to include in the response:<br /><br /> -   `snapshots`: Specifies that snapshots should be included in the enumeration. Snapshots are listed from oldest to newest in the response.<br />-   `metadata`: Specifies that blob metadata be returned in the response.<br />-   `uncommittedblobs`: Specifies that blobs for which blocks have been uploaded, but which have not been committed using [Put Block List](../StorageServicesREST/Put-Block-List.md), be included in the response.<br />-   `copy`: Version 2012-02-12 and newer. Specifies that metadata related to any current or previous `Copy Blob` operation should be included in the response.<br /><br /> To specify more than one of these options on the URI, you must separate each option with a URL-encoded comma ("%82").|  
|`timeout`|Optional. The `timeout` parameter is expressed in seconds. For more information, see [Setting Timeouts for Blob Service Operations](../StorageServicesREST/Setting-Timeouts-for-Blob-Service-Operations.md).|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Required for all authenticated requests, optional for anonymous requests. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
### Request Body  
 None.  
  
### Sample Request  
 See [Enumerating Blob Resources](../StorageServicesREST/Enumerating-Blob-Resources.md) for a sample request.  
  
##  <a name="response"></a> Response  
 The response includes an HTTP status code, a set of response headers, and a response body in XML format.  
  
### Status Code  
 A successful operation returns status code 200 (OK).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`Content-Type`|Specifies the format in which the results are returned. Currently this value is `application/xml`.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Blob service used to execute the request. This header is returned for requests made using version 2009-09-19 and newer.<br /><br /> This header is also returned for anonymous requests without a version specified if the container was marked for public access using the 2009-09-19 version of the Blob service.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
### Response Body  
 The format of the XML response is as follows.  
  
 Note that the `Prefix`, `Marker`, `MaxResults`, and `Delimiter` elements are present only if they were specified on the request URI. The `NextMarker` element has a value only if the list results are not complete.  
  
 Snapshots, blob metadata, and uncommitted blobs are included in the response only if they are specified with the `include` parameter on the request URI.  
  
 In version 2009-09-19 and newer, the blob's properties are encapsulated within a `Properties` element.  
  
 Beginning with version 2009-09-19, `List Blobs` returns the following renamed elements in the response body:  
  
-   `Last-Modified` (previously `LastModified`)  
  
-   `Content-Length` (previously `Size`)  
  
-   `Content-Type` (previously `ContentType`)  
  
-   `Content-Encoding` (previously `ContentEncoding`)  
  
-   `Content-Language` (previously `ContentLanguage`)  
  
 The `Content-MD5` element appears for blobs created with version 2009-09-19 and newer. In version 2012-02-12 and newer, the Blob service calculates the `Content-MD5` value when you upload a blob using [Put Blob](../StorageServicesREST/Put-Blob.md), but does not calculate this when you create a blob using [Put Block List](../StorageServicesREST/Put-Block-List.md). You can explicitly set the `Content-MD5` value when you create the blob, or by calling [Put Block List](../StorageServicesREST/Put-Block-List.md) or [Set Blob Properties](../StorageServicesREST/Set-Blob-Properties.md) operations.  
  
 For versions from 2009-09-19 and newer but prior to version 2015-02-21, calling `List Blobs` on a container that includes append blobs will fail with status code 409 (FeatureVersionMismatch) if the result of listing contains an append blob.  
  
 `LeaseState` and `LeaseDuration` appear only in version 2012-02-12 and later.  
  
 `CopyId`, `CopyStatus`, `CopySource`, `CopyProgress`, `CopyCompletionTime`, and `CopyStatusDescription` only appear in version 2012-02-12 and later, when this operation includes the `include={copy}` parameter. These elements do not appear if this blob has never been the destination in a `Copy Blob` operation, or if this blob has been modified after a concluded `Copy Blob` operation using `Set Blob Properties`, `Put Blob`, or `Put Block List`. These elements also do not appear with a blob created by [Copy Blob](../StorageServicesREST/Copy-Blob.md) before version 2012-02-12.  
  
 In version 2013-08-15 and newer, the `EnumerationResults` element contains a `ServiceEndpoint` attribute specifying the blob endpoint, and a `ContainerName` field specifying the name of the container. In previous versions these two attributes were combined together in the `ContainerName` field. Also in version 2013-08-15 and newer, the `Url` element under `Blob` has been removed.  
  
 For version 2015-02-21 and above, `List Blobs` returns blobs of all types (block, page, and append blobs).  
  
 For version 2015-12-11 and above, `List Blobs` returns the `ServerEncrypted` element. This element is set to `true` if the blob and application metadata are completely encrypted, and `false` otherwise.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<EnumerationResults ServiceEndpoint="http://myaccount.blob.core.windows.net/"  ContainerName="mycontainer">  
  <Prefix>string-value</Prefix>  
  <Marker>string-value</Marker>  
  <MaxResults>int-value</MaxResults>  
  <Delimiter>string-value</Delimiter>  
  <Blobs>  
    <Blob>  
      <Name>blob-name</name>  
      <Snapshot>date-time-value</Snapshot>  
      <Properties>  
        <Last-Modified>date-time-value</Last-Modified>  
        <Etag>etag</Etag>  
        <Content-Length>size-in-bytes</Content-Length>  
        <Content-Type>blob-content-type</Content-Type>  
        <Content-Encoding />  
        <Content-Language />  
        <Content-MD5 />  
        <Cache-Control />  
        <x-ms-blob-sequence-number>sequence-number</x-ms-blob-sequence-number>  
        <BlobType>BlockBlob|PageBlob|AppendBlob</BlobType>  
        <LeaseStatus>locked|unlocked</LeaseStatus>  
        <LeaseState>available | leased | expired | breaking | broken</LeaseState>  
        <LeaseDuration>infinite | fixed</LeaseDuration>  
        <CopyId>id</CopyId>  
        <CopyStatus>pending | success | aborted | failed </CopyStatus>  
        <CopySource>source url</CopySource>  
        <CopyProgress>bytes copied/bytes total</CopyProgress>  
        <CopyCompletionTime>datetime</CopyCompletionTime>  
        <CopyStatusDescription>error string</CopyStatusDescription>  
        <ServerEncrypted>true</ServerEncrypted>  
      </Properties>  
      <Metadata>     
        <Name>value</Name>  
      </Metadata>  
    </Blob>  
    <BlobPrefix>  
      <Name>blob-prefix</Name>  
    </BlobPrefix>  
  </Blobs>  
  <NextMarker />  
</EnumerationResults>  
```  
  
### Sample Response  
 See [Enumerating Blob Resources](../StorageServicesREST/Enumerating-Blob-Resources.md) for a sample response.  
  
##  <a name="authorization"></a> Authorization  
 If the container's access control list (ACL) is set to allow anonymous access to the container, any client may call this operation. Otherwise, this operation can be called by the account owner and by anyone with a Shared Access Signature that has permission to list blobs in a container.  
  
## Remarks  
 **Blob Properties in the Response**  
  
 If you have requested that uncommitted blobs be included in the enumeration, note that some properties are not set until the blob is committed, so some properties may not be returned in the response.  
  
 The `x-ms-blob-sequence-number` element is only returned for page blobs.  
  
 For page blobs, the value returned in the `Content-Length` element corresponds to the value of the blob's `x-ms-blob-content-length` header.  
  
 The `Content-MD5` element appears in the response body only if it has been set on the blob using version 2009-09-19 or later. You can set the `Content-MD5` property when the blob is created or by calling [Set Blob Properties](../StorageServicesREST/Set-Blob-Properties.md). In version 2012-02-12 and newer, `Put Blob` sets a block blob’s MD5 value even when the `Put Blob` request doesn’t include an MD5 header.  
  
 **Metadata in the Response**  
  
 The `Metadata` element is present only if the `include=metadata` parameter was specified on the URI. Within the `Metadata` element, the value of each name-value pair is listed within an element corresponding to the pair's name.  
  
 Note that metadata requested with this parameter must be stored in accordance with the naming restrictions imposed by the 2009-09-19 version of the Blob service. Beginning with this version, all metadata names must adhere to the naming conventions for [C# identifiers](http://msdn.microsoft.com/library/aa664670\(VS.71\).aspx).  
  
 If a metadata name-value pair violates the naming restrictions enforced by the 2009-09-19 version, the response body indicates the problematic name within an `x-ms-invalid-name` element, as shown in the following XML fragment:  
  
```  
  
…  
<Metadata>  
  <MyMetadata1>first value</MyMetadata1>  
  <MyMetadata2>second value</MyMetadata2>  
  <x-ms-invalid-name>invalid-metadata-name</x-ms-invalid-name>  
</Metadata>  
…  
  
```  
  
 **Snapshots in the Response**  
  
 Snapshots are listed in the response only if the `include=snapshots` parameter was specified on the URI. Snapshots listed in the response do not include the `LeaseStatus` element, as snapshots cannot have active leases.  
  
 If you call `List Blobs` with a delimiter, you cannot also include snapshots in the enumeration. A request that includes both returns an InvalidQueryParameter error (HTTP status code 400 – Bad Request).  
  
 **Uncommitted Blobs in the Response**  
  
 Uncommitted blobs are listed in the response only if the `include=uncommittedblobs` parameter was specified on the URI. Uncommitted blobs listed in the response do not include any of the following elements:  
  
-   `Last-Modified`  
  
-   `Etag`  
  
-   `Content-Type`  
  
-   `Content-Encoding`  
  
-   `Content-Language`  
  
-   `Content-MD5`  
  
-   `Cache-Control`  
  
-   `Metadata`  
  
 **Returning Result Sets Using a Marker Value**  
  
 If you specify a value for the `maxresults` parameter and the number of blobs to return exceeds this value, or exceeds the default value for `maxresults`, the response body will contain a `NextMarker` element that indicates the next blob to return on a subsequent request. To return the next set of items, specify the value of `NextMarker` as the marker parameter on the URI for the subsequent request.  
  
 Note that the value of `NextMarker` should be treated as opaque.  
  
 **Using a Delimiter to Traverse the Blob Namespace**  
  
 The `delimiter` parameter enables the caller to traverse the blob namespace by using a user-configured delimiter. In this way, you can traverse a virtual hierarchy of blobs as though it were a file system. The delimiter may be a single character or a string. When the request includes this parameter, the operation returns a `BlobPrefix` element. The `BlobPrefix` element is returned in place of all blobs whose names begin with the same substring up to the appearance of the delimiter character. The value of the `BlobPrefix` element is *substring+delimiter*, where *substring* is the common substring that begins one or more blob names, and *delimiter* is the value of the *delimiter* parameter.  
  
 You can use the value of `BlobPrefix` to make a subsequent call to list the blobs that begin with this prefix, by specifying the value of `BlobPrefix` for the `prefix` parameter on the request URI.  
  
 Note that each `BlobPrefix` element returned counts toward the maximum result, just as each `Blob` element does.  
  
 Blobs are listed in alphabetical order in the response body, with upper-case letters listed first.  
  
 **Copy errors in CopyStatusDescription**  
  
 `CopyStatusDescription` contains more information about the `Copy Blob` failure.  
  
-   When a copy attempt fails and the Blob service is still retrying the operation, `CopyStatus` is set to `pending`, and the `CopyStatusDescription` text describes the failure that may have occurred during the last copy attempt.  
  
-   When `CopyStatus` is set to `failed`, the `CopyStatusDescription` text describes the error that caused the copy operation to fail.  
  
 The following table describes the three fields of every `CopyStatusDescription` value.  
  
|Component|Description|  
|---------------|-----------------|  
|HTTP status code|Standard 3-digit integer specifying the failure.|  
|Error code|Keyword describing error that is provided by Azure in the <ErrorCode\> element. If no <ErrorCode\> element appears, a keyword containing standard error text associated with the 3-digit HTTP status code in the HTTP specification is used. See [Common REST API Error Codes](../StorageServicesREST/Common-REST-API-Error-Codes.md).|  
|Information|Detailed description of failure, in quotes.|  
  
 The following table describes the `CopyStatus` and `CopyStatusDescription` values of common failure scenarios.  
  
> [!IMPORTANT]
>  Description text shown here can change without warning, even without a version change, so do not rely on matching this exact text.  
  
|Scenario|CopyStatus value|CopyStatusDescription value|  
|--------------|----------------------|---------------------------------|  
|Copy operation completed successfully.|success|empty|  
|User aborted copy operation before it completed.|aborted|empty|  
|A failure occurred when reading from the source blob during a copy operation, but the operation will be retried.|pending|502 BadGateway "Encountered a retryable error when reading the source. Will retry. Time of failure: <time\>"|  
|A failure occurred when writing to the destination blob of a copy operation, but the operation will be retried.|pending|500 InternalServerError "Encountered a retryable error. Will retry. Time of failure: <time\>"|  
|An unrecoverable failure occurred when reading from the source blob of a copy operation.|failed|404 ResourceNotFound "Copy failed when reading the source." **Note:**  When reporting this underlying error, Azure returns `ResourceNotFound` in the <ErrorCode\> element. If no <ErrorCode\> element appeared in the response, a standard string representation of the HTTP status such as `NotFound` would appear.|  
|The timeout period limiting all copy operations elapsed. (Currently the timeout period is 2 weeks.)|failed|500 OperationCancelled "The copy exceeded the maximum allowed time."|  
|The copy operation failed too often when reading from the source, and didn’t meet a minimum ratio of attempts to successes. (This timeout prevents retrying a very poor source over 2 weeks before failing).|failed|500 OperationCancelled "The copy failed when reading the source."|  
  
## See Also  
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Blob Service Error Codes](../StorageServicesREST/Blob-Service-Error-Codes.md)
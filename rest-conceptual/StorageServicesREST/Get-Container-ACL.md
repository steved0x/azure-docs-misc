---
title: "Get Container ACL"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: cc52e59f-2cb5-41b8-9ed8-3c9513dba389
caps.latest.revision: 63
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
# Get Container ACL
The `Get Container ACL` operation gets the permissions for the specified container. The permissions indicate whether container data may be accessed publicly.  
  
 Beginning with the 2009-09-19 version, the container permissions provide the following options for managing container access:  
  
-   **Full public read access:** Container and blob data can be read via anonymous request. Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.  
  
-   **Public read access for blobs only:** Blob data within this container can be read via anonymous request, but container data is not available. Clients cannot enumerate blobs within the container via anonymous request.  
  
-   **No public read access:** Container and blob data can be read by the account owner only.  
  
 `Get Container ACL` also returns details about any container-level access policies specified on the container that may be used with Shared Access Signatures. For more information, see [Establishing a Stored Access Policy](../StorageServicesREST/Establishing-a-Stored-Access-Policy.md).  
  
 All public access to the container is anonymous, as is access via a Shared Access Signature.  
  
## Request  
 The `Get Container ACL` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`GET/HEAD`|`https://myaccount.blob.core.windows.net/mycontainer?restype=container&comp=acl`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Blob service port as `127.0.0.1:10000`, followed by the emulated storage account name:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`GET/HEAD`|`http://127.0.0.1:10000/devstoreaccount1/mycontainer?restype=container&comp=acl`|HTTP/1.1|  
  
 For more information, see [Using the Azure Storage Emulator for Development and Testing](assetId:///f0e3acde-f019-4148-9544-34cf2ff27211).  
  
### URI Parameters  
 The following additional parameters may be specified on the request URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`timeout`|Optional. The `timeout` parameter is expressed in seconds. For more information, see [Setting Timeouts for Blob Service Operations](../StorageServicesREST/Setting-Timeouts-for-Blob-Service-Operations.md).|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-lease-id: <ID>`|Optional, version 2012-02-12 and newer. If specified, `Get Container ACL` only succeeds if the container’s lease is active and matches this ID. If there is no active lease or the ID does not match, `412 (Precondition Failed)` is returned.|  
|`x-ms-version`|Required for all authenticated requests. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
### Request Body  
 None.  
  
## Response  
 The response includes an HTTP status code, a set of response headers, and a response body.  
  
### Status Code  
 A successful operation returns status code `200 (OK)`.  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`x-ms-blob-public-access`|Indicates whether data in the container may be accessed publicly and the level of access. Possible values include:<br /><br /> -   `container`: Indicates full public read access for container and blob data. Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.<br />-   `blob:` Indicates public read access for blobs. Blob data within this container can be read via anonymous request, but container data is not available. Clients cannot enumerate blobs within the container via anonymous request.<br />-   `true:` Indicates that the container was marked for full public read access using a version prior to 2009-09-19.<br /><br /> If this header is not returned in the response, the container is private to the account owner.|  
|`ETag`|The entity tag for the container. If the request version is 2011-08-18 or newer, the ETag value will be in quotes.|  
|`Last-Modified`|Returns the date and time the container was last modified. The date format follows RFC 1123. For more information, see [Representation of Date-Time Values in Headers](../StorageServicesREST/Representation-of-Date-Time-Values-in-Headers.md).<br /><br /> Any operation that modifies the container or its properties or metadata updates the last modified time. Operations on blobs do not affect the last modified time of the container.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Blob service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
### Response Body  
 If a container-level access policy has been specified for the container, `Get Container ACL` returns the signed identifier and access policy in the response body.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<SignedIdentifiers>  
  <SignedIdentifier>  
    <Id>unique-value</Id>  
    <AccessPolicy>  
      <Start>start-time</Start>  
      <Expiry>expiry-time</Expiry>  
      <Permission>abbreviated-permission-list</Permission>  
    </AccessPolicy>  
  </SignedIdentifier>  
</SignedIdentifiers>  
```  
  
### Sample Response  
  
```  
Response Status:  
HTTP/1.1 200 OK  
  
Response Headers:  
Transfer-Encoding: chunked  
x-ms-blob-public-access: container  
Date: Sun, 25 Sep 2011 20:28:22 GMT  
ETag: "0x8CAFB82EFF70C46"  
Last-Modified: Sun, 25 Sep 2011 19:42:18 GMT  
x-ms-version: 2011-08-18  
Server: Windows-Azure-Blob/1.0 Microsoft-HTTPAPI/2.0  
  
<?xml version="1.0" encoding="utf-8"?>  
<SignedIdentifiers>  
  <SignedIdentifier>   
    <Id>MTIzNDU2Nzg5MDEyMzQ1Njc4OTAxMjM0NTY3ODkwMTI=</Id>  
    <AccessPolicy>  
      <Start>2009-09-28T08:49:37.0000000Z</Start>  
      <Expiry>2009-09-29T08:49:37.0000000Z</Expiry>  
      <Permission>rwd</Permission>  
    </AccessPolicy>  
  </SignedIdentifier>  
</SignedIdentifiers>  
  
```  
  
## Authorization  
 Only the account owner may call this operation.  
  
## Remarks  
 Only the account owner may read data in a particular storage account, unless the account owner has specified that blobs within the container are available for public read access, or made resources in the container available via a Shared Access Signature.  
  
## See Also  
 [Restrict Access to Containers and Blobs](assetId:///1d1c1a78-7a01-4477-b8e0-394d122e15a6)   
 [Use a Stored Access Policy](assetId:///c0d4fe58-e6f4-4a90-bad5-138f59967560)   
 [Set Container ACL](../StorageServicesREST/Set-Container-ACL.md)   
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Blob Service Error Codes](../StorageServicesREST/Blob-Service-Error-Codes.md)
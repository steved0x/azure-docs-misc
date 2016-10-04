---
title: "Set Container ACL"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 55958376-0879-4805-ace9-079d297ab3fa
caps.latest.revision: 73
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
# Set Container ACL
The `Set Container ACL` operation sets the permissions for the specified container. The permissions indicate whether blobs in a container may be accessed publicly.  
  
 Beginning with the 2009-09-19 version, the container permissions provide the following options for managing container access:  
  
-   **Full public read access:** Container and blob data can be read via anonymous request. Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.  
  
-   **Public read access for blobs only:** Blob data within this container can be read via anonymous request, but container data is not available. Clients cannot enumerate blobs within the container via anonymous request.  
  
-   **No public read access:** Container and blob data can be read by the account owner only.  
  
 `Set Container ACL` also sets a stored access policy for use with shared access signatures. For more information, see [Use a Stored Access Policy](assetId:///c0d4fe58-e6f4-4a90-bad5-138f59967560).  
  
 All public access to the container is anonymous, as is access via a shared access signature.  
  
## Request  
 The `Set Container ACL` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`PUT`|`https://myaccount.blob.core.windows.net/mycontainer?restype=container&comp=acl`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Blob service port as `127.0.0.1:10000`, followed by the emulated storage account name:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`PUT`|`http://127.0.0.1:10000/devstoreaccount1/mycontainer?restype=container&comp=acl`|HTTP/1.1|  
  
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
|`x-ms-version`|Optional. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-blob-public-access`|Optional. Specifies whether data in the container may be accessed publicly and the level of access. Possible values include:<br /><br /> -   `container`: Specifies full public read access for container and blob data. Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.<br />-   `blob:` Specifies public read access for blobs. Blob data within this container can be read via anonymous request, but container data is not available. Clients cannot enumerate blobs within the container via anonymous request.<br /><br /> If this header is not included in the request, container data is private to the account owner.<br /><br /> Note that setting public access for a container in an Azure Premium Storage account is not permitted.|  
|`x-ms-lease-id: <ID>`|Optional, version 2012-02-12 and newer. If specified, `Set Container ACL` only succeeds if the container's lease is active and matches this ID. If there is no active lease or the ID does not match, 412 (Precondition Failed) is returned.|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
 This operation also supports the use of conditional headers to execute the operation only if a specified condition is met. For more information, see [Specifying Conditional Headers for Blob Service Operations](../StorageServicesREST/Specifying-Conditional-Headers-for-Blob-Service-Operations.md).  
  
### Request Body  
 To specify a stored access policy, provide a unique identifier and access policy in the request body for the `Set Container ACL` operation.  
  
 The `SignedIdentifier` element includes the unique identifier, as specified in the `Id` element, and the details of the access policy, as specified in the `AccessPolicy` element. The maximum length of the unique identifier is 64 characters.  
  
 The `Start` and `Expiry` fields must be expressed as UTC times and must adhere to a valid ISO 8061 format. Supported ISO 8061 formats include the following:  
  
-   `YYYY-MM-DD`  
  
-   `YYYY-MM-DDThh:mmTZD`  
  
-   `YYYY-MM-DDThh:mm:ssTZD`  
  
-   `YYYY-MM-DDThh:mm:ss.fffffffTZD`  
  
 For the date portion of these formats, `YYYY` is a four-digit year representation, `MM` is a two-digit month representation, and `DD` is a two-digit day representation. For the time portion, `hh` is the hour representation in 24-hour notation, `mm` is the two-digit minute representation, `ss` is the two-digit second representation, and `fffffff` is the seven-digit millisecond representation. A time designator `T` separates the date and time portions of the string, while a time zone designator `TZD` specifies a time zone.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<SignedIdentifiers>  
  <SignedIdentifier>   
    <Id>unique-64-character-value</Id>  
    <AccessPolicy>  
      <Start>start-time</Start>  
      <Expiry>expiry-time</Expiry>  
      <Permission>abbreviated-permission-list</Permission>  
    </AccessPolicy>  
  </SignedIdentifier>  
</SignedIdentifiers>  
  
```  
  
### Sample Request  
  
```  
Request Syntax:  
PUT https://myaccount.blob.core.windows.net/mycontainer?restype=container&comp=acl HTTP/1.1  
  
Request Headers:  
x-ms-version: 2011-08-18  
x-ms-date: Sun, 25 Sep 2011 00:42:49 GMT  
x-ms-blob-public-access: container  
Authorization: SharedKey myaccount:V47F2tYLS29MmHPhiR8FyiCny9zO5De3kVSF0RYQHmo=  
  
Request Body:  
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
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 200 (OK).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`ETag`|The ETag for the container. If the request version is 2011-08-18 or newer, the ETag value will be in quotes.|  
|`Last-Modified`|Returns the date and time the container was last modified. The date format follows RFC 1123. For more information, see [Representation of Date-Time Values in Headers](../StorageServicesREST/Representation-of-Date-Time-Values-in-Headers.md).<br /><br /> Any operation that modifies the container or its properties or metadata updates the last modified time, including setting the container's permissions. Operations on blobs do not affect the last modified time of the container.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md)|  
|`x-ms-version`|Indicates the version of the Blob service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
### Sample Response  
  
```  
Response Status:  
HTTP/1.1 200 OK  
  
Response Headers:  
Transfer-Encoding: chunked  
Date: Sun, 25 Sep 2011 22:42:55 GMT  
ETag: "0x8CB171613397EAB"  
Last-Modified: Sun, 25 Sep 2011 22:42:55 GMT  
x-ms-version: 2011-08-18  
Server: Windows-Azure-Blob/1.0 Microsoft-HTTPAPI/2.0  
```  
  
## Authorization  
 Only the account owner may call this operation.  
  
## Remarks  
 Only the account owner may access resources in a particular container, unless the owner has specified that container resources are available for public access by setting the permissions on the container, or has issued a shared access signature for a resource within the container.  
  
 When you set permissions for a container, the existing permissions are replaced. To update the container's permissions, call [Get Container ACL](../StorageServicesREST/Get-Container-ACL.md) to fetch all access policies associated with the container, modify the access policy that you wish to change, and then call `Set Container ACL` with the complete set of data to perform the update.  
  
 **Enabling Anonymous Public Access on Container Data**  
  
 To enable anonymous public read access on container data, call `Set Container ACL` with the `x-ms-blob-public-access` header set to `container` or `blob`. To disable anonymous access, call `Set Container ACL` without specifying the `x-ms-blob-public-access` header.  
  
 If you set `x-ms-blob-public-access` to `blob`, clients can call the following operations anonymously:  
  
-   [Get Blob](../StorageServicesREST/Get-Blob.md)  
  
-   [Get Blob Properties](../StorageServicesREST/Get-Blob-Properties.md)  
  
-   [Get Blob Metadata](../StorageServicesREST/Get-Blob-Metadata.md)  
  
-   [Get Block List](../StorageServicesREST/Get-Block-List.md) (for the committed block list only)  
  
-   [Get Page Ranges](../StorageServicesREST/Get-Page-Ranges.md)  
  
 If you set `x-ms-blob-public-access` to `container`, clients can call the following operations anonymously:  
  
-   The blob access operations listed above.  
  
-   [Get Container Properties](../StorageServicesREST/Get-Container-Properties.md)  
  
-   [Get Container Metadata](../StorageServicesREST/Get-Container-Metadata.md)  
  
-   [List Blobs](../StorageServicesREST/List-Blobs.md)  
  
 **Establishing Container-Level Access Policies**  
  
 A stored access policy can specify the start time, expiry time, and permissions for the shared access signatures with which it's associated. Depending on how you want to control access to your container or blob resource, you can specify all of these parameters within the stored access policy, and omit them from the URL for the shared access signature. Doing so permits you to modify the associated signature's behavior at any time, as well as to revoke it. Or you can specify one or more of the access policy parameters within the stored access policy, and the others on the URL. Finally, you can specify all of the parameters on the URL. In this case, you can use the stored access policy to revoke the signature, but not to modify its behavior. See specifying a [Use a Stored Access Policy](assetId:///c0d4fe58-e6f4-4a90-bad5-138f59967560) for more information about establishing access policies.  
  
 Together the shared access signature and the stored access policy must include all fields required to authenticate the signature. If any required fields are missing, the request will fail. Likewise, if a field is specified both in the shared access signature URL and in the stored access policy, the request will fail with status code 400 (Bad Request).  
  
 At most five separate access policies can be set for a given container at any time. If more than five access policies are passed in the request body, then the service returns status code 400 (Bad Request).  
  
 A shared access signature can be issued on a container or a blob regardless of whether container data is available for anonymous read access. A shared access signature provides a greater measure of control over how, when, and to whom a resource is made accessible.  
  
> [!NOTE]
>  When you establish a stored access policy on a container, it may take up to 30 seconds to take effect. During this interval, a shared access signature that is associated with the stored access policy will fail with status code 403 (Forbidden), until the access policy becomes active.  
  
## See Also  
 [Restrict Access to Containers and Blobs](assetId:///1d1c1a78-7a01-4477-b8e0-394d122e15a6)   
 [Delegating Access with a Shared Access Signature](../StorageServicesREST/Delegating-Access-with-a-Shared-Access-Signature.md)   
 [Create and Use a Shared Access Signature](assetId:///b41f98e9-14ab-499a-9fd2-fb9202c9ccd2)   
 [Use a Stored Access Policy](assetId:///c0d4fe58-e6f4-4a90-bad5-138f59967560)   
 [Get Container ACL](../StorageServicesREST/Get-Container-ACL.md)   
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Blob Service Error Codes](../StorageServicesREST/Blob-Service-Error-Codes.md)
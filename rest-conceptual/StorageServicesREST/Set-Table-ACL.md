---
title: "Set Table ACL"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: a68b978f-5cbe-4275-b42a-68b7f88ee968
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
# Set Table ACL
The `Set Table ACL` operation sets the stored access policies for the table that may be used with Shared Access Signatures. For more information, see [Establishing a Stored Access Policy](../StorageServicesREST/Establishing-a-Stored-Access-Policy.md).  
  
> [!NOTE]
>  The `Set Table ACL` operation is available in version 2012-02-12 and newer.  
  
> [!NOTE]
>  An *access control list* (ACL) is a list of *access control entries* (ACE). Each ACE in an ACL identifies a *trustee* and specifies the *access rights* allowed, denied, or audited for that trustee. For more information, see [Access Control Lists](http://go.microsoft.com/fwlink/?LinkId=294100).  
  
## Request  
 The `Set Table ACL` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`PUT`|`https://myaccount.table.core.windows.net/mytable?comp=acl`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Table service port as `127.0.0.1:10002`, followed by the emulated storage account name:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`PUT`|`http://127.0.0.1:10002/devstoreaccount1/mytable?comp=acl`|HTTP/1.1|  
  
 For more information, see [Differences Between the Storage Emulator and Azure Storage Services](assetId:///c60f2090-c0f4-4817-8559-e98786461dbe).  
  
### URI Parameters  
 The following additional parameters may be specified on the request URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
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
 To specify a stored access policy, provide a unique identifier and access policy in the request body for the `Set Table ACL` operation.  
  
 The `SignedIdentifier` element includes the unique identifier, as specified in the `Id` element, and the details of the access policy, as specified in the `AccessPolicy` element. The maximum length of the unique identifier is 64 characters.  
  
 The `Start` and `Expiry` fields must be expressed as UTC times and must adhere to a valid ISO 8061 format. Supported ISO 8061 formats include the following:  
  
-   `YYYY-MM-DD`  
  
-   `YYYY-MM-DDThh:mmTZD`  
  
-   `YYYY-MM-DDThh:mm:ssTZD`  
  
-   `YYYY-MM-DDThh:mm:ss.ffffffTZD`  
  
 For the date portion of these formats, `YYYY` is a four-digit year representation, `MM` is a two-digit month representation, and `DD` is a two-digit day representation. For the time portion, `hh` is the hour representation in 24-hour notation, `mm` is the two-digit minute representation, `ss` is the two-digit second representation, and `ffffff` is the six-digit millisecond representation. A time designator `T` separates the date and time portions of the string, while a time zone designator `TZD` specifies a time zone.  
  
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
PUT https://myaccount.table.core.windows.net/mytable?comp=acl HTTP/1.1  
  
Request Headers:  
x-ms-version: 2013-08-15  
x-ms-date: Mon, 25 Nov 2013 00:42:49 GMT  
Authorization: SharedKey myaccount:V47F2tYLS29MmHPhiR8FyiCny9zO5De3kVSF0RYQHmo=  
  
Request Body:  
<?xml version="1.0" encoding="utf-8"?>  
<SignedIdentifiers>  
  <SignedIdentifier>   
    <Id>MTIzNDU2Nzg5MDEyMzQ1Njc4OTAxMjM0NTY3ODkwMTI=</Id>  
    <AccessPolicy>  
      <Start>2013-11-26T08:49:37.0000000Z</Start>  
      <Expiry>2013-11-27T08:49:37.0000000Z</Expiry>  
      <Permission>raud</Permission>  
    </AccessPolicy>  
  </SignedIdentifier>  
</SignedIdentifiers>  
  
```  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 204 (No Content).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md)|  
|`x-ms-version`|Indicates the version of the Table service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
### Sample Response  
  
```  
Response Status:  
HTTP/1.1 204 No Content  
  
Response Headers:  
Transfer-Encoding: chunked  
Date: Mon, 25 Nov 2013 22:42:55 GMT  
x-ms-version: 2013-08-15  
Server: Windows-Azure-Table/1.0 Microsoft-HTTPAPI/2.0  
  
```  
  
## Authorization  
 Only the account owner may call this operation.  
  
## Remarks  
 Only the account owner may access resources in a particular table, unless the owner has issued a Shared Access Signature for a resource within the table.  
  
 When you set permissions for a table, the existing permissions are replaced. To update the table’s permissions, call [Get Table ACL](../StorageServicesREST/Get-Table-ACL.md) to fetch all access policies associated with the table, modify the access policy that you wish to change, and then call `Set Table ACL` with the complete set of data to perform the update.  
  
 **Establishing Stored Access Policies**  
  
 A stored access policy can specify the start time, expiry time, and permissions for the Shared Access Signatures with which it's associated. Depending on how you want to control access to your table resource, you can specify all of these parameters within the stored access policy, and omit them from the URL for the Shared Access Signature. Doing so permits you to modify the associated signature's behavior at any time, as well as to revoke it. Or you can specify one or more of the access policy parameters within the stored access policy, and the others on the URL. Finally, you can specify all of the parameters on the URL. In this case, you can use the stored access policy to revoke the signature, but not to modify its behavior. See [Use a Stored Access Policy](assetId:///c0d4fe58-e6f4-4a90-bad5-138f59967560) for more information about establishing access policies.  
  
 Together the Shared Access Signature and the stored access policy must include all fields required to authenticate the signature. If any required fields are missing, the request will fail. Likewise, if a field is specified both in the Shared Access Signature URL and in the stored access policy, the request will fail with status code 400 (Bad Request). See [Constructing a Service SAS](../StorageServicesREST/Constructing-a-Service-SAS.md) for more information about the fields that comprise a Shared Access Signature.  
  
 Note that at most five separate access policies can be set for a given table at any time. If more than five access policies are passed in the request body, then the service returns status code 400 (Bad Request).  
  
> [!NOTE]
>  When you establish a stored access policy on a table, it may take up to 30 seconds to take effect. During this interval, a shared access signature that is associated with the stored access policy will fail with status code `403 (Forbidden)`, until the access policy becomes active.  
  
## See Also  
 [Use a Stored Access Policy](assetId:///c0d4fe58-e6f4-4a90-bad5-138f59967560)   
 [Create and Use a Shared Access Signature](assetId:///b41f98e9-14ab-499a-9fd2-fb9202c9ccd2)   
 [Delegating Access with a Shared Access Signature](../StorageServicesREST/Delegating-Access-with-a-Shared-Access-Signature.md)   
 [Get Table ACL](../StorageServicesREST/Get-Table-ACL.md)   
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)
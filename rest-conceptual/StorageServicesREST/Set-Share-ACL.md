---
title: "Set Share ACL"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 032f3a38-db93-4673-ac7e-0434311e1240
caps.latest.revision: 8
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
# Set Share ACL
**Set Share ACL** sets a stored access policy for use with shared access signatures. For more information, see [Use a Stored Access Policy](https://msdn.microsoft.com/en-us/library/azure/ee393341.aspx).  
  
## Request  
 The **Set Share ACL** request may be constructed as follows. HTTPS is recommended. Replace `myaccount` with the name of your storage account:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|PUT|`https://myaccount.file.core.windows.net/myshare?restype=share&comp=acl`|HTTP/1.1|  
  
### URI Parameters  
 The following additional parameters may be specified on the request URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`timeout`|Optional. The `timeout` parameter is expressed in seconds. For more information, see [Setting Timeouts for Blob Service Operations](https://msdn.microsoft.com/en-us/library/azure/dd179431.aspx).|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](https://msdn.microsoft.com/en-us/library/azure/dd179428.aspx).|  
|`Date or x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](https://msdn.microsoft.com/en-us/library/azure/dd179428.aspx).|  
|`x-ms-version`|Required for all authenticated requests. Specifies the version of the operation to use for this request. This operation is available only in versions 2015-02-21 and later.<br /><br /> For more information, see [Versioning for the Azure Storage Services](https://msdn.microsoft.com/en-us/library/azure/dd894041.aspx).|  
  
### Request Body  
 To specify a stored access policy, provide a unique identifier and access policy in the request body for the **Set Share ACL** operation.  
  
 The **SignedIdentifier** element includes the unique identifier, as specified in the **Id** element, and the details of the access policy, as specified in the **AccessPolicy** element. The maximum length of the unique identifier is 64 characters.  
  
 The **Start** and **Expiry** fields must be expressed as UTC times and must adhere to a valid ISO 8061 format. Supported ISO 8061 formats include the following:  
  
-   `YYYY-MM-DD`  
  
-   `YYYY-MM-DDThh:mmTZD`  
  
-   `YYYY-MM-DDThh:mm:ssTZD`  
  
-   `YYYY-MM-DDThh:mm:ss.fffffffTZD`  
  
 For the date portion of these formats, `YYYY` is a four-digit year representation, `MM` is a two-digit month representation, and `DD` is a two-digit day representation. For the time portion, `hh` is the hour representation in 24-hour notation, `mm` is the two-digit minute representation, `ss` is the two-digit second representation, and `fffffff` is the seven-digit millisecond representation. A time designator `T` separates the date and time portions of the string, while a time zone designator `TZD` specifies a time zone.  
  
 XML  
  
```  
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
PUT https://myaccount.file.core.windows.net/myshare?restype=share&comp=acl HTTP/1.1  
  
Request Headers:  
x-ms-version: 2015-02-21  
x-ms-date: <date>  
Authorization: SharedKey myaccount:V47F2tYLS29MmHPhiR8FyiCny9zO5De3kVSF0RYQHmo=  
  
Request Body:  
<?xml version="1.0" encoding="utf-8"?>  
<SignedIdentifiers>  
  <SignedIdentifier>   
    <Id>MTIzNDU2Nzg5MDEyMzQ1Njc4OTAxMjM0NTY3ODkwMTI=</Id>  
    <AccessPolicy>  
      <Start>2015-07-01T08:49:37.0000000Z</Start>  
      <Expiry>2015-07-02T08:49:37.0000000Z</Expiry>  
      <Permission>rwd</Permission>  
    </AccessPolicy>  
  </SignedIdentifier>  
</SignedIdentifiers>  
```  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 200 (OK).  
  
 For information about status codes, see [Status and Error Codes](https://msdn.microsoft.com/en-us/library/azure/dd179382.aspx).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response Header|Description|  
|---------------------|-----------------|  
|`ETag`|Returns the date and time the container was last modified. The date format follows RFC 1123. For more information, see [Representation of Date/Time Values in Headers](https://msdn.microsoft.com/en-us/library/azure/dd135714.aspx).|  
|`Last-Modified`|Any operation that modifies the share or its properties or metadata updates the last modified time, including setting the file’s permissions. Operations on files do not affect the last modified time of the share.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](https://msdn.microsoft.com/en-us/library/azure/dd573365.aspx).|  
|`x-ms-version`|Indicates the version of the File service used to execute the request.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
### Sample Response  
  
```  
Response Status:  
HTTP/1.1 200 OK  
  
Response Headers:  
Transfer-Encoding: chunked  
Date: <date>  
ETag: "0x8CB171613397EAB"  
Last-Modified: <date>  
x-ms-version: 2015-02-21  
Server: Windows-Azure-File/1.0 Microsoft-HTTPAPI/2.0  
```  
  
## Authorization  
 Only the account owner may call this operation.  
  
## Remarks  
 Only the account owner may access resources in a particular share, unless the owner has specified that share resources are available for public access by setting the permissions on the share, or has issued a shared access signature for a resource within the share.  
  
 When you set permissions for a container, the existing permissions are replaced. To update the container's permissions, call [Get Share ACL](../StorageServicesREST/Get-Share-ACL.md) to fetch all access policies associated with the container, modify the access policy that you wish to change, and then call **Set Share ACL** with the complete set of data to perform the update.  
  
 **Establishing Share-Level Access Policies**  
  
 A stored access policy can specify the start time, expiry time, and permissions for the shared access signatures with which it is associated. Depending on how you want to control access to your share or file resource, you can specify all of these parameters within the stored access policy, and omit them from the URL for the shared access signature. Doing so permits you to modify the associated signature's behavior at any time, as well as to revoke it. Or you can specify one or more of the access policy parameters within the stored access policy, and the others on the URL. Finally, you can specify all of the parameters on the URL. In this case, you can use the stored access policy to revoke the signature, but not to modify its behavior. See specifying a [Use a Stored Access Policy](https://msdn.microsoft.com/en-us/library/azure/ee393341.aspx) for more information about establishing access policies.  
  
 Together the shared access signature and the stored access policy must include all fields required to authenticate the signature. If any required fields are missing, the request will fail. Likewise, if a field is specified both in the shared access signature URL and in the stored access policy, the request will fail with status code 400 (Bad Request). See [Creating a Shared Access Signature](https://msdn.microsoft.com/en-us/library/azure/hh508996.aspx) for more information about the fields that comprise a shared access signature.  
  
 At most five separate access policies can be set for a given share at any time. If more than five access policies are passed in the request body, then the service returns status code 400 (Bad Request).  
  
 A shared access signature can be issued on a share or a file regardless of whether container data is available for anonymous read access. A shared access signature provides a greater measure of control over how, when, and to whom a resource is made accessible.  
  
> [!NOTE]
>  When you establish a stored access policy on a container, it may take up to 30 seconds to take effect. During this interval, a shared access signature that is associated with the stored access policy will fail with status code 403 (Forbidden), until the access policy becomes active.  
  
## See Also  
 [Operations on Shares (File Service)](../StorageServicesREST/Operations-on-Shares--File-Service-.md)
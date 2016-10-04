---
title: "Get Table ACL"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 4131c1c3-8605-4bcb-9e85-e1a8ac7f17c6
caps.latest.revision: 15
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
# Get Table ACL
The `Get Table ACL` operation returns details about any stored access policies specified on the table that may be used with Shared Access Signatures. For more information, see [Establishing a Stored Access Policy](../StorageServicesREST/Establishing-a-Stored-Access-Policy.md).  
  
> [!NOTE]
>  The `Get Table ACL` operation is available in version 2012-02-12 and later.  
  
> [!NOTE]
>  An *access control list* (ACL) is a list of *access control entries* (ACE). Each ACE in an ACL identifies a *trustee* and specifies the *access rights* allowed, denied, or audited for that trustee. For more information, see [Access Control Lists](http://go.microsoft.com/fwlink/?LinkId=294100).  
  
## Request  
 The `Get Table ACL` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`GET/HEAD`|`https://myaccount.table.core.windows.net/mytable?comp=acl`|HTTP/1.1|  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Table service port as `127.0.0.1:10002`, followed by the emulated storage account name:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`GET/HEAD`|`http://127.0.0.1:10002/devstoreaccount1/mytable?comp=acl`|HTTP/1.1|  
  
 For more information, see [Differences Between the Storage Emulator and Azure Storage Services](assetId:///c60f2090-c0f4-4817-8559-e98786461dbe).  
  
### URI Parameters  
 The following additional parameters may be specified on the request URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`timeout`|Optional. The `timeout` parameter is expressed in seconds. For more information, see [Setting Timeouts for Table Service Operations](../StorageServicesREST/Setting-Timeouts-for-Table-Service-Operations.md).|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
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
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Table service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
### Response Body  
 If a stored access policy has been specified for the table, `Get Table ACL` returns the signed identifier and access policy in the response body.  
  
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
Date: Mon, 25 Nov 2013 20:28:22 GMT  
x-ms-version: 2013-08-15  
Server: Windows-Azure-Table/1.0 Microsoft-HTTPAPI/2.0  
  
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
  
## Authorization  
 Only the account owner may call this operation.  
  
## Remarks  
 Only the account owner may read data in a particular storage account unless the account owner has made resources in the table available via a Shared Access Signature.  
  
## See Also  
 [Delegating Access with a Shared Access Signature](../StorageServicesREST/Delegating-Access-with-a-Shared-Access-Signature.md)   
 [Establishing a Stored Access Policy](../StorageServicesREST/Establishing-a-Stored-Access-Policy.md)   
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Set Table ACL](../StorageServicesREST/Set-Table-ACL.md)
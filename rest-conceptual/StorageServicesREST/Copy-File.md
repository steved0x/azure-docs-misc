---
title: "Copy File"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 9108f963-eba1-4148-a00e-2d051bca4487
caps.latest.revision: 6
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
# Copy File
The `Copy File` operation copies a blob or file to a destination file within the storage account.  
  
 Available in version 2015-02-21 and newer.  
  
## Request  
 The `Copy File` request may be constructed as follows. HTTPS is recommended.  
  
 Beginning with version 2013-08-15, you may specify a shared access signature for the destination file if it is in the same account as the source file. Beginning with version 2015-04-05, you may also specify a shared access signature for the destination file if it is in a different storage account.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|PUT|`https://myaccount.file.core.windows.net/myshare/mydirectorypath/myfile`|HTTP/1.1|  
  
 Replace the path components shown in the request URI with your own, as follows:  
  
|Path Component|Description|  
|--------------------|-----------------|  
|`Myaccount`|The name of your storage account.|  
|`Myshare`|The name of your file share.|  
|`Mydirectorypath`|Optional. The path to the parent directory.|  
|`Myfile`|The name of the file.|  
  
 For details on path naming restrictions, see [Naming and Referencing Shares, Directories, Files, and Metadata](../StorageServicesREST/Naming-and-Referencing-Shares--Directories--Files--and-Metadata.md).  
  
### URI Parameters  
 The following additional parameters may be specified on the request URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`timeout`|Optional. The timeout parameter is expressed in seconds. For more information, see [Setting Timeouts for File Service Operations](#_Setting_Timeouts_for).|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](http://msdn.microsoft.com/en-us/library/azure/dd179428.aspx).|  
|`Date or x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](http://msdn.microsoft.com/en-us/library/azure/dd179428.aspx).|  
|`x-ms-version`|Required for all authenticated requests. Specifies the version of the operation to use for this request. This operation is available only in versions 2015-02-21 and later.<br /><br /> For more information, see [Versioning for the Azure Storage Services](https://msdn.microsoft.com/en-us/library/azure/dd894041.aspx).|  
|`x-ms-meta-name:value`|Optional. Name-value pairs associated with the file as metadata. If no name-value pairs are specified, the operation will copy the metadata from the source blob or file to the destination file. If one or more name-value pairs are specified, the destination file is created with the specified metadata, and the metadata is not copied from the source blob or file. Metadata names must adhere to the naming rules for [C# identifiers](http://msdn.microsoft.com/en-us/library/aa664670\(VS.71\).aspx).<br /><br /> Note that file metadata specified via the File service is not accessible from an SMB client.|  
|`x-ms-copy-source:name`|Required. Specifies the URL of the source file or blob, up to 2 KB in length.<br /><br /> To copy a file to another file within the same storage account, you may use Shared Key to authenticate the source file. If you are copying a file from another storage account, or if you are copying a blob from the same storage account or another storage account, then you must authenticate the source file or blob using a shared access signature. If the source is a public blob, no authentication is required to perform the copy operation.<br /><br /> Here are some examples of source object URLs:<br /><br /> -   `https://myaccount.file.core.windows.net/myshare/mydirectorypath/myfile`<br />-   `https://myaccount.blob.core.windows.net/mycontainer/myblob?sastoken`|  
  
### Request Body  
 None.  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 202 (Accepted).  
  
 For information about status codes, see [Status and Error Codes](http://msdn.microsoft.com/en-us/library/azure/dd179382.aspx).  
  
### Response Headers  
 The response for this operation includes the following headers. The response also includes additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`ETag`|If the copy is completed, contains the ETag of the destination file. If the copy is not complete, contains the ETag of the empty file created at the start of the copy.|  
|`Last-Modified`|Returns the date/time that the copy operation to the destination file completed.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](http://msdn.microsoft.com/en-us/library/azure/dd573365.aspx).|  
|`x-ms-version`|Indicates the version of the File service used to execute the request.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
|`x-ms-copy-id: <id>`|String identifier for this copy operation. Use with Get File or Get File Properties to check the status of this copy operation, or pass to Abort Copy File to abort a pending copy.|  
|`x-ms-copy-status: <success &#124; pending>`|State of the copy operation with these values:<br /><br /> -   **success**: the copy completed successfully.<br />-   **pending**: the copy is still in progress.|  
  
### Response Body  
 None  
  
### Sample Response  
  
```  
Response Status:  
HTTP/1.1 202 Accepted  
  
Response Headers:   
Last-Modified: <date>   
ETag: "0x8CEB669D794AFE2"  
Server: Windows-Azure-File/1.0 Microsoft-HTTPAPI/2.0  
x-ms-request-id: cc6b209a-b593-4be1-a38a-dde7c106f402  
x-ms-version: 2015-02-21  
x-ms-copy-id: 1f812371-a41d-49e6-b123-f4b542e851c5  
x-ms-copy-status: pending  
Date: <date>  
```  
  
## Authorization  
 This operation can be called by the account owner, or by a client possessing a shared access signature that has permission to write to the destination file or its share. Note that the shared access signature specified on the request applies only to the destination file.  
  
 Access to the source file or blob is authorized separately, as described in the details for the request header `x-ms-copy-source`.  
  
 The following table describes how the destination and source objects for a [Copy File](assetId:///Copy File?qualifyHint=False&autoUpgrade=True) operation may be authenticated.  
  
||Authentication with Shared Key/Shared Key Lite|Authentication with Shared Access Signature|Public Object Not Requiring Authentication|  
|-|-----------------------------------------------------|-------------------------------------------------|------------------------------------------------|  
|Destination file|Yes|Yes|N/A|  
|Source file in same account|Yes|Yes|N/A|  
|Source file in another account|No|Yes|N/A|  
|Source blob in the same account or another account|No|Yes|Yes|  
  
## Remarks  
 The **Copy File** operation can complete asynchronously. The copy ID returned by the `x-ms-copy-id` response header can be used to check the status of the copy operation or to abort it. The File service copies files on a best-effort basis.  
  
 When copying from a blob to a file, the source be a block blob or a page blob, or a snapshot of either. When copying from a file to a file, the source file can reside on a regular share or a share snapshot.  
  
 If the destination file exists, it will be overwritten. The destination file cannot be modified while the copy operation is in progress.  
  
 The **Copy File** operation always copies the entire source blob or file; copying a range of bytes or set of blocks is not supported.  
  
 When the source of a copy operation provides ETags, if there are any changes to the source while the copy is in progress, the copy will fail. An attempt to change the destination file while a copy is in progress will fail with 409 (Conflict).  
  
 The ETag for the destination file changes when the **Copy File** operation is initiated, and continues to change frequently during the copy operation.  
  
## Copying Properties and Metadata  
 When a blob or file is copied, the following system properties are copied to the destination file with the same values:  
  
-   Content-Type  
  
-   Content-Encoding  
  
-   Content-Language  
  
-   Content-Length  
  
-   Cache-Control  
  
-   Content-MD5  
  
-   Content-Disposition  
  
 The destination file is always the same size as the source blob or file, so the value of the Content-Length header for the destination file matches that for the source blob or file.  
  
## Copying a Leased Blob to a File  
 The **Copy File** operation only reads from the source blob, so the lease state of the source blob does not matter. However, the **Copy File** operation saves the ETag of the source blob when the copy is initiated. If the ETag value changes before the copy completes, the copy fails. You can prevent changes to the source blob by leasing it during the copy operation.  
  
## Working with a Pending Copy  
 The **Copy File** operation may complete the copy asynchronously. Use the following table to determine the next step based on the status code returned by **Copy File**:  
  
|Status Code|Meaning|  
|-----------------|-------------|  
|202 (Accepted), x-ms-copy-status: success|Copy completed successfully.|  
|202 (Accepted), x-ms-copy-status: pending|Copy has not completed. Poll the destination blob using Get File Properties to examine the x-ms-copy-status until copy completes or fails.|  
|4xx, 500, or 503|Copy failed.|  
  
 During and after a **Copy File** operation, the properties of the destination file contain the copy ID of the **Copy File** operation and URL of the source blob or file. When the copy completes, the File service writes the time and outcome value (**success**, **failed**, or **aborted**) to the destination file properties. If the operation **failed**, the `x-ms-copy-status-description` header contains an error detail string.  
  
 A pending **Copy File** operation has a 2 week timeout. A copy attempt that has not completed after 2 weeks times out and leaves an empty file with the `x-ms-copy-status` field set to **failed** and the `x-ms-status-description` set to 500 (OperationCancelled). Intermittent, non-fatal errors that can occur during a copy might impede progress of the copy but not cause it to fail. In these cases, `x-ms-copy-status-description` describes the intermittent errors.  
  
 Any attempt to modify the destination file during the copy will fail with **409 (Conflict) Copy File in Progress**.  
  
 If you call **Abort Copy File** operation, you will see a `x-ms-copy-status:aborted` header and the destination file will have intact metadata and a file length of zero bytes. You can repeat the original call to **Copy File** to try the copy again.  
  
## Billing  
 The destination account of a **Copy File** operation is charged for one transaction to initiate the copy, and also incurs one transaction for each request to abort or request the status of the copy operation.  
  
 When the source file or blob is in another account, the source account incurs transaction costs. In addition, if the source and destination accounts reside in different regions (e.g. US North and US South), bandwidth used to transfer the request is charged to the source account as egress. Egress between accounts within the same region is free.  
  
## See Also  
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [File Service Error Codes](../StorageServicesREST/File-Service-Error-Codes.md)   
 [Abort Copy File](../StorageServicesREST/Abort-Copy-File.md)
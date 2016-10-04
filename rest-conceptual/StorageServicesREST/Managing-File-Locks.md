---
title: "Managing File Locks"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 06db1069-ee35-4410-9b56-31c40a2cd276
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
# Managing File Locks
The Microsoft Azure File service can be accessed through two different protocol endpoints:  
  
-   Server Message Block (SMB) Protocol  
  
-   Representational State Transfer (REST) over Hypertext Transfer Protocol (HTTP).  
  
 This topic describes the locking interactions between each protocol.  
  
## SMB File Locking  
 SMB clients that mount file shares can leverage file system locking mechanisms to manage access to shared files. These include:  
  
-   Whole file access sharing for read, write, and delete.  
  
-   Byte range locks to manage read and write access to regions within a single file.  
  
 When an SMB client opens a file, it specifies both the file access and share mode. The following file access options are typically used by SMB clients, though all combinations are legal:  
  
-   **None:** Opens a file for query attribute access only.  
  
-   **Read:** Opens a file for read access only.  
  
-   **Write:** Opens a file for write access only.  
  
-   **Read/Write:** Opens a file with read/write permissions.  
  
-   **Delete:** Opens a file for delete access only.  
  
 The following file share modes are typically used by SMB clients:  
  
-   **None:** Declines sharing of the current file. Any request to open the file with read, write, or delete access will fail until the file is closed.  
  
-   **Shared Read:** Allows subsequent opening of the file for reading. If this flag is not specified, any request to open the file for reading will fail until the file is closed.  
  
-   **Shared Write:** Allows subsequent opening of the file for writing. If this flag is not specified, any request to open the file for writing will fail until the file is closed.  
  
-   **Shared Read/Write:** Allows subsequent opening of the file for reading or writing. If this flag is not specified, any request to open the file for reading or writing will fail until the file is closed.  
  
-   **Shared Delete:** Allows subsequent deleting of a file. If this flag is not specified, any request to delete the file will fail until the file is closed.  
  
## SMB Client Open File Examples  
 Consider the following open file examples:  
  
-   **File Opens without Sharing Violation**  
  
    -   Client A opens the file with FileAccess.Read and FileShare.Write (denies subsequent Read/Delete while open).  
  
    -   Client B then opens the file with FileAccess.Write with FileShare.Read (denies subsequent Write/Delete while open).  
  
    -   *Result:* This is allowed since there is no conflict between file access and file share modes.  
  
-   **Sharing Violation Due to File Access**  
  
    -   Client A opens the file with FileAccess.Write and FileShare.Read (denies subsequent Write/Delete while open).  
  
    -   Client B then opens the file with FileAccess.Write with FileShare.Write (denies subsequent Read/Delete while open).  
  
    -   *Result:* Client B encounters a sharing violation since it specified a file access that is denied by the share mode specified previously by Client A.  
  
-   **Sharing Violation Due to Share Mode**  
  
    -   Client A opens the file with FileAccess.Write and FileShare.Write (denies subsequent Read/Delete while open).  
  
    -   Client B then opens the file with FileAccess.Write with FileShare.Read (denies subsequent Write/Delete while open).  
  
    -   *Result:* Client B encounters a sharing violation since it specified a share mode that denies write access to a file that is still open for write access.  
  
## REST Operation File Access  
 When a File service operation is performed, it must respect the share mode specified for any file open on an SMB client. The following file access mode is used to determine whether the operation can be completed:  
  
|REST Operation|REST Operation File Access Equivalent|  
|--------------------|-------------------------------------------|  
|[List Directories and Files](../StorageServicesREST/List-Directories-and-Files.md)|N/A.|  
|[Create File](../StorageServicesREST/Create-File.md)|Write, Delete.|  
|[Get File](../StorageServicesREST/Get-File.md)|Read.|  
|[Set File Properties](../StorageServicesREST/Set-File-Properties.md)|Write.|  
|[Get File Properties](../StorageServicesREST/Get-File-Properties.md)|N/A.|  
|[Set File Metadata](../StorageServicesREST/Set-File-Metadata.md)|Write.|  
|[Get File Metadata](../StorageServicesREST/Get-File-Metadata.md)|N/A.|  
|[Delete File](../StorageServicesREST/Delete-File2.md)|Delete.|  
|[Put Range](../StorageServicesREST/Put-Range.md)|Write.|  
|[List Ranges](../StorageServicesREST/List-Ranges.md)|Read.|  
  
 [List Directories and Files](../StorageServicesREST/List-Directories-and-Files.md), [Get File Properties](../StorageServicesREST/Get-File-Properties.md), and [Get File Metadata](../StorageServicesREST/Get-File-Metadata.md) do not operate on file content and do not require read access to the file (*i.e.*, these operations will still succeed even if an SMB client has the file open for exclusive read access).  
  
 The following are examples of REST requests interacting with the SMB share modes:  
  
-   **REST Get File Sharing Violation**  
  
    -   The SMB Client opens the file with FileAccess.Read  and FileShare.Write (denies subsequent Read/Delete while open).  
  
    -   The REST Client then performs a [Get File](../StorageServicesREST/Get-File.md) operation on the file (thereby using FileAccess.Read as specified in the table above).  
  
    -   **Result:** The REST Client’s request fails with status code 409 (Conflict) and error code SharingViolation since the SMB client still has the file open while denying Read/Delete access.  
  
-   **REST Put Range Sharing Violation**  
  
    -   The SMB Client opens the file with FileAccess.Write and FileShare.Read (denies subsequent Write/Delete while open).  
  
    -   The REST Client then performs a [Put Range](../StorageServicesREST/Put-Range.md) operation on the file (thereby using FileAccess.Write as specified in the table above).  
  
    -   Result: The REST Client’s request fails with status code 409 (Conflict) and error code SharingViolation since SMB Client still has the file open while denying Write/Delete access.  
  
 The next section includes a comprehensive table of REST API sharing violation scenarios.  
  
## SMB Client Sharing Mode Implications on REST Operations  
 Depending on the share mode specified when an SMB client opens a file, it is possible for the REST service to return status code 409 (Conflict) with error code `SharingViolation` as described in the following table:  
  
|SMB Client File Sharing Mode|REST File Service Operations Failing with a Sharing Violation|  
|----------------------------------|-------------------------------------------------------------------|  
|`None`<br /><br /> `(Deny Read, Write, Delete)`|The following read, write, and delete operations on the file will fail:<br /><br /> -   Create File<br />-   Get File<br />-   Set File Properties<br />-   Set File Metadata<br />-   Delete File<br />-   Put Range<br />-   List Ranges|  
|`Shared Read`<br /><br /> `Deny Write, Delete)`|The following write and delete operations on the file will fail:<br /><br /> -   Create File<br />-   Set File Properties<br />-   Set File Metadata<br />-   Delete File<br />-   Put Range|  
|`Shared Write`<br /><br /> `(Deny Read, Delete)`|The following read and delete operations on the file will fail:<br /><br /> -   Create File.<br />-   Get File.<br />-   Delete File.<br />-   List Ranges.|  
|`Shared Delete`<br /><br /> `(Deny Read, Write)`|The following read and write operations on the file will fail:<br /><br /> -   Create File<br />-   Get File<br />-   Set File Properties<br />-   Set File Metadata<br />-   Put Range<br />-   List Ranges<br />-   Delete File|  
|`Shared Read/Write`<br /><br /> `(Deny Delete)`|The following delete operations on the file will fail:<br /><br /> -   Create File.<br />-   Delete File.|  
|`Shared Read/Delete`<br /><br /> `(Deny Write)`|The following write operations on the file will fail:<br /><br /> -   Create File<br />-   Set File Properties<br />-   Set File Metadata<br />-   Put Range<br />-   Delete File|  
|`Shared Write/Delete`<br /><br /> `(Deny Read)`|The following read operations on the file will fail:<br /><br /> -   Get File<br />-   List Ranges<br />-   Delete File|  
|`Shared Read/Write/Delete`<br /><br /> `(Deny Nothing)`|Delete File|  
  
 The File service will return sharing violations only when files are open on SMB clients. Note that for a File service [Delete File](../StorageServicesREST/Delete-File2.md) operation to succeed, there can be no SMB clients with handles open against that file. Please refer to the [Delete File](../StorageServicesREST/Delete-File2.md) operation and the section below titled **Interaction between the File Service and SMB Opportunistic Locks** for more details.  
  
## SMB Delete Implications on REST  
 When an SMB client opens a file for delete, it marks the file as pending delete until all other SMB client open handles on that file are closed. While a file is marked as pending delete, any REST operation on that file will return status code 409 (Conflict) with error code SMBDeletePending. Status code 404 (Not Found) is not returned since it is possible for the SMB client to remove the pending deletion flag prior to closing the file. In other words, status code 404 (Not Found) is only expected when the file has been removed.  
  
 Note that while a file is in a SMB pending delete state, it will not be included in the `List Files` results.  
  
 Also note that the REST `Delete File` and REST `Delete Directory` operations are committed atomically and do not result in pending delete state.  
  
## File Attribute Implications on REST  
 It is possible for SMB clients to read and set file attributes, including:  
  
-   Archive  
  
-   Read-only  
  
-   Hidden  
  
-   System  
  
 If a file or directory is marked read-only then any REST operation that attempts to write to the file will fail with status code 412 (Precondition Failed) and error code ReadOnlyAttribute. These operations include:  
  
-   `Create File`  
  
-   `Set File Properties`  
  
-   `Set File Metadata`  
  
-   `Put Range`  
  
 Note that these file attributes cannot be set or read from REST clients. Once a file is made read-only, REST clients will be unable to write to the file until the SMB client removes the read-only attribute.  
  
## Interaction between the File Service and SMB Opportunistic Locks  
 SMB opportunistic lock (*oplock*) is a caching mechanism that SMB clients request in order to improve performance and reduce network transfers. This means that the latest state of a particular file or directory may be cached on an SMB client. There are multiple opportunistic lock types, referred to as *SMB lease types*:  
  
-   **Read (R):** When acquired, the SMB client can read from local cache.  
  
-   **Write (W):** When acquired, the SMB client can write locally without the need to flush the data back to the File service.  
  
-   **Handle (H):** When acquired, the SMB client is not required to immediately notify the File service when a handle is closed. This is useful when an application continues opening and closing files with the same access and sharing mode.  
  
 Note that the above SMB lease types are independent of the access and sharing mode specified. Typically an SMB client attempts to acquire all lease types whenever it opens a new handle against a file, regardless of access and sharing mode.  
  
 Depending on the REST operation called, it may be necessary for a request to break an existing opportunistic lock. In the case of a write oplock, the SMB client must flush cached changes to the File service. Here are some cases where each type of oplock needs to be broken:  
  
-   A **Read (R)** oplock needs to be broken whenever a write operation is issued, such as `Put Range`.  
  
-   A **Write (W)** oplock needs to be broken whenever a read operation is issued, such as `Get File`.  
  
-   A **Handle (H)** oplock needs to be broken whenever a client issues a delete operation, since the File service requires that no handles can be open if a delete operation is to succeed.  
  
     Handle oplocks are also broken when a REST operation faces a sharing violation with an existing SMB handle (see the table on sharing violations above), in order to verify that the handle(s) are still opened by an application running on the client(s).  
  
 Breaking the oplock may require flushing cached SMB client changes, which may cause delays in operation response time, or may cause the operation to fail with status code 408 (Request Timeout) and error code `ClientCacheFlushDelay`.  
  
 Following are some scenarios where oplocks are broken:  
  
 **An opblock break and SMB client flush are required, and the REST client experiences a delay:**  
  
1.  The SMB client opens a file, acquires an RWH oplock, and writes data locally.  
  
2.  The REST Client sends a `Get File` request.  
  
    -   The File service breaks the write (W) oplock, leaving the client with an RH oplock.  
  
    -   The SMB client flushes its cached data against the File service and acknowledges the oplock break.  
  
    -   The File service processes the `Get File` request and responds back with the requested data.  
  
 In the above example, the REST client will experience delays caused by the oplock break and the time taken by the SMB client to flush its data against the File service.  
  
 Note that subsequent calls to `Get File` will not experience any additional delays since the write (W) oplock has already been broken.  
  
 **An oplock break is required, but the REST client won't experience a delay**  
  
1.  The SMB client has acquired an RH oplock.  
  
2.  The REST Client sends a `Put Range` request.  
  
    -   The File service sends an oplock break request to the SMB client and does not wait for a response.  
  
    -   The File service processes the `Put Range` request.  
  
 In the above example, the oplock break is required, but the `Put Range` request will not experience any additional delays since a response is not needed when breaking the read oplock.  
  
 The following table summarizes the behavior of the File service for each REST operation, based on the oplock state of the SMB client that has already acquired a handle on the same file, and assuming that the SMB handle access and sharing don't conflict with the REST operation. If there is a conflict, the handle oplock is also broken to ensure that the handle is still open on the client. In the case of a *blocking* oplock break, the File service must wait for an acknowledgement that the break was successful. In the case of a *non-blocking* oplock break, it does not have to wait.  
  
|REST Operation|Current OpLock types|OpLock break performed|Resulting Oplock|  
|--------------------|--------------------------|----------------------------|----------------------|  
|Get File|RWH|Yes (Blocking)|RH|  
|Get File|RH|No|RH|  
|Get File|RW|Yes (Blocking)|R|  
|Get File Properties|RWH|Yes (Blocking)|RH|  
|Get File Properties|RH|No|RH|  
|Get File Properties|RW|Yes (Blocking)|R|  
|List Ranges|RWH|Yes (Blocking)|RH|  
|List Ranges|RH|No|RH|  
|List Ranges|RW|Yes (Blocking)|R|  
|Get File Metadata|RWH|Yes (Blocking)|RH|  
|Get File Metadata|RH|No|RH|  
|Get File Metadata|RW|Yes (Blocking)|R|  
|List Files|RWH|No|RWH|  
|List Files|RH|No|RH|  
|List Files|RW|No|RW|  
|Put Range|RWH|Yes (Blocking)|None|  
|Put Range|RH|Yes (Non-Blocking)|None|  
|Put Range|RW|Yes(Blocking)|None|  
|Set File Properties|RWH|Yes (Blocking)|None|  
|Set File Properties|RH|Yes (Non-Blocking)|None|  
|Set File Properties|RW|Yes (Blocking)|None|  
|Set File Metadata|RWH|Yes (Blocking)|None|  
|Set File Metadata|RH|Yes (Non-Blocking)|None|  
|Set File Metadata|RW|Yes (Blocking)|None|  
|Delete File|RWH|Yes (Blocking)|RW|  
|Delete File|RH|Yes (Blocking)|R|  
|Delete File|RW|No|RW|  
  
 In the case where a blocking oplock break is required, if the break does not succeed within the specified request timeout or within 30 seconds, whichever completes first, the REST operation will fail with status code 408 (Request Timeout) and error code `ClientCacheFlushDelay`.  
  
 Note that the `Delete File` request also requires breaking the oplock handle (H) lease. This ensures that there are no file handles still opened by an SMB client application when a REST client calls `Delete File`. If there is a sharing violation, the request fails with status code 409 (Conflict) and error code `SharingViolation`.  
  
## See Also  
 [File Service Concepts](../StorageServicesREST/File-Service-Concepts.md)
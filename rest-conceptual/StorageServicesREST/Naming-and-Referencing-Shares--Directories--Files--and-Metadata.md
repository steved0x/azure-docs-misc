---
title: "Naming and Referencing Shares, Directories, Files, and Metadata"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: f38d4c69-cb50-4ef3-a8a3-276341689769
caps.latest.revision: 14
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
# Naming and Referencing Shares, Directories, Files, and Metadata
A storage account can contain zero or more Azure File shares. A share contains properties, metadata, and zero or more files or directories. A directory contains properties and zero or more files or directories. A file is any single entity comprised of binary data, properties, and metadata.  
  
## Resource Names  
 The URI to reference a share, directory or file must be unique. Within a given storage account, every share must have a unique name. Every file within a given share or directory must also have a unique name within that share or directory.  
  
 If you attempt to create a share, directory, or file with a name that violates naming rules, the request will fail with status code 400 (Bad Request).  
  
## Share Names  
 The rules for File service share names are more restrictive than what is prescribed by the SMB protocol for SMB share names, so that the Blob and File services can share similar naming conventions for containers and shares. The naming restrictions for shares are as follows:  
  
-   A share name must be a valid DNS name.  
  
-   Share names must start with a letter or number, and can contain only letters, numbers, and the dash (-) character.  
  
-   Every dash (-) character must be immediately preceded and followed by a letter or number; consecutive dashes are not permitted in share names.  
  
-   All letters in a share name must be lowercase.  
  
-   Share names must be from 3 through 63 characters long.  
  
 For those interested, the below table shows a comparison of the naming restrictions for the SMB protocol as well as for the Blob service today:  
  
|[Naming and Referencing Containers, Blobs, and Metadata](../StorageServicesREST/Naming-and-Referencing-Containers--Blobs--and-Metadata.md)|[SMB Share Name Restrictions](http://msdn.microsoft.com/library/cc422525\(v=prot.13\))|  
|-------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|  
|-   A container name must be a valid DNS name.<br />-   Container names must start with a letter or number, and can contain only letters, numbers, and the dash (-) character.<br />-   Every dash (-) character must be immediately preceded and followed by a letter or number; consecutive dashes are not permitted in container names.<br />-   All letters in a container name must be lowercase.<br />-   Container names must be 3 to 63 characters long.|-   A share name must be no more than 80 characters in length.<br />-   The following characters are illegal in a share name: `\ / [ ] : &#124; < > + = ; , * ? "`<br />-   Control characters in range 0x00 through 0x1F, inclusive, are illegal in a share name.<br />-   All other Unicode characters are legal.<br />-   Names are case preserving and case insensitive.|  
  
## Directory and File Names  
 The Azure File service naming rules for directory and file names are as follows:  
  
-   Directory and file names are case-preserving and case-insensitive.  
  
-   Directory and file component names must be no more than 255 characters in length.  
  
-   Directory names cannot end with the forward slash character (/). If provided, it will be automatically removed.  
  
-   File names must not end with the forward slash character (/).  
  
-   Reserved URL characters must be properly escaped.  
  
-   The following characters are not allowed: `" \ / : | < > * ?`  
  
-   Illegal URL path characters not allowed. Code points like `\uE000`, while valid in NTFS filenames, are not valid Unicode characters. In addition, some ASCII or Unicode characters, like control characters (`0x00` to `0x1F`, `\u0081`, etc.), are also not allowed. For rules governing Unicode strings in HTTP/1.1 see [RFC 2616, Section 2.2: Basic Rules](http://www.ietf.org/rfc/rfc2616.txt) and [RFC 3987](http://www.ietf.org/rfc/rfc3987.txt).  
  
-   The following file names are not allowed: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, dot character (.), and two dot characters (..).  
  
 For those interested, the below table shows a comparison of the naming restrictions for the SMB protocol as well as the Blob service today:  
  
|[Naming and Referencing Containers, Blobs, and Metadata](../StorageServicesREST/Naming-and-Referencing-Containers--Blobs--and-Metadata.md)|[SMB Protocol Name Restrictions](http://msdn.microsoft.com/library/cc422524\(v=prot.13\))|  
|-------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|  
|1.  A blob name must be at least one character long and cannot be more than 1,024 characters long.<br />2.  Blob names are case-sensitive.<br />3.  Reserved URL characters must be properly escaped.<br />4.  Blob names can end with a virtual directory delimiter, such as a forward slash (/)<br />5.  Illegal URL path characters not allowed: Code points like \uE000, while valid in NTFS filenames, are not valid Unicode characters. In addition, some ASCII or Unicode characters, like control characters (0x00 to 0x1F, \u0081, etc.), are also not allowed. For rules governing Unicode strings in HTTP/1.1 see [RFC 2616, Section 2.2: Basic Rules](http://www.ietf.org/rfc/rfc2616.txt) and [RFC 3987](http://www.ietf.org/rfc/rfc3987.txt).|-   A pathname may be no more than 32,760 characters in length.<br />-   Each pathname component (file / directory) may be no more than 255 characters in length.<br />-   A pathname is composed of one or more pathname components separated by the (\\) backward slash character.<br />-   Pathname is case preserving and case insensitive (two names which differ only in case is not allowed).<br />-   Cannot have a directory path that is the same as a file path.<br />-   The following characters are illegal in a component name: `\ / : &#124; < > * ? "`<br />-   Control characters in range 0x00 through 0x1F, inclusive, are illegal in a share name.|  
  
## Pathnames  
 A pathname is composed of one or more pathname components (directory or file name) separated by the forward-slash (/) character. All pathname components other than the last path name component denote directories. The last path name component denotes a directory or a file. The following naming rules apply:  
  
1.  A pathname may be no more than 1,024 characters in length.  
  
2.  A pathname is composed of one or more pathname components separated by the forward-slash (/) character.  
  
3.  The depth of subdirectories in the path cannot exceed 250.  
  
4.  The same name cannot be used for a file and a directory that share the same parent directory. For example, a file and a directory that are each named `data` cannot exist under the same parent path.  
  
## Metadata Names  
 Metadata for a share or file resource is stored as name-value pairs associated with the resource. Directories do not have metadata. Metadata names must adhere to the naming rules for [C# identifiers](http://msdn.microsoft.com/library/aa664670\(VS.71\).aspx).  
  
 Note that metadata names preserve the case with which they were created, but are case-insensitive when set or read. If two or more metadata headers with the same name are submitted for a resource, the Azure File service returns status code 400 (Bad Request).  
  
## Resource URI Syntax  
 Each resource has a corresponding base URI, which refers to the resource itself. For the storage account, the base URI includes the name of the account only:  
  
```  
https://myaccount.file.core.windows.net  
```  
  
 For a share, the base URI includes the name of the account and the name of the share:  
  
```  
https://myaccount.file.core.windows.net/myshare  
```  
  
 For a directory, the base URI includes the name of the account, the name of the share, and the path of the directory:  
  
```  
https://myaccount.file.core.windows.net/myshare/myparentdir/mydir  
```  
  
 For a file, the base URI includes the name of the account, name of the share, and the path of the file:  
  
```  
https://myaccount.file.core.windows.net/myshare/myfile  
https://myaccount.file.core.windows.net/myshare/mydir/myfile  
https://myaccount.file.core.windows.net/myshare/myparentdir/mydir/myfile  
```  
  
## See Also  
 [File Service Concepts](../StorageServicesREST/File-Service-Concepts.md)
---
title: "Naming and Referencing Containers, Blobs, and Metadata"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: d525950c-17ba-4b3b-9ed1-19a2145f769a
caps.latest.revision: 49
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
# Naming and Referencing Containers, Blobs, and Metadata
This topic describes naming and referring to containers, blobs, metadata, and snapshots. A storage account can contain zero or more containers. A container contains properties, metadata, and zero or more blobs. A blob is any single entity comprised of binary data, properties, and metadata.  
  
## Resource Names  
 The URI to reference a container or a blob must be unique. Because every account name is unique, two accounts can have containers with the same name. However, within a given storage account, every container must have a unique name. Every blob within a given container must also have a unique name within that container.  
  
 If you attempt to create a container or blob with a name that violates naming rules, the request will fail with status code 400 (Bad Request).  
  
> [!IMPORTANT]
>  Blob and container names are passed to the Blob service within a URL. Certain characters must be percent-encoded to appear in a URL, using UTF-8 (preferred) or MBCS. This encoding occurs automatically when you use the Azure .NET Libraries or construct a <xref:System.Uri?qualifyHint=False> object that includes a blob or container name. However, there are certain characters that are not valid in URL paths even when encoded. These characters cannot appear in blob or container names.  Code points like \uE000, while valid in NTFS filenames, are not valid Unicode characters, so they cannot be used.  In addition, some ASCII or Unicode characters, like control characters (0x00 to 0x1F, \u0081, etc.), are also not allowed. For rules governing Unicode strings in HTTP/1.1 see:  
>   
>  -   [RFC 2616, Section 2.2: Basic Rules](http://www.ietf.org/rfc/rfc2616.txt)  
> -   [RFC 3987](http://www.ietf.org/rfc/rfc3987.txt)  
  
### Container Names  
 A container name must be a valid DNS name, conforming to the following naming rules:  
  
1.  Container names must start with a letter or number, and can contain only letters, numbers, and the dash (-) character.  
  
2.  Every dash (-) character must be immediately preceded and followed by a letter or number; consecutive dashes are not permitted in container names.  
  
3.  All letters in a container name must be lowercase.  
  
4.  Container names must be from 3 through 63 characters long.  
  
### Blob Names  
 A blob name must conforming to the following naming rules:  
  
-   A blob name can contain any combination of characters.  
  
-   A blob name must be at least one character long and cannot be more than 1,024 characters long.  
  
-   Blob names are case-sensitive.  
  
-   Reserved URL characters must be properly escaped.  
  
-   The number of path segments comprising the blob name cannot exceed 254. A path segment is the string between consecutive delimiter characters (*e.g.*, the forward slash '/') that corresponds to the name of a virtual directory.  
  
> [!NOTE]
>  Avoid blob names that end with a dot (.), a forward slash (/), or a sequence or combination of the two.  
  
 The Blob service is based on a flat storage scheme, not a hierarchical scheme. However, you may specify a character or string delimiter within a blob name to create a virtual hierarchy. For example, the following list shows valid and unique blob names. Notice that a string can be valid as both a blob name and as a virtual directory name in the same container:  
  
-   /a  
  
-   /a.txt  
  
-   /a/b  
  
-   /a/b.txt  
  
 You can take advantage of the delimiter character when enumerating blobs.  
  
### Metadata Names  
 Metadata for a container or blob resource is stored as name-value pairs associated with the resource. Metadata names must adhere to the naming rules for [C# identifiers](http://msdn.microsoft.com/library/aa664670\(VS.71\).aspx).  
  
 Note that metadata names preserve the case with which they were created, but are case-insensitive when set or read. If two or more metadata headers with the same name are submitted for a resource, the Blob service returns status code 400 (Bad Request).  
  
## Resource URI Syntax  
 Each resource has a corresponding base URI, which refers to the resource itself.  
  
 For the storage account, the base URI includes the name of the account only:  
  
```  
https://myaccount.blob.core.windows.net  
```  
  
 For a container, the base URI includes the name of the account and the name of the container:  
  
```  
https://myaccount.blob.core.windows.net/mycontainer  
```  
  
 For a blob, the base URI includes the name of the account, the name of the container, and the name of the blob:  
  
```  
https://myaccount.blob.core.windows.net/mycontainer/myblob  
```  
  
 A storage account may have a root container, a default container that can be omitted from the URI. A blob in the root container can be referenced without naming the container, or the root container can be explicitly referenced by its name (`$root`). See [Working with the Root Container](../StorageServicesREST/Working-with-the-Root-Container.md) for more information. The following URIs both refer to a blob in the root container:  
  
```  
  
https://myaccount.blob.core.windows.net/myblob  
https://myaccount.blob.core.windows.net/$root/myblob  
  
```  
  
## Blob Snapshots  
 A snapshot is a read-only version of a blob stored as it was at the time the snapshot was created. You can use snapshots to create a backup or checkpoint of a blob. A snapshot blob name includes the base blob URI plus a date-time value that indicates when the snapshot was created.  
  
 For example, assume that a blob has the following URI:  
  
```  
https://myaccount.blob.core.windows.net/mycontainer/myblob  
```  
  
 The URI for a snapshot of that blob is formed as follows:  
  
```  
https://myaccount.blob.core.windows.net/mycontainer/myblob?snapshot=<DateTime>  
```  
  
 The .NET client library can list snapshots as <xref:Microsoft.WindowsAzure.StorageClient.CloudBlob?qualifyHint=False> objects when you call <xref:Microsoft.WindowsAzure.StorageClient.CloudBlobContainer.ListBlobs?qualifyHint=False> with <xref:Microsoft.WindowsAzure.StorageClient.BlobRequestOptions.BlobListingDetails?qualifyHint=False> set to <xref:Microsoft.WindowsAzure.StorageClient.BlobListingDetails.Snapshots?qualifyHint=False>.  
  
## See Also  
 [How to Use the Blob Storage Service](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)   
 [Enumerating Blob Resources](../StorageServicesREST/Enumerating-Blob-Resources.md)   
 [Blob Service Concepts](../StorageServicesREST/Blob-Service-Concepts.md)   
 [Working with the Root Container](../StorageServicesREST/Working-with-the-Root-Container.md)   
 [Snapshot Blob](../StorageServicesREST/Snapshot-Blob.md)
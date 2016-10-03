---
title: "File Service REST API"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: db279087-50f1-4465-93a5-3bcf25e1f19b
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
# File Service REST API
The Server Message Block (SMB) protocol is the preferred file share protocol used on premise today. The Microsoft Azure File service enables customers to leverage the availability and scalability of Azure’s Cloud Infrastructure as a Service (IaaS) SMB without having to rewrite SMB client applications.  
  
 The Azure File service also offers a compelling alternative to traditional Direct Attached Storage (DAS) and Storage Area Network (SAN) solutions, which are often complex and expensive to install, configure, and operate. Pricing for the new Azure File service is consistent with existing Azure Storage services and is charged in units of storage capacity and transactions. See the [Azure Storage Pricing page](https://www.windowsazure.com/pricing/details/) for details.  
  
 Files stored in Azure File service shares are accessible via the SMB protocol, and also via REST APIs, at the endpoint `http|https://<account>.file.core.window.net`. Note that HTTPS is recommended.  
  
 While the Azure File service REST APIs are similar to the Azure Blob service REST APIs, there are minor differences related to how the service models the underlying file system. These differences are noted in the operations table below.  
  
## Azure File Service REST Operations  
 The Azure File service offers the following four resources: the storage account, shares, directories, and files. Shares provide a way to organize sets of files and also can be mounted as an SMB file share that is hosted in the cloud.  
  
 The File service REST API provides a way to work with share, directory, and file resources via HTTP/HTTPS operations. File service operations are available only in version 2014-02-14 of the storage services or later.  
  
 The File service REST API includes the operations listed in the table below.  
  
|Operation|Resource Type|REST Verb|Description|Differences with corresponding Blob service operation|  
|---------------|-------------------|---------------|-----------------|-----------------------------------------------------------|  
|[List Shares](../rest-conceptual/List-Shares.md)|Storage account|GET|Lists all the file shares in a storage account|None|  
|[Get File Service Properties](../rest-conceptual/Get-File-Service-Properties.md)|Storage account|GET|Gets the File service properties for the storage account|None|  
|[Set File Service Properties](../rest-conceptual/Set-File-Service-Properties.md)|Storage account|PUT|Sets the File service properties for the storage account|None|  
|[Preflight File Request](../rest-conceptual/Preflight-File-Request.md)|Storage account|OPTIONS|Queries the Cross-Origin Resource Sharing (CORS) rules for the File service prior to sending the actual request.|None|  
|[Create Share](../rest-conceptual/Create-Share.md)|Share|PUT|Creates a new share in a storage account.|Request header|  
|[Get Share ACL](../rest-conceptual/Get-Share-ACL.md)|Share|GET/HEAD|Returns information about stored access policies specified on the share.|Response body|  
|[Set Share ACL](../rest-conceptual/Set-Share-ACL.md)|Share|PUT|Sets a stored access policy for use with shared access signatures.|Request body|  
|[Get Share Properties](../rest-conceptual/Get-Share-Properties.md)|Share|GET/HEAD|Returns all user-defined metadata and system properties of a share.|None|  
|[Set Share Properties](../rest-conceptual/Set-Share-Properties.md)|Share|PUT|Sets system properties for a share.|N/A|  
|[Get Share Metadata](../rest-conceptual/Get-Share-Metadata.md)|Share|GET/HEAD|Returns only user-defined metadata of a share.|None|  
|[Set Share Metadata](../rest-conceptual/Set-Share-Metadata.md)|Share|PUT|Sets user-defined metadata of a share.|None|  
|[Get Share Stats](../rest-conceptual/Get-Share-Stats.md)|Share|GET|Retrieves statistics related to the share.|N/A|  
|[Delete Share](../rest-conceptual/Delete-Share.md)|Share|DELETE|Deletes the share and any files and directories that it contains.|None|  
|[List Directories and Files](../rest-conceptual/List-Directories-and-Files.md)|Directory|GET|Lists files and directories within the share or specified directory.|Query String Params, Response Body|  
|[Create Directory](../rest-conceptual/Create-Directory.md)|Directory|PUT|Creates a directory in the share or parent directory.|New|  
|[Get Directory Properties](../rest-conceptual/Get-Directory-Properties.md)|Directory|GET/HEAD|Returns system defined properties of a directory. This allows users to check for directory existence. Only LMT i.e. created date will be returned.|New|  
|[Get Directory Metadata](../rest-conceptual/Get-Directory-Metadata.md)|Directory|GET/HEAD|Retrieves all user-defined metadata on the directory.|New|  
|[Set Directory Metadata](../rest-conceptual/Set-Directory-Metadata.md)|Directory|PUT|Sets user-defined metadata of an existing directory.|New|  
|[Delete Directory](../rest-conceptual/Delete-Directory.md)|Directory|DELETE|Deletes the directory. Only supported for empty directories.|New|  
|[Create File](../rest-conceptual/Create-File.md)|File|PUT|Creates a new file or replaces an existing file within a directory or share.|Name<br /><br /> Request Headers|  
|[Get File](../rest-conceptual/Get-File.md)|File|GET|Reads or downloads a file from the File service, including its user-defined metadata and system properties.|Name, Response Headers|  
|[Set File Properties](../rest-conceptual/Set-File-Properties.md)|File|PUT|Sets system properties defined for an existing file.|Name,<br /><br /> Request & Response Headers|  
|[Get File Properties](../rest-conceptual/Get-File-Properties.md)|File|HEAD|Returns all system properties and user-defined metadata on the file.|Name, Response Headers|  
|[Get File Metadata](../rest-conceptual/Get-File-Metadata.md)|File|GET/HEAD|Retrieves all user-defined metadata on the file.|Name only|  
|[Set File Metadata](../rest-conceptual/Set-File-Metadata.md)|File|PUT|Sets user-defined metadata of an existing file.|Name only|  
|[Delete File](../rest-conceptual/Delete-File2.md)|File|DELETE|Deletes the file permanently.|Name only|  
|[Copy File](../rest-conceptual/Copy-File.md)|File|PUT|Copies a source blob or file to a destination file in this storage account.|Name, Param, Response Headers|  
|[Abort Copy File](../rest-conceptual/Abort-Copy-File.md)|File|PUT|Aborts a pending [Copy File](../rest-conceptual/Copy-File.md) operation, and leaves a destination file with zero length and full metadata.|Name, Param, Response Headers|  
|[Put Range](../rest-conceptual/Put-Range.md)|File|PUT|Puts a range of data into a file, or clears a range in the file.|Name,<br /><br /> Query String Param, Response Header & Body|  
|[List Ranges](../rest-conceptual/List-Ranges.md)|File|GET|Returns a list of active ranges for the file. Active ranges are those that have been populated with data using Put Range API.|Name,<br /><br /> Query String Param, Response Body|  
  
## In This Section  
 This section contains the following topics.  
  
-   [Features Not Supported By the Azure File Service](../rest-conceptual/Features-Not-Supported-By-the-Azure-File-Service.md)  
  
-   [File Service Concepts](../rest-conceptual/File-Service-Concepts.md)  
  
-   [Operations on the Account (File Service)](../rest-conceptual/Operations-on-the-Account--File-Service-.md)  
  
-   [Operations on Shares (File Service)](../rest-conceptual/Operations-on-Shares--File-Service-.md)  
  
-   [Operations on Directories](../rest-conceptual/Operations-on-Directories.md)  
  
-   [Operations on Files](../rest-conceptual/Operations-on-Files.md)  
  
## See Also  
 [Storage Services REST](../rest-conceptual/Azure-Storage-Services-REST-API-Reference.md)
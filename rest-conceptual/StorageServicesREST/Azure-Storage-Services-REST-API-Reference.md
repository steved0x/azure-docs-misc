---
title: "Azure Storage Services REST API Reference"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 1db599af-4cb7-4869-af4b-7bfd6a3a48e8
caps.latest.revision: 42
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
# Azure Storage Services REST API Reference
The REST APIs for the Windows® Azure™ storage services offer programmatic access to the Blob, Queue, Table, and File services in Azure or in the development environment, via the storage emulator.  
  
 All storage services are accessible via REST APIs. Storage services may be accessed from within a service running in Azure, or directly over the Internet from any application that can send an HTTP/HTTPS request and receive an HTTP/HTTPS response.  
  
> [!IMPORTANT]
>  The Azure storage services support both HTTP and HTTPS; however, using HTTPS is highly recommended.  
  
## Storage Account  
 All access to storage services takes place through the storage account. The storage account is the highest level of the namespace for accessing each of the fundamental services. It is also the basis for authentication.  
  
 The REST APIs for storage services expose the storage account as a resource.  
  
 To create and manage a storage account, see [Manage Accounts, Subscriptions, and Administrative Roles](assetId:///673cc2bd-6232-4152-9a6f-6d80324d7f87).  
  
## Blob Service  
 The Blob service provides storage for entities, such as binary files and text files. The REST API for the Blob service exposes two resources: containers and blobs. A container is a set of blobs; every blob must belong to a container. The Blob service defines three types of blobs:  
  
-   Block blobs, which are optimized for streaming. This type of blob is the only blob type available with versions prior to 2009-09-19.  
  
-   Page blobs, which are optimized for random read/write operations and which provide the ability to write to a range of bytes in a blob. Page blobs are available with version 2009-09-19 and later.  
  
-   Append blobs, which are optimized for append operations only. Append blobs are available only with version 2015-02-21 and later.  
  
 Containers and blobs support user-defined metadata in the form of name-value pairs specified as headers on a request operation.  
  
 Using the REST API for the Blob service, developers can create a hierarchical namespace similar to a file system. Blob names may encode a hierarchy by using a configurable path separator. For example, the blob names *MyGroup/MyBlob1* and *MyGroup/MyBlob2* imply a virtual level of organization for blobs. The enumeration operation for blobs supports traversing the virtual hierarchy in a manner similar to that of a file system, so that you can return a set of blobs that are organized beneath a group. For example, you can enumerate all blobs organized under *MyGroup/*.  
  
 A block blob may be created in one of two ways. Block blobs less than or equal to 64 MB in size can be uploaded by calling the [Put Blob](../StorageServicesREST/Put-Blob.md) operation. Block blobs larger than 64 MB must be uploaded as a set of blocks, each of which must be less than or equal to 4 MB in size. A set of successfully uploaded blocks can be assembled in a specified order into a single contiguous blob by calling [Put Block List](../StorageServicesREST/Put-Block-List.md). The maximum size currently supported for a block blob is 200,000 MB.  
  
 Page blobs are created and initialized with a maximum size with a call to [Put Blob](../StorageServicesREST/Put-Blob.md). To write content to a page blob, you call the [Put Page](../StorageServicesREST/Put-Page.md) operation. The maximum size currently supported for a page blob is 1 TB.  
  
 Append blobs can be created by calling [Put Blob](../StorageServicesREST/Put-Blob.md). An append blob created with the [Put Blob](../StorageServicesREST/Put-Blob.md) operation does not include any content. To write content to an append blob, you add blocks to the end of the blob by calling the [Append Block](../StorageServicesREST/Append-Block.md) operation. Updating or deleting existing blocks is not supported. Each block can be of different size, up to a maximum of 4 MB. The maximum size for a append blob is 200,000 MB, and an append blob can include no more than 50,000 blocks.  
  
 Blobs support conditional update operations that may be useful for concurrency control and efficient uploading.  
  
 Blobs can be read by calling the [Get Blob](../StorageServicesREST/Get-Blob.md) operation. A client may read the entire blob, or an arbitrary range of bytes.  
  
 For the Blob service API reference, see [Blob Service REST API](../StorageServicesREST/Blob-Service-REST-API.md).  
  
## Queue Service  
 The Queue service provides reliable, persistent messaging within and between services. The REST API for the Queue service exposes two resources: queues and messages.  
  
 Queues support user-defined metadata in the form of name-value pairs specified as headers on a request operation.  
  
 Each storage account may have an unlimited number of message queues that are named uniquely within the account. Each message queue may contain an unlimited number of messages. The maximum size for a message is limited to 64KB for version 2011-08-18 and 8KB for previous versions.  
  
 When a message is read from the queue, the consumer is expected to process the message and then delete it. After the message is read, it is made invisible to other consumers for a specified interval. If the message has not yet been deleted at the time the interval expires, its visibility is restored, so that another consumer may process it.  
  
 For more information about the Queue service, see [Queue Service REST API](../StorageServicesREST/Queue-Service-REST-API.md).  
  
## Table Service  
 The Table service provides structured storage in the form of tables. The Table service supports a REST API that implements the [OData protocol](http://www.odata.org/).  
  
 Within a storage account, a developer may create named tables. Tables store data as entities. An entity is a collection of named properties and their values, similar to a row. Tables are partitioned to support load balancing across storage nodes. Each table has as its first property a partition key that specifies the partition an entity belongs to. The second property is a row key that identifies an entity within a given partition. The combination of the partition key and the row key forms a primary key that identifies each entity uniquely within the table.  
  
 The Table service does not enforce any schema. A developer may choose to implement and enforce a schema on the client side. For more information about the Table service, see [Table Service REST API](../StorageServicesREST/Table-Service-REST-API.md).  
  
## File Service  
 The Server Message Block (SMB) protocol is the preferred file share protocol used on premise today. The Microsoft Azure File service enables customers to leverage the availability and scalability of Azure’s Cloud Infrastructure as a Service (IaaS) SMB without having to rewrite SMB client applications.  
  
 The Azure File service also offers a compelling alternative to traditional Direct Attached Storage (DAS) and Storage Area Network (SAN) solutions, which are often complex and expensive to install, configure, and operate.  
  
 Files stored in Azure File service shares are accessible via the SMB protocol, and also via REST APIs. The File service offers the following four resources: the storage account, shares, directories, and files. Shares provide a way to organize sets of files and also can be mounted as an SMB file share that is hosted in the cloud.  
  
## See Also  
 [Blob Service REST API](../StorageServicesREST/Blob-Service-REST-API.md)   
 [Queue Service REST API](../StorageServicesREST/Queue-Service-REST-API.md)   
 [Table Service REST API](../StorageServicesREST/Table-Service-REST-API.md)   
 [File Service REST API](../StorageServicesREST/File-Service-REST-API.md)
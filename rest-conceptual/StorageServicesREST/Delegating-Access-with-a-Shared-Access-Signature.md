---
title: "Delegating Access with a Shared Access Signature"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 98f3411e-d85d-4be9-809e-135b3d4ed436
caps.latest.revision: 36
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
# Delegating Access with a Shared Access Signature
A shared access signature (SAS) is a URI that grants restricted access rights to Azure Storage resources. You can provide a shared access signature to clients who should not be trusted with your storage account key but to whom you wish to delegate access to certain storage account resources. By distributing a shared access signature URI to these clients, you can grant them access to a resource for a specified period of time, with a specified set of permissions.  
  
 The URI query parameters comprising the SAS token incorporate all of the information necessary to grant controlled access to a storage resource. A client who is in possession of the SAS can make a request against Azure Storage with just the SAS URI, and the information contained in the SAS token is used to authenticate the request.  
  
 Beginning with version 2015-04-05, Azure Storage supports two types of shared access signatures (SAS):  
  
-   An account-level SAS, introduced with version 2015-04-05. The account SAS delegates access to resources in one or more of the storage services. All of the operations available via a service SAS are also available via an account SAS. Additionally, with the account SAS, you can delegate access to operations that apply to a given service, such as `Get/Set Service Properties` and `Get Service Stats`. You can also delegate access to read, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS. See [Constructing an Account SAS](../StorageServicesREST/Constructing-an-Account-SAS.md) for more information about account SAS.  
  
-   A service-level SAS. The service SAS delegates access to a resource in just one of the storage services: the Blob, Queue, Table, or File service. See [Constructing a Service SAS](../StorageServicesREST/Constructing-a-Service-SAS.md) and [Service SAS Examples](../StorageServicesREST/Service-SAS-Examples.md) for more information about service SAS.  
  
> [!NOTE]
>  Stored access policies are currently not supported for account SAS.  
  
 Additionally, a service SAS can reference a stored access policy that provides an additional level of control over a set of signatures, including the ability to modify or revoke access to the resource if necessary. For more information on stored access policies, see [Establishing a Stored Access Policy](../StorageServicesREST/Establishing-a-Stored-Access-Policy.md).  
  
## See Also  
 [Storage Services REST](../StorageServicesREST/Azure-Storage-Services-REST-API-Reference.md)
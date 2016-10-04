---
title: "Establishing a Stored Access Policy"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 52285540-5788-4b38-ac30-f40a68a93dde
caps.latest.revision: 9
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
# Establishing a Stored Access Policy
A stored access policy provides an additional level of control over service-level shared access signatures (SAS) on the server side. Establishing a stored access policy serves to group shared access signatures and to provide additional restrictions for signatures that are bound by the policy. You can use a stored access policy to change the start time, expiry time, or permissions for a signature, or to revoke it after it has been issued.  
  
 The following storage resources support stored access policies:  
  
-   Blob containers  
  
-   File shares  
  
-   Queues  
  
-   Tables  
  
 For more details on working with stored access policies, see [Use a Stored Access Policy](assetId:///c0d4fe58-e6f4-4a90-bad5-138f59967560).  
  
> [!NOTE]
>  Note that a stored access policy on a container can be associated with a shared access signature granting permissions to the container itself or to the blobs it contains. Similarly, a stored access policy on a file share can be associated with a shared access signature granting permissions to the share itself or to the files it contains.  
>   
>  Stored access policies are currently not supported for account SAS.  
  
## Creating or Modifying a Stored Access Policy  
 To create or modify a stored access policy, call the Set ACL operation for the resource (*i.e.*, [Set Container ACL](../StorageServicesREST/Set-Container-ACL.md), [Set Queue ACL](../StorageServicesREST/Set-Queue-ACL.md), [Set Table ACL](../StorageServicesREST/Set-Table-ACL.md), [Set Share ACL](../StorageServicesREST/Set-Share-ACL.md)) with a request body that specifies the terms of the access policy. The body of the request includes a unique signed identifier of your choosing, up to 64 characters in length, and the optional parameters of the access policy, as follows:  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<SignedIdentifiers>  
  <SignedIdentifier>   
    <Id>unique-64-char-value</Id>  
    <AccessPolicy>  
      <Start>start-time</Start>  
      <Expiry>expiry-time</Expiry>  
      <Permission>abbreviated-permission-list</Permission>  
    </AccessPolicy>  
  </SignedIdentifier>  
</SignedIdentifiers>  
  
```  
  
> [!NOTE]
>  Table entity range restrictions (`startpk`, `startrk`, `endpk`, and `endrk`) cannot be specified in a stored access policy.  
  
 A maximum of five access policies may be set on a container, table, or queue at any given time. Each `SignedIdentifier` field, with its unique `Id` field, corresponds to one access policy. Attempting to set more than five access policies at one time results in the service returning status code 400 (Bad Request).  
  
## Modifying or Revoking a Shared Access Signature  
 To modify the parameters of the stored access policy, you can call the access control list operation for the resource type to replace the existing policy, specifying a new start time, expiry time, or set of permissions. For example, if your existing policy grants read and write permissions to a resource, you can modify it to grant only read permissions for all future requests. In this case, the signed identifier of the new policy, as specified by the `ID` field, would be identical to the signed identifier of the policy you are replacing.  
  
 To revoke a stored access policy, you can either delete it, or rename it by changing the signed identifier. Changing the signed identifier breaks the associations between any existing signatures and the stored access policy. Deleting or renaming the stored access policy immediately effects all of the shared access signatures associated with it.  
  
 To remove a single access policy, call the resource's Set ACL operation, passing in the set of signed identifiers that you wish to maintain on the container. To remove all access policies from the resource, call the Set ACL operation with an empty request body.  
  
## See Also  
 [Delegating Access with a Shared Access Signature](../StorageServicesREST/Delegating-Access-with-a-Shared-Access-Signature.md)
---
title: "Versioning for the Azure Storage Services"
ms.custom: na
ms.date: 2016-09-22
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: cc4fba5c-7015-40bf-a29c-b6f0c684ff3c
caps.latest.revision: 58
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
# Versioning for the Azure Storage Services
The Microsoft Azure storage services support multiple versions. To make a request against the storage services, you must specify the version that you want to use for that operation, unless the request is anonymous.  
  
 The current version of the Azure storage services is 2015-12-11, and using that version is recommended where possible. For a list of all other supported versions, and for information about using each version, see [Azure Storage Services Versions 2015-07-08 and Earlier](../StorageServicesREST/Azure-Storage-Services-Versions-2015-07-08-and-Earlier.md).  
  
## Version 2015-12-11  
 Version 2015-12-11 includes these changes:  
  
-   The [Put Blob](../StorageServicesREST/Put-Blob.md), [Put Block](../StorageServicesREST/Put-Block.md), [Put Block List](../StorageServicesREST/Put-Block-List.md), [Put Page](../StorageServicesREST/Put-Page.md), [Append Block](../StorageServicesREST/Append-Block.md), and [Set Blob Metadata](../StorageServicesREST/Set-Blob-Metadata.md) operations now return the `x-ms-request-server-encrypted` response header. This header is set to `true` if the contents of the request have been successfully encrypted.  
  
-   The [Get Blob](../StorageServicesREST/Get-Blob.md) and [Get Blob Properties](../StorageServicesREST/Get-Blob-Properties.md) operations now return the `x-ms-server-encrypted` response header. This header is set to `true` if the blob data and application metadata are completely encrypted. If the blob is not encrypted, or if only parts of the blob/application metadata are encrypted, this header is set to `false`.  
  
-   Beginning with version 2015-12-11, the AtomPub payload format is no longer supported for Table service operations. Version 2015-12-11 and later versions support only JSON for the payload format.  
  
## Specifying Storage Service Versions in Requests  
 How you specify the version of the storage services to use for a request relates to how that request is authenticated. The following sections describe authentication options and how the service version is specified for each:  
  
1.  **Requests using Shared Key or Shared Key Lite.** To authenticate a request with Shared Key/Shared Key Lite, you must pass the `x-ms-version` header on the request. In the case of the Blob service, you can specify the default version for all requests by calling [Set Blob Service Properties](../StorageServicesREST/Set-Blob-Service-Properties.md).  
  
2.  **Requests using a Shared Access Signature (SAS).** You can specify two versioning options on a shared access signature. If specified, the   optional `api-version` header indicates which service version to use to execute the API operation. The `SignedVersion (sv)` parameter specifies the service version to use to authorize and authenticate the request made with the SAS. If the `api-version` header is not specified, then the value of the `SignedVersion (sv)` parameter also indicates the version to use to execute the API operation.  
  
3.  **Requests using anonymous access.** In the case of anonymous access against the Blob service, no version is passed in; the heuristics for which version is used for the request are described below.  
  
### Requests Authenticated Using Shared Key/Shared Key Lite  
 To authenticate a request with Shared Key/Shared Key Lite, specify the `x-ms-version` header on the request. The `x-ms-version` request header value must be specified in the format YYYY-MM-DD. For example:  
  
```  
Request Headers:  
x-ms-version: 2015-12-11  
```  
  
 The following rules indicates how requests using Shared Key/Shared Key Lite are evaluated to determine the version to use in processing the request.  
  
-   If a request has a valid `x-ms-version` header, the storage service uses the specified version. All requests to the Table and Queue services that do not use a shared access signature must specify an `x-ms-version` header. All requests to the Blob service that do not use a shared access signature must specify an `x-ms-version` header unless the default version has been set, as described below.  
  
-   If a request to the Blob service does not have an `x-ms-version` header, but the account owner has set a default version using [Set Blob Service Properties](../StorageServicesREST/Set-Blob-Service-Properties.md), then the specified default version is used as the version for the request.  
  
### Requests Authenticated With a Shared Access Signature  
 A shared access signature (SAS) generated using version 2014-02-14 or later supports two versioning options:  
  
-   The `api-version` query parameter defines the REST protocol version to use for processing a request made using the SAS.  
  
-   The `SignedVersion (sv)` query parameter defines the SAS version to use for authentication and authorization.  
  
 The `SignedVersion` query parameter is used for authentication and authorization when a client makes a request using the SAS. Authentication and authorization parameters such as `si`, `sr`, `sp`, `sig`, `st`, `se`, `tn`, `spk`, `srk`, `epk`, and `erk` are all interpreted using the specified version.  
  
 REST protocol parameters such as  `rscc`, `rscd`, `rsce`, `rscl`, and `rsct` are enforced using the version provided in the `api-version` parameter header. If the `api-version` header is not specified, then the service version provided for `SignedVersion` is used.  
  
 Note that the `api-version` parameter is not part of the string-to-sign in the authentication as described in [Constructing a Service SAS](../StorageServicesREST/Constructing-a-Service-SAS.md).  
  
 The following table explains the versioning scheme used by the service for authentication and authorization and for calling the REST protocol when the `SignedVersion` parameter is set to version 2014-02-14 or later.  
  
|Value of *api-version* parameter|Version used for authentication and authorization|Version used for protocol behavior|  
|---------------------------------------|-------------------------------------------------------|----------------------------------------|  
|Not specified|Version specified in the `sv` parameter|Version specified in the `sv` parameter|  
|Any valid storage services version in format `XXXX-XX-XX`|Version specified in the `sv` parameter|Valid storage services version `XXXX-XX-XX`|  
  
 **Example 1**  
  
 The following sample request calls [List Blobs](../StorageServicesREST/List-Blobs.md) with `sv=2015-04-05`, and without the `api-version` parameter.  
  
 `https://myaccount.blob.core.windows.net/mycontainer?restype=container&comp=list&sv=2015-04-05&si=readpolicy&sig=a39 %2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d`  
  
 In this case, the service authenticates and authorizes the request using version 2015-04-05 and also executes the operation using version 2015-04-05.  
  
 **Example 2**  
  
 The following sample request calls [List Blobs](../StorageServicesREST/List-Blobs.md) with `sv=2015-04-05` and with the `api-version` parameter.  
  
 `https://myaccount.blob.core.windows.net/mycontainer?restype=container&comp=list&sv=2015-04-05&si=readpolicy&sig=a39 %2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d&api-version=2012-02-12`  
  
 Here, the service authenticates and authorizes the request using version 2015-04-05 and executes the operation using version 2012-02-12.  
  
> [!NOTE]
>  The .NET Storage Client Library will always set the REST protocol version (in the `api-version` parameter) to the version that it is based on.  
  
### Requests Via Anonymous Access  
 If a request to the Blob service does not specify the `x-ms-version` header, and the default version for the service has not been set using [Set Blob Service Properties](../StorageServicesREST/Set-Blob-Service-Properties.md), then the earliest version of the Blob service is used to process the request. However, if the container was made public with a [Set Container ACL](../StorageServicesREST/Set-Container-ACL.md) operation performed using version 2009-09-19 or newer, then the request is processed using version 2009-09-19.  
  
## See Also  
 [Storage Services REST](../StorageServicesREST/Azure-Storage-Services-REST-API-Reference.md)   
 [Versioning Best Practices](../StorageServicesREST/Versioning-Best-Practices.md)   
 [Protocol Version Support for .NET Client Library Versions](../StorageServicesREST/Protocol-Version-Support-for-.NET-Client-Library-Versions.md)
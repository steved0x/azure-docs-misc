---
title: "Azure Storage Services Versions 2015-07-08 and Earlier"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 2279856c-ff44-4560-bfa5-b03ae644c0af
caps.latest.revision: 10
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
# Azure Storage Services Versions 2015-07-08 and Earlier
The Microsoft Azure storage services support multiple versions. To make a request against the storage services, you must specify the version that you want to use for that operation, unless the request is anonymous.  
  
## Available Versions  
 The current version of the Azure storage services is 2015-12-11, and using that version is recommended where possible. For information about the latest version, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).  
  
 Additional supported versions are listed below.  
  
-   [Version 2015-07-08](../StorageServicesREST/Version-2015-07-08.md)  
  
-   [Version 2015-04-05](../StorageServicesREST/Version-2015-04-05.md)  
  
-   [Version 2015-02-21](../StorageServicesREST/Version-2015-02-21.md)  
  
-   [Version 2014-02-14](../StorageServicesREST/Version-2014-02-14.md)  
  
-   [Version 2013-08-15](../StorageServicesREST/Version-2013-08-15.md)  
  
-   [Version 2012-02-12](../StorageServicesREST/Version-2012-02-12.md)  
  
-   [Version 2011-08-18](../StorageServicesREST/Version-2011-08-18.md)  
  
-   [Version 2009-09-19](../StorageServicesREST/Version-2009-09-19.md)  
  
-   [Version 2009-07-17](../StorageServicesREST/Version-2009-07-17.md)  
  
-   [Version 2009-04-14](../StorageServicesREST/Version-2009-04-14.md)  
  
## Requests Authenticated via a Shared Access Signature (SAS)  
 A request made via a SAS is processed according to which service version was used to generate the SAS. Versions 2013-08-15 and 2012-02-12 include a versioning parameter (`SignedVersion`, or `sv`), which specifies which version to use to authenticate and execute the SAS request.  
  
### Version 2012-02-12 and later  
 Requests with Shared Access Signatures (SAS) generated using version 2012-02-12 or later require the `SignedVersion (sv)` parameter. `SignedVersion` indicates the service version used for authentication and authorization and for calling the API operation. If the `x-ms-version` header is passed on the request, it is ignored; only the `SignedVersion (sv)` parameter determines the service version to use to process the request made via the SAS.  
  
> [!NOTE]
>  For version 2013-08-15 and earlier, code that prepares and distributes shared access signature URLs (*i.e.*, SAS providers or generators) should specify versions that are understood by client software (*i.e.*, SAS consumers) that makes storage service requests.  
  
 The following table indicates which services are supported for which version for a request made via a SAS:  
  
|Value of SignedVersion (sv) parameter|Supported services|  
|---------------------------------------------|------------------------|  
|2015-12-11|All (Blob, Queue, Table, File)|  
|2015-04-05|All (Blob, Queue, Table, File)|  
|2015-02-21|All (Blob, Queue, Table, File)|  
|2014-02-14|Blob, Queue, Table|  
|2013-08-15|Blob, Queue, Table|  
|2012-02-12|Blob, Queue, Table|  
  
 **Example**  
  
 The following example shows a SAS which calls [List Blobs](../StorageServicesREST/List-Blobs.md) using `sv=2013-08-15`.  
  
 `https://myaccount.blob.core.windows.net/mycontainer?restype=container&comp=list&sv=2013-08-15&si=readpolicy&sig=a39 %2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d`  
  
 In this example, the service will authenticate, authorize, and execute using version 2013-08-15. The response will not include the `Url` element under the `Blob` element, as it was removed in 2013-08-15 version.  
  
 If a client application using a version of the Storage Client Library based on version 2012-02-12 makes a request using this SAS, the client would expect the `Uri` element and so would fail with a `NullReferenceException`.  
  
### Versions Prior to 2012-02-12 (Blob Service Only)  
 The Blob service introduced shared access signatures in version 2009-07-17, while the Table and Queue services introduced shared access signatures in version 2012-02-12, so SAS behavior prior to version 2012-02-12 applies only to the Blob service. Version 2012-02-12 also introduced the `SignedVersion (sv)` parameter, which enables the SAS generator to specify the version to use to process the request. A SAS generated with a version prior to 2012-02-12 cannot specify the version to use to process the request and so relies on the rules outlined below.  
  
 In versions prior to 2012-02-12, the following rules are used to process the SAS request for authentication, authorization, and API execution:  
  
1.  If the SAS request against the Blob service has a valid `x-ms-version` header, the earliest valid version (2009-07-17) is used to interpret the SAS parameters, and the version specified by `x-ms-version` is used to perform the Blob service storage operation.  
  
2.  If the SAS request against the Blob service does not have an `x-ms-version` header and the owner has set the default version for this storage service type using [Set Blob Service Properties](../StorageServicesREST/Set-Blob-Service-Properties.md), version 2009-07-17 is used to interpret the SAS parameters and the owner-specified default version is used to perform the Blob service storage operation.  
  
3.  If the SAS request against the Blob service does not have an `x-ms-version` header and the owner has not set a default version, the Blob service uses the earliest valid version (2009-07-17) to interpret the SAS parameters. If the container is public and its access restrictions were set with a [Set Container ACL](../StorageServicesREST/Set-Container-ACL.md) operation that used version 2009-09-19 or newer, version 2009-09-19 is used to perform the Blob service operation.  
  
4.  If the SAS request against the Blob service does not have an `x-ms-version` header and the owner has not set a default version, the Blob service uses the earliest valid version (2009-07-17) to interpret the SAS parameters. If the container access restrictions were not set with a [Set Container ACL](../StorageServicesREST/Set-Container-ACL.md) operation that used version 2009-09-19 or newer, the Blob service operation is performed using the earliest version of the service.  
  
 The following table applies the above rules to various scenarios, and assumes the `SignedVersion` parameter is not included.  
  
||||  
|-|-|-|  
|**Value of x-ms-version header**|**Version used to interpret SAS parameters for authentication and authorization for Blob service**|**Version used to perform Blob service operation**|  
|None|Earliest valid SAS version (2009-07-17)|2009-09-19 is used if the container was set to public by [Set Container ACL](../StorageServicesREST/Set-Container-ACL.md) using version 2009-09-19 or newer; otherwise the earliest version of Blob service is used.|  
|2011-08-18|Earliest valid SAS version (2009-07-17)|2011-08-18.|  
|Any version XXXX-XX-XX|Earliest valid SAS version (2009-07-17)|Version XXXX-XX-XX|  
  
> [!NOTE]
>  We highly recommend using version 2011-08-18 version and later for scenarios that require quoted ETag values or valid `Accept-Ranges` response headers, since browsers and other streaming clients require these for efficient download and retries.  
  
## See Also  
 [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md)
---
title: "SAS Error Codes"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: c80e638f-b110-4f90-9209-fe7f204a407a
caps.latest.revision: 9
author: tamram
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
# SAS Error Codes
Beginning with version 2015-04-05, Azure Storage returns several new error codes for  shared access signatures (SAS).  
  
|Scenario|Storage Error Code|Old Http Status Code|New Http Status Code|Error Message|Applies To (SAS Type)|  
|--------------|------------------------|--------------------------|--------------------------|-------------------|-----------------------------|  
|Authorization of IP address or range failed|`AuthorizationSourceIPMismatch`|N/A|403 (Forbidden)|This request is not authorized to perform this operation using this source IP {SourceIP}.|Account SAS<br /><br /> Service SAS|  
|Authorization of HTTPS failed|`AuthorizationProtocolMismatch`|N/A|403 (Forbidden)|This request is not authorized to perform this operation using this protocol.|Account SAS<br /><br /> Service SAS|  
|Unauthorized signed permission (including create and add permissions)|`AuthorizationPermissionMismatch`|404 (Not Found)|403 (Forbidden)|This request is not authorized to perform this operation using this permission.|Account SAS<br /><br /> Service SAS|  
|Unauthorized signed service|`AuthorizationServiceMismatch`|N/A|403 (Forbidden)|This request is not authorized to perform this operation using this service.|Account SAS<br /><br /> Service SAS|  
|Unauthorized signed resource type|`AuthorizationResourceTypeMismatch`|N/A|403 (Forbidden)|This request is not authorized to perform this operation using this resource type.|Account SAS<br /><br /> Service SAS|  
|Other authorization errors (for example, attempting  to modify an ACL or calling another unsupported SAS API)|`AuthorizationFailure`|404 (Not Found)|403 (Forbidden)|This request is not authorized to perform this operation.|Account SAS<br /><br /> Service SAS|  
|Stored access policy for file or blob relies on Create or Add permission, and Get ACL is called using a version prior to 2015-04-05|`FeatureVersionMismatch`|N/A|409 (Conflict)|Stored access policy contains a permission that is not supported by this version.|Service SAS|  
  
## See Also  
 [Delegating Access with a Shared Access Signature](../StorageServicesREST/Delegating-Access-with-a-Shared-Access-Signature.md)   
 [Constructing a Service SAS](../StorageServicesREST/Constructing-a-Service-SAS.md)
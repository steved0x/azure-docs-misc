---
title: "API Management authentication policies"
ms.custom: na
ms.date: 2015-12-02
ms.prod: azure
ms.reviewer: na
ms.service: api-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
caps.latest.revision: 6
author: steved0x
manager: douge
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
# API Management authentication policies
This topic provides a reference for the following API Management policies. For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AuthenticationPolicies"></a> Authentication policies  
  
-   [Authenticate with Basic](../templates/API-Management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.  
  
-   [Authenticate with client certificate](../templates/API-Management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.  
  
##  <a name="Basic"></a> Authenticate with Basic  
 Use the `authentication-basic` policy to authenticate with a backend service using Basic authentication. This policy effectively sets the HTTP Authorization header to the value corresponding to the credentials provided in the policy.  
  
### Policy statement  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### Example  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### Elements  
  
|Name|Description|Required|  
|----------|-----------------|--------------|  
|authentication-basic|Root element.|Yes|  
  
### Attributes  
  
|Name|Description|Required|Default|  
|----------|-----------------|--------------|-------------|  
|username|Specifies the username of the Basic credential.|Yes|N/A|  
|password|Specifies the password of the Basic credential.|Yes|N/A|  
  
### Usage  
 This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Policy sections:** inbound  
  
-   **Policy scopes:** API  
  
##  <a name="ClientCertificate"></a> Authenticate with client certificate  
 Use the `authentication-certificate` policy to authenticate with a backend service using client certificate. The certificate needs to be [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.  
  
### Policy statement  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### Example  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### Elements  
  
|Name|Description|Required|  
|----------|-----------------|--------------|  
|authentication-certificate|Root element.|Yes|  
  
### Attributes  
  
|Name|Description|Required|Default|  
|----------|-----------------|--------------|-------------|  
|thumbprint|The thumbprint for the client certificate.|Yes|N/A|  
  
### Usage  
 This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Policy sections:** inbound  
  
-   **Policy scopes:** API  
  
## See Also  
 [Policy reference](../templates/API-Management-policy-reference.md)
---
title: "Saved document snippets"
ms.custom: na
ms.date: 09/29/2016
ms.reviewer: na
ms.service: api-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 3470f97a-f707-40f8-b184-5253e32ea14b
caps.latest.revision: 11
author: steved0x
manager: dwrede
---
# Saved document snippets
Saved stuff that isn't ready for publishing yet.  
  
##  <a name="AdvancedPolicies"></a> Advanced policies - published but left here as a template  
  
-   [Wait](#Wait) - Waits for enclosed [Send request](../templates/API-Management-advanced-policies.md#SendRequest), [Get value from cache](../templates/API-Management-caching-policies.md#GetFromCacheByKey), or [Control flow](../templates/API-Management-advanced-policies.md#choose) policies to complete before proceeding.  
  
##  <a name="Wait"></a> Wait  
 The `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies to complete before it completes. The wait policy can have as its immediate child policies [Send request](../templates/API-Management-advanced-policies.md#SendRequest), [Get value from cache](../templates/API-Management-caching-policies.md#GetFromCacheByKey), and [Control flow](../templates/API-Management-advanced-policies.md#choose) policies.  
  
### Policy statement  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### Example  
 In the following example there are two `choose` policies as immediate child policies of the `wait` policy. Each of these `choose` policies executes in parallel. Each `choose` policy attempts to retrieve a cached value. If there is a cache miss, a backend service is called to provide the value. In this example the `wait` policy does not complete until all of its immediate child policies complete, because the `for` attribute is set to `all`.  
  
```xml  
<wait for="all">  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-one="])">  
      <cache-lookup-value key="key-one" variable-name="value-one" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-one="))">  
          <send-request mode="new" response-variable-name="value-one">  
            <set-url>https://backend-one</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-two="])">  
      <cache-lookup-value key="key-two" variable-name="value-two" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-two="))">  
          <send-request mode="new" response-variable-name="value-two">  
            <set-url>https://backend-two</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
</wait>  
  
```  
  
### Elements  
  
|Element|Description|Required|  
|-------------|-----------------|--------------|  
|wait|Root element. May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.|Yes|  
  
### Attributes  
  
|Attribute|Description|Required|Default|  
|---------------|-----------------|--------------|-------------|  
|for|Determines whether the `wait` policy waits for all immediate child policies to be completed or just one.|No|all|  
  
### Usage  
 This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Policy sections:** inbound, outbound  
  
-   **Policy scopes:** all scopes
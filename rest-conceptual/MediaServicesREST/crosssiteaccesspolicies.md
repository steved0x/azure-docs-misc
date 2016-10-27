---
title: "CrossSiteAccessPolicies"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 92b02bbc-cf26-46c7-ae43-00d62ae21705
caps.latest.revision: 5
author: "Juliako"
ms.author: "juliako"
manager: "erikre"
translation.priority.mt: 
  - "de-de"
  - "es-es"
  - "fr-fr"
  - "it-it"
  - "ja-jp"
  - "ko-kr"
  - "pt-br"
  - "ru-ru"
  - "zh-cn"
  - "zh-tw"
---
# CrossSiteAccessPolicies
Used by the [StreamingEndpoint](../MediaServicesREST/streamingendpoint.md) and [Channel](../MediaServicesREST/channel.md) entities to specify cross site access policies for various clients.  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`ClientAccessPolicy`<br /><br /> Optional.|Edm.String|Use this property to specify the client access policy for Microsoft Silverlight clients.<br /><br /> The following example defines clientaccesspolicy xml.<br /><br /> `<?xml version="1.0" encoding="utf-8"?> <access-policy>   <cross-domain-access>     <policy>       <allow-from http-request-headers='*'>         <domain uri='http://*' />       </allow-from>       <grant-to>         <resource path='/' include-subpaths='false' />       </grant-to>     </policy>   </cross-domain-access> </access-policy>`|  
|`CrossDomainPolicy`<br /><br /> Optional.|Edm.String|Use this property to specify the cross domain access policy for Adobe Flash clients.<br /><br /> The following example defines crossdomain xml.<br /><br /> `<?xml version="1.0" ?> <!DOCTYPE cross-domain-policy SYSTEM 'http://www.macromedia.com/xml/dtds/cross-domain-policy.dtd'> <cross-domain-policy>   <allow-access-from domain='*' /> </cross-domain-policy>`|
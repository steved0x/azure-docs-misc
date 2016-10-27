---
title: "Azure Media Services REST API Reference"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 784dd5de-172d-4bf3-94e6-eb4499f51a82
caps.latest.revision: 23
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
# Azure Media Services REST API Reference
The Microsoft Azure Media Services REST API reference section describes the entities and functions that are used when creating, processing, managing, and delivering Assets.  
  
 The table below shows Media Services REST API versions. It also shows major modifications that were made in each version. To examine Media Services entities, entity properties, associations, functions, and so on, paste the following URI in a browser: https://media.windows.net/API/$metadata?api-version=2.x (where x is a version number).  
  
|x-ms-version|Description|  
|--------------------|-----------------|  
|2.13||  
|2.12|The following new types/properties were added:<br /><br /> FirstQuality<br /><br /> AssetFilter.FirstQuality<br /><br /> Filter.FirstQuality|  
|2.11|The following new entities were added:<br /><br /> [AssetFilter](../MediaServicesREST/assetfilter.md)<br /><br /> [Filter](../MediaServicesREST/filter.md)<br /><br /> [FilterTrackSelect](../MediaServicesREST/filtertrackselect.md)<br /><br /> [PresentationTimeRange](../MediaServicesREST/presentationtimerange.md)|  
|2.10|The following [Channel](../MediaServicesREST/channel.md)’s properties were added to support live encoding with Media Services:<br /><br /> `EncodingType`<br /><br /> `Encoding`<br /><br /> `Slate`<br /><br /> You can also signal to start and end advertisement and hide and how a slate image.|  
|2.9|The `CdnEnabled` property was added to [StreamingEndpoint](../MediaServicesREST/streamingendpoint.md).|  
|2.8|The following new entity was added: [EncodingReservedUnitType](../MediaServicesREST/encodingreservedunittype.md).|  
|2.7|Breaking change: [Origin](../MediaServicesREST/origin1.md) was renamed to [StreamingEndpoint](../MediaServicesREST/streamingendpoint.md). For more details, see [StreamingEndpoint](../MediaServicesREST/streamingendpoint.md).<br /><br /> Updated properties: [Asset](../MediaServicesREST/asset.md).<br /><br /> DeliveryPolicies.<br /><br /> New entities, complex types, and properties:<br /><br /> [AkamaiAccessControl](../MediaServicesREST/streamingendpoint.md#AkamaiAccessControl)<br /><br /> [AkamaiSignatureHeaderAuthenticationKey](../MediaServicesREST/streamingendpoint.md#AkamaiSignatureHeaderAuthenticationKey)<br /><br /> [AssetDeliveryPolicy](../MediaServicesREST/assetdeliverypolicy.md)<br /><br /> [Channel](../MediaServicesREST/channel.md)<br /><br /> [ChannelInput ComplexType](../MediaServicesREST/channel.md#ChannelInput)<br /><br /> [ChannelInputAccessControl ComplexType](../MediaServicesREST/channel.md#ChannelInputAccessControl)<br /><br /> [ChannelEndpoint ComplexType](../MediaServicesREST/channel.md#ChannelEndpoint)<br /><br /> [ChannelOutput ComplexType](../MediaServicesREST/channel.md#ChannelOutput)<br /><br /> [ChannelOutputHls ComplexType](../MediaServicesREST/channel.md#ChannelOutputHls)<br /><br /> [ChannelPreview ComplexType](../MediaServicesREST/channel.md#ChannelPreview)<br /><br /> [ChannelPreviewAccessControl ComplexType](../MediaServicesREST/channel.md#ChannelPreviewAccessControl)<br /><br /> [ContentKeyAuthorizationPolicy](../MediaServicesREST/contentkeyauthorizationpolicy.md)<br /><br /> [ContentKeyAuthorizationPolicyOption](../MediaServicesREST/contentkeyauthorizationpolicyoption.md)<br /><br /> [ContentKeyAuthorizationPolicyRestriction ComplexType Properties](../MediaServicesREST/contentkeyauthorizationpolicyoption.md#restrions)<br /><br /> [CrossSiteAccessPolicies](../MediaServicesREST/crosssiteaccesspolicies.md)<br /><br /> `IPAccessControl`. See [IPAccessControl](../MediaServicesREST/channel.md#IPAccessControl) and [StreamingEndpoint](../MediaServicesREST/streamingendpoint.md#IPAccessControl).<br /><br /> `IPRange`. See [IPRange ComplexType](../MediaServicesREST/channel.md#IPRange) and [StreamingEndpoint](../MediaServicesREST/streamingendpoint.md#IPRange).<br /><br /> [Program](../MediaServicesREST/program.md)<br /><br /> [StreamingEndpointAccessControl](../MediaServicesREST/streamingendpoint.md#StreamingEndpointAccessControl)<br /><br /> [StreamingEndpointCacheControl](../MediaServicesREST/streamingendpoint.md#StreamingEndpointCacheControl)|  
|2.6|Current.<br /><br /> No model updates.|  
|2.5|The `BytesUsed` property was added to [StorageAccount](../MediaServicesREST/storageaccount.md).|  
|2.4|No model updates.|  
|2.3|The `AuthorizationPolicyId` property was added to [ContentKey](../MediaServicesREST/contentkey.md).|  
|2.2|The following new entries were added to the model:<br /><br /> [Origin](../MediaServicesREST/origin1.md)<br /><br /> [StorageAccount](../MediaServicesREST/storageaccount.md)<br /><br /> [Operation](../MediaServicesREST/operation.md)<br /><br /> The following new properties were added to entities:<br /><br /> [Asset](../MediaServicesREST/asset.md): Uri, StorageAccountName, and StorageAccount.<br /><br /> [Locator](../MediaServicesREST/locator.md): Name.<br /><br /> [IngestManifest](../MediaServicesREST/ingestmanifest.md): StorageAccountName and StorageAccount.|  
|2.1|The following new entries were added to the model:<br /><br /> [NotificationEndPoint](../MediaServicesREST/notificationendpoint.md)<br /><br /> [JobNotificationSubscription](../MediaServicesREST/jobnotificationsubscription.md)|  
|2.0|Initial public release.|  
  
## In This Section  
 [AccessPolicy](../MediaServicesREST/accesspolicy.md)  
  
 [AssetDeliveryPolicy](../MediaServicesREST/assetdeliverypolicy.md)  
  
 [AssetFile](../MediaServicesREST/assetfile.md)  
  
 [Asset](../MediaServicesREST/asset.md)  
  
 [Channel](../MediaServicesREST/channel.md)  
  
 [ContentKey](../MediaServicesREST/contentkey.md)  
  
 [ContentKeyAuthorizationPolicy](../MediaServicesREST/contentkeyauthorizationpolicy.md)  
  
 [ContentKeyAuthorizationPolicyOption](../MediaServicesREST/contentkeyauthorizationpolicyoption.md)  
  
 [CrossSiteAccessPolicies](../MediaServicesREST/crosssiteaccesspolicies.md)  
  
 [ErrorDetail](../MediaServicesREST/errordetail.md)  
  
 [IngestManifest](../MediaServicesREST/ingestmanifest.md)  
  
 [IngestManifestAsset](../MediaServicesREST/ingestmanifestasset.md)  
  
 [IngestManifestFile](../MediaServicesREST/ingestmanifestfile.md)  
  
 [IngestManifestStatistics](../MediaServicesREST/ingestmanifeststatistics.md)  
  
 [Job](../MediaServicesREST/job.md)  
  
 [JobTemplate](../MediaServicesREST/jobtemplate.md)  
  
 [Locator](../MediaServicesREST/locator.md)  
  
 [MediaProcessor](../MediaServicesREST/mediaprocessor.md)  
  
 [NotificationEndPoint](../MediaServicesREST/notificationendpoint.md)  
  
 [Operation](../MediaServicesREST/operation.md)  
  
 [Program](../MediaServicesREST/program.md)  
  
 [StorageAccount](../MediaServicesREST/storageaccount.md)  
  
 [StreamingEndpoint](../MediaServicesREST/streamingendpoint.md)  
  
 [Task](../MediaServicesREST/task.md)  
  
 [TaskHistoricalEvent](../MediaServicesREST/taskhistoricalevent.md)  
  
 [TaskTemplate](../MediaServicesREST/tasktemplate.md)  
  
 [REST API Functions](../MediaServicesREST/rest-api-functions.md)  
  
## Reference  
  
## Related Sections
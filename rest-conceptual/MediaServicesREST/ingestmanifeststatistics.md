---
title: "IngestManifestStatistics"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: e2054edb-7d95-41b7-834c-2fe5846f2666
caps.latest.revision: 6
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
# IngestManifestStatistics
IngestManifestStatistics is a complex type provided by the **Statistics** property of an [IngestManifest](../MediaServicesREST/ingestmanifest.md). IngestManifestStatistics are used to determine the progress of bulk ingesting operations for an IngestManifest. For more information on bulk ingesting, see [Ingesting Assets in Bulk with the REST API](http://msdn.microsoft.com/en-us/3caa81ea-c840-4265-b8fa-f958cdde12b6).  
  
## IngestManifestStatistics Entity Properties  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`PendingFilesCount`<br /><br /> Read-only. Set by Media Services.|Edm.Int32|This value specifies the count of files currently pending upload for IngestManifestAssets contained in an IngestManifest.|  
|`FinishedFilesCount`<br /><br /> Read-only. Set by Media Services.|Edm.Int32|This value specifies the count of how many files have already been uploaded and successfully processed for respective IngestManifestAssets contained in an IngestManifest.|  
|`ErrorFilesCount`<br /><br /> Read-only. Set by Media Services.|Edm.Int32|This value specifies the count how many files have encountered an error during processing.|  
|`ErrorFilesDetails`<br /><br /> Read-only. Set by Media Services.|Edm.String|This value provides error details for errors encountered processing assets files.|  
  
## See Also  
 [IngestManifest](../MediaServicesREST/ingestmanifest.md)   
 [IngestManifestAsset](../MediaServicesREST/ingestmanifestasset.md)   
 [IngestManifestFile](../MediaServicesREST/ingestmanifestfile.md)
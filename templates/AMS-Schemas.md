---
title: "AMS Schemas"
ms.custom: na
ms.date: 2016-07-13
ms.prod: azure
ms.reviewer: na
ms.service: media-services
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1122fbb4-4d0e-4027-9a4c-c1833697fa13
caps.latest.revision: 15
author: juliako
manager: erikre
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
# AMS Schemas
Topics in this section discuss a few Media Services encoder XML schemas:  Preset schemas, Input and Output metadata schemas.  
  
 In Media Services, an `Asset` contains digital files (including video, audio, images, thumbnail collections, text tracks and closed caption files) and the metadata about these files. After digital files are uploaded into an asset, they could be used in the Media Services encoding and streaming workflows. When you encode an asset, an output asset is produced upon completion of the encoding job. Among other files, the output asset contains XML metadata files that describe the input asset and the output asset.  These XML files conform to schemas described in the [Input Metadata](../templates/Input-Metadata.md) and [Output Metadata](../templates/Output-Metadata.md) topics.  
  
 Media Services defines a set of encoding presets you can use when creating encoding jobs with `Media Encoder Standard`. You should use one of the presets described in the [Task Presets for MES (Media Encoder Standard)](../templates/Task-Presets-for-MES--Media-Encoder-Standard-.md) topic.
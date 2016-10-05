---
title: "Task Preset for Azure Media Indexer"
ms.custom: na
ms.date: 2016-07-13
ms.prod: azure
ms.reviewer: na
ms.service: media-services
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b3cfe35-f4d6-4123-810c-a4b9dfef75b7
caps.latest.revision: 12
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
# Task Preset for Azure Media Indexer
Azure Media Indexer is a Media Processor that you use to perform the following tasks: make media files and content searchable, generate closed captioning tracks and keywords, index asset files that are part of your asset.  
  
 This topic describes the task preset that you need to pass to your indexing job.  For complete example, see [Indexing Media Files with Azure Media Indexer](http://azure.microsoft.com/documentation/articles/media-services-index-content/).  
  
## Azure Media Indexer Configuration XML  
 The following table explains elements and attributes of the configuration XML.  
  
|Name|Require|Description|  
|----------|-------------|-----------------|  
|`Input`|true|Asset file(s) that you want to index.<br /><br /> Azure Media Indexer supports the following media file formats: MP4, WMV, MP3, M4A, WMA, AAC, WAV.<br /><br /> You can specify the file name (s) in the `name` or `list` attribute of the `input` element (as shown below).If you do not specify which asset file to index, the primary file is picked. If no primary asset file is set, the first file in the input asset is indexed.<br /><br /> To explicitly specify the asset file name, do:<br /><br /> `<input name="TestFile.wmv" />`<br /><br /> You can also index multiple asset files at once (up to 10 files). To do this:<br /><br /> - Create a text file (manifest file) and give it an .lst extension.<br /><br /> - Add a list of all the asset file names in your input asset to this manifest file.<br /><br /> - Add (upload) thanifest file to the asset.<br /><br /> - Specify the name of the manifest file in the input’s list attribute.<br /><br /> `<input list="input.lst">`<br /><br /> **Note:** If you add more than 10 files to the manifest file, the indexing job will fail with the 2006 error code.|  
|`metadata`|false|Metadata for the specified asset file(s).<br /><br /> `<metadata key="..." value="..." />`<br /><br /> You can supply `value`s for predefined `key`s. Currently the following keys are supported:<br /><br /> “title” and “description” -  used to update the language model to improve speech recognition accuracy.<br /><br /> `<metadata key="title" value="[Title of the media file]" /><metadata key="description" value="[Description of the media file]" />`<br /><br /> “username” and “password” - used for authentication when downloading internet files via http or https.<br /><br /> `<metadata key="username" value="[UserName]" /><metadata key="password" value="[Password]" />`<br /><br /> The username and password values apply to all media URLs in the input manifest.|  
|`features`<br /><br /> Added in version 1.2. Currently, the only supported feature is speech recognition ("ASR").|False|The Speech Recognition feature has the following settings keys:<br /><br /> Language:<br /><br /> - The natural language to be recognized in the multimedia file.<br /><br /> - English, Spanish<br /><br /> CaptionFormats:<br /><br /> - a semicolon-separated list of the desired output caption formats (if any)<br /><br /> - ttml;sami;webvtt<br /><br /> GenerateAIB:<br /><br /> - A boolean flag specifying whether or not an AIB file is required (for use with SQL Server and the customer Indexer IFilter).  For more information, see [Using AIB Files with Azure Media Indexer and SQL Server](http://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/).<br /><br /> - True; False<br /><br /> GenerateKeywords:<br /><br /> - A boolean flag specifying whether or not a keyword XML file is required.<br /><br /> - True; False.|  
  
 The following example shows the Azure Media Indexer configuration XML.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<configuration version="2.0">  
  <input>  
    <metadata key="title" value="[Title of the media file]" />  
    <metadata key="description" value="[Description of the media file]" />  
  </input>  
  <settings>  
  </settings>  
  
  <features>  
    <feature name="ASR">    
      <settings>  
        <add key="Language" value="English"/>  
        <add key="CaptionFormats" value="ttml;sami;webvtt"/>  
        <add key="GenerateAIB" value ="true" />  
        <add key="GenerateKeywords" value ="true" />  
      </settings>  
    </feature>  
  </features>  
  
</configuration>  
  
```
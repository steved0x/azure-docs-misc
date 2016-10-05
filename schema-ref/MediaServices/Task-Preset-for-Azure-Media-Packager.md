---
title: "Task Preset for Azure Media Packager"
ms.custom: na
ms.date: 2016-07-13
ms.prod: azure
ms.reviewer: na
ms.service: media-services
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dce6f107-012c-4773-9e68-a1b584c508df
caps.latest.revision: 30
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
# Task Preset for Azure Media Packager
> [!NOTE]
>  The end of life date for Windows Azure Media Packager and Windows Azure Media Encryptor has been extended to March 1, 2017. Before that date, the functionalities of these processors will be added to Media Encoder Standard (MES). Customers will be provided with instructions on how to migrate their workflows to send Jobs to MES. Format conversion and encryption capabilities may also be available through dynamic packaging and dynamic encryption.  
  
 This topic contains templated XML configuration files for running Microsoft Azure Media Services tasks using the Windows Azure Media Packager media processor. These configuration files could be referenced as a configuration preset when performing one of the following tasks:  
  
-   [Convert MP4 Content to Smooth Streams](#MP4ToSmooth),  
  
-   [Convert Smooth Streams to Apple HTTP Live Streams](#SmoothToHLS),  
  
-   [Validate an Asset that Contains Multi-bitrate Smooth Streaming or MP4 Files](#ValidateMP4).  
  
## Azure Media Packager Preset  
  
###  <a name="MP4ToSmooth"></a> Convert MP4 Content to Smooth Streams  
 The following configuration xml converts MP4 files encoded with H.264 (AVC) video and AAC-LC audio codecs to Smooth Streams. Copy the following xml into a file and name the file `MediaPackager_MP4ToSmooth.xml`.  
  
 You can reference this file as a configuration preset when you convert MP4 content to smooth streaming content.  
  
```  
<taskDefinition xmlns="http://schemas.microsoft.com/iis/media/v4/TM/TaskDefinition#">  
  <name>MP4 to Smooth Streams</name>  
  <id>5e1e1a1c-bba6-11df-8991-0019d1916af0</id>  
  <description xml:lang="en" />  
  <inputFolder />  
  <properties namespace="http://schemas.microsoft.com/iis/media/V4/TM/MP4ToSmooth#" prefix="mp4">  
    <property name="keepSourceNames" value="false" />  
  </properties>  
  <taskCode>  
    <type>Microsoft.Web.Media.TransformManager.MP4toSmooth.MP4toSmooth_Task, Microsoft.Web.Media.TransformManager.MP4toSmooth, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35</type>  
  </taskCode>  
</taskDefinition>  
```  
  
 The following table explains the properties of the `MP4 to Smooth Streams` xml:  
  
|Name|Required|Description|  
|----------|--------------|-----------------|  
|keepSourceNames|false|This property tells the MP4 to Smooth task to keep the original file name rather than add the bitrate information.|  
  
 The `PackageMP4ToSmoothStreamingTask` method defined in the [this](http://azure.microsoft.com/documentation/articles/media-services-static-packaging/) topic shows how to use the Azure Media Packager media processor to convert MP4s to Smooth Streaming.  
  
###  <a name="SmoothToHLS"></a> Convert Smooth Streams to Apple HTTP Live Streams  
 Azure Media Services only supports converting from Smooth Streaming to HLS, you cannot encode to or convert from any other formats to HLS.  
  
 The following configuration xml converts Smooth Streams encoded with H.264 (AVC) video and AAC-LC audio codecs to Apple HTTP Live Streams (MPEG-2 TS) and creates an Apple HTTP Live Streaming playlist (.m3u8) file for the converted presentation.  
  
> [!IMPORTANT]
>  To convert to Apple HTTP Live Streaming, Smooth Streaming video tracks must contain only H.264 (AVC) video. VC-1 is not supported. Smooth Streaming audio tracks must contain only AAC-LC or HE-AAC audio codecs. Dolby DD+ is not supported for conversion to Apple HTTP Live Streams.  
  
 Copy the following xml into a file and name the file `MediaPackager_SmoothToHLS.xml`. You can reference this file as a configuration preset when you convert Smooth Streaming content to Apple HLS format.  
  
```  
 <taskDefinition xmlns="http://schemas.microsoft.com/iis/media/v4/TM/TaskDefinition#">  
    <name>Smooth Streams to Apple HTTP Live Streams</name>  
    <id>A72D7A5D-3022-45f2-89B4-1DDC5457C111</id>  
    <description xml:lang="en" />  
    <inputFolder />  
    <outputFolder>TS_Out</outputFolder>  
    <properties namespace="http://schemas.microsoft.com/iis/media/AppleHTTP#" prefix="hls">  
        <property name="maxbitrate" value="6600000" />  
        <property name="manifest" value="" />  
        <property name="segment" value="10" />  
        <property name="log" value="" />  
        <property name="encrypt" value="false" />  
        <property name="pid" value="" />  
        <property name="codecs" value="false" />  
        <property name="backwardcompatible" value="false" />  
        <property name="allowcaching" value="true" />  
        <property name="key" value="" />  
        <property name="keyuri" value="" />  
        <property name="overwrite" value="true" />  
    </properties>  
    <taskCode>  
        <type>Microsoft.Web.Media.TransformManager.SmoothToHLS.SmoothToHLSTask, Microsoft.Web.Media.TransformManager.SmoothToHLS, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35</type>  
    </taskCode>  
</taskDefinition>  
```  
  
> [!NOTE]
>  If you want for the HLS to get encrypted with AES make sure to set the `encrypt` property to `true`, set the `key` value, and the `keyuri` value for your authentication\authorization server.  
>   
>  Media Services will create a key file and place it in the asset container. You should copy the `/asset-containerguid/*.key` file to your server (or create your own key file) and then delete the *.key file from the asset container. For more information, see [Using Static Encryption to Protect HLSv3 with AES-128](assetId:///e990c745-7b08-4810-8331-488870f2393e).  
  
 The following table explains the properties of the `Smooth Streams to Apple HTTP Live Streams` xml:  
  
|Name|Required|Description|  
|----------|--------------|-----------------|  
|maxbitrate|true|The maximum bit rate, in bits per second (bps), to be converted to MPEG-2 TS. On-demand Smooth Streams at or below this value are converted to MPEG-2 TS segments. Smooth Streams above this value are not converted. Most Apple devices can play media encoded at bit rates up to 6,600 Kbps.|  
|manifest|false|The file name to use for the converted Apple HTTP Live Streaming playlist file (a file with an .m3u8 file name extension). If no value is specified, the following default value is used: &lt;ISM_file_name&gt;-m3u8-aapl.m3u8|  
|segment|false|The duration of each MPEG-2 TS segment, in seconds. 10 seconds is the Apple-recommended setting for most Apple mobile digital devices.|  
|log|false|The file name to use for a log file (with a .log file name extension) that records the conversion activity. If you specify a log file name, the file is stored in the task output folder.|  
|encrypt|false|Enables encryption of MPEG-2 TS segments by using the Advanced Encryption Standard (AES) with a 128-bit key (AES-128).|  
|pid|false|The program ID of the MPEG-2 TS presentation. Different encodings of MPEG-2 TS streams in the same presentation use the same program ID so that clients can easily switch between bit rates.|  
|codecs|false|Enables codec format identifiers, as defined by RFC 4281, to be included in the Apple HTTP Live Streaming playlist (.m3u8) file.|  
|backwardcompatible|false|Enables playback of the MPEG-2 TS presentation on devices that use the Apple iOS 3.0 mobile operating system.|  
|allowcaching|false|Enables the MPEG-2 TS segments to be cached on Apple devices for later playback.|  
|key|false|The hexadecimal representation of the 16-octet content key value that is used for encryption.|  
|keyuri|false|An alternate URI to be used by clients for downloading the key file. If no value is specified, it is assumed that the Live Smooth Streaming publishing point provides the key file.|  
|overwrite|false|Enables existing files in the output folder to be overwritten if converted output files have identical file names.|  
  
 [This](http://azure.microsoft.com/documentation/articles/media-services-static-packaging/) topic shows how to use the Azure Media Packager media processor to convert Smooth Streaming to HLS.  
  
###  <a name="ValidateMP4"></a> Validate an Asset that Contains Multi-bitrate Smooth Streaming or MP4 Files  
 The following configuration xml prepares MP4 asset for dynamic packaging. Copy the following xml into a file and name the file `MediaPackager_ValidateTask.xml`.  
  
 You can reference this file as a configuration preset for a task that checks whether an asset that contains a set of existing adaptive bitrate files can be converted to Smooth Streaming or Apple HLS format. You would use this preset when working with dynamic packaging..  
  
```  
<taskDefinition xmlns="http://schemas.microsoft.com/iis/media/v4/TM/TaskDefinition#">  
    <name>MP4 Preprocessor</name>  
    <id>859515BF-9BA3-4BDD-A3B6-400CEF07F870</id>  
    <description xml:lang="en" />  
    <inputFolder />  
    <properties namespace="http://schemas.microsoft.com/iis/media/V4/TM/MP4Preprocessor#" prefix="mp4p">  
    <property name="SmoothRequired" value="true" />  
    <property name="HLSRequired" value="true" />  
    </properties>  
    <taskCode>  
  <type>Microsoft.Web.Media.TransformManager.MP4PreProcessor.MP4Preprocessor_Task, Microsoft.Web.Media.TransformManager.MP4Preprocessor, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35</type>  
    </taskCode>  
</taskDefinition>  
  
```  
  
 The following table explains the properties of the `MP4 Preprocessor` xml:  
  
|Name|Required|Description|  
|----------|--------------|-----------------|  
|SmoothRequired|false|If the value property is set to true, the pre-processor task will check whether or not the specified content can be converted to Smooth Streaming format. If the content cannot be converted successfully, the pre-processor validation task will fail. This indicates that the On-Demand Streaming server will also fail to convert this content to Smooth Streaming.|  
|HLSRequired|false|If the value property is set to true, the pre-processor task will check whether or not the specified content can be converted to HLS format. If the content cannot be converted successfully, the pre-processor validation task will fail. This indicates that the On-Demand Streaming server will also fail to convert this content to HLS.|
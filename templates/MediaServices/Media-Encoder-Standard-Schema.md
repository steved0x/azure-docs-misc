---
title: "Media Encoder Standard Schema"
ms.custom: na
ms.date: 2016-07-12
ms.prod: azure
ms.reviewer: na
ms.service: media-services
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e9567d03-c379-42f1-ae7a-8198c3ddf5e6
caps.latest.revision: 33
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
# Media Encoder Standard Schema
This topic describes some of the elements and types of the XML schema on which [Media Encoder Standard presets](../MediaServices/Task-Presets-for-MES--Media-Encoder-Standard-.md) are based. The topic gives explanation of elements and their valid values. The full schema will be published at a later date.  
  
##  <a name="Preset"></a> Preset (root element)  
 Defines an encoding preset.  
  
### Elements  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Encoding`|[Encoding](#Encoding)|Root element, indicates that the input sources are to be encoded.|  
|`Outputs`|[Outputs](#Output)|Collection of desired output files.|  
  
### Attributes  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Version`<br /><br /> Required|`xs:decimal`|The preset version. The following restrictions apply: xs:fractionDigits value="1"  and xs:minInclusive value="1" For example, `version="1.0"`.|  
  
##  <a name="Encoding"></a> Encoding  
 Contains a sequence of the following elements.  
  
### Elements  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`H264Video`|[H264Video](#H264Video)|Settings for H.264 encoding of video.|  
|`AACAudio`|[AACAudio](#AACAudio)|Settings for AAC encoding of audio.|  
|`BmpImage`|[BmpImage](#BmpImage)|Settings for Bmp image.|  
|`PngImage`|[PngImage](#PngImage)|Settings for Png image.|  
|`JpgImage`|[JpgImage](#JpgImage)|Settings for Jpg image.|  
  
##  <a name="H264Video"></a> H264Video  
  
### Elements  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`TwoPass`<br /><br /> minOccurs="0"|`xs:boolean`|Currently, only one-pass encoding is supported.|  
|`KeyFrameInterval`<br /><br /> minOccurs="0"<br /><br /> `default="00:00:02"`|`xs:time`|Determines the (default) spacing between IDR frames .|  
|`SceneChangeDetection`<br /><br /> minOccurs="0"<br /><br /> default=”false”|`xs:boolean`|If set to true, encoder attempts to detect scene change in the video and inserts an IDR frame.|  
|`Complexity`<br /><br /> minOccurs="0"<br /><br /> default="Balanced"|`xs:string`|Controls the trade-off between encode speed and video quality. Could be one of the following values: `Speed`, `Balanced`, or `Quality`<br /><br /> Default: `Balanced`|  
|`SyncMode`<br /><br /> minOccurs="0"||Feature will be exposed in a future releases.|  
|`H264Layers`<br /><br /> minOccurs="0"|[H264Layers](#H264Layers)|Collection of output video layers.|  
  
##  <a name="H264Layers"></a> H264Layers  
  
### Elements  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`H264Layer`<br /><br /> minOccurs="0" maxOccurs="unbounded"|[H264Layer](#H264Layer)|A collection of H264 layers.|  
  
##  <a name="H264Layer"></a> H264Layer  
  
> [!NOTE]
>  Video limits are based on the values described in the [H264 Levels](https://en.wikipedia.org/wiki/H.264/MPEG-4_AVC#Levels) table.  
  
### Elements  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Profile`<br /><br /> minOccurs="0"<br /><br /> default=”Auto”|`xs:string`|Could be of one of the following `xs:string` values: `Auto`, `Baseline`, `Main`, `High`.|  
|`Level`<br /><br /> minOccurs="0"<br /><br /> default=”Auto”|`xs:string`||  
|`Bitrate`<br /><br /> minOccurs="0"|`xs:int`|The bitrate used for this video layer, specified in kbps.|  
|`MaxBitrate`<br /><br /> minOccurs="0"|`xs:int`|The maximum bitrate used for this video layer, specified in kbps.|  
|`BufferWindow`<br /><br /> minOccurs="0"<br /><br /> default="00:00:05"|`xs:time`|Length of the video buffer.|  
|`Width`<br /><br /> minOccurs="0"|`xs:int`|Width of the output video frame, in pixels.<br /><br /> Note that currently, you must specify both Width and Height .|  
|`Height`<br /><br /> minOccurs="0"|`xs:int`|Height of the output video frame, in pixels.<br /><br /> Note that currently, you must specify both Width and Height .|  
|`BFrames`<br /><br /> minOccurs="0"|`xs:int`|Number of B frames between reference frames.|  
|`ReferenceFrames`<br /><br /> minOccurs="0"<br /><br /> default=”3”|`xs:int`|Number of reference frames in a GOP.|  
|`EntropyMode`<br /><br /> minOccurs="0"<br /><br /> default=”Cabac”|`xs:string`|Could be one of the following values: `Cabac` and `Cavlc`.|  
|`FrameRate`<br /><br /> minOccurs="0"|rational number|Determines the frame rate of the output video. Use default of “0/1” to let the encoder use the same frame rate as the input video. Allowed values are expected to be common video frame rates, as shown below. However, any valid rational is allowed. For example 1/1 would be 1 fps and is valid.<br /><br /> - 12/1  (12 fps)<br /><br /> - 15/1 (15 fps)<br /><br /> - 24/1 (24 fps)<br /><br /> - 24000/1001 (23.976 fps)<br /><br /> - 25/1 (25 fps)<br /><br /> - 30/1 (30 fps)<br /><br /> - 30000/1001 (29.97 fps)|  
|`AdaptiveBFrame`<br /><br /> minOccurs="0"|`xs:boolean`|Copy from Azure media encoder|  
|`Slices`<br /><br /> minOccurs="0"<br /><br /> default="0"|`xs:int`|Determines how many slices a frame is divided into. Recommend using default.|  
  
##  <a name="AACAudio"></a> AACAudio  
 Contains a sequence of the following elements and groups.  
  
 For more information about AAC, see [AAC](https://en.wikipedia.org/wiki/Advanced_Audio_Coding).  
  
### Elements  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Profile`<br /><br /> minOccurs="0 "<br /><br /> default="AACLC"|`xs:string`|Could be one of the following values: `AACLC`, `HEAACV1`, or `HEAACV2`.|  
  
### Attributes  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Condition`|`xs:string`|To force the encoder to produce an asset that contains a silent audio track when input has no audio, specify the "InsertSilenceIfNoAudio" value.<br /><br /> By default, if you send an input to the encoder that contains only video, and no audio, then the output asset will contain files that contain only video data. Some players may not be able to handle such output streams. You can use this setting to force the encoder to add a silent audio track to the output in that scenario.|  
  
### Groups  
  
|Reference|Description|  
|---------------|-----------------|  
|[AudioGroup](#AudioGroup)<br /><br /> minOccurs="0"|See description of [AudioGroup](#AudioGroup) to know the appropriate number of channels, sampling rate, and bit rate that could be set for each profile.|  
  
##  <a name="AudioGroup"></a> AudioGroup  
 For details about what values are valid for each profile, see the “Audio codec details” table that follows.  
  
### Elements  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Channels`<br /><br /> minOccurs="0"|`xs:int`|The number of audio channels encoded. The following are valid options: 1, 2, 5, 6, 8.<br /><br /> Default: 2.|  
|`SamplingRate`<br /><br /> minOccurs="0"|`xs:int`|The audio sampling rate, specified in Hz.|  
|`Bitrate`<br /><br /> minOccurs="0"|`xs:int`|The bitrate used when encoding the audio, specified in kbps.|  
  
### Audio codec details  
  
|Audio Codec||  
|-----------------|-|  
|`AACLC`|1:<br /><br /> - 11025 : 8 <= bitrate < 16<br /><br /> - 12000 : 8 <= bitrate < 16<br /><br /> - 16000 : 8 <= bitrate < 32<br /><br /> - 22050 : 24 <= bitrate < 32<br /><br /> - 24000 : 24 <= bitrate < 32<br /><br /> - 32000 : 32 <= bitrate <= 192<br /><br /> - 44100 : 56 <= bitrate <= 288<br /><br /> - 48000 : 56 <= bitrate <= 288<br /><br /> - 88200 : 128 <= bitrate <= 288<br /><br /> - 96000 : 128 <= bitrate <= 288<br /><br /> 2:<br /><br /> - 11025 : 16 <= bitrate < 24<br /><br /> - 12000 : 16 <= bitrate < 24<br /><br /> - 16000 : 16 <= bitrate < 40<br /><br /> - 22050 : 32 <= bitrate < 40<br /><br /> - 24000 : 32 <= bitrate < 40<br /><br /> - 32000 :  40 <= bitrate <= 384<br /><br /> - 44100 : 96 <= bitrate <= 576<br /><br /> - 48000 : 96 <= bitrate <= 576<br /><br /> - 88200 : 256 <= bitrate <= 576<br /><br /> - 96000 : 256 <= bitrate <= 576<br /><br /> 5/6:<br /><br /> - 32000 : 160 <= bitrate <= 896<br /><br /> - 44100 : 240 <= bitrate <= 1024<br /><br /> - 48000 : 240 <= bitrate <= 1024<br /><br /> - 88200 : 640 <= bitrate <= 1024<br /><br /> - 96000 : 640 <= bitrate <= 1024<br /><br /> 8:<br /><br /> - 32000 : 224 <= bitrate <= 1024<br /><br /> - 44100 : 384 <= bitrate <= 1024<br /><br /> - 48000 : 384 <= bitrate <= 1024<br /><br /> - 88200 : 896 <= bitrate <= 1024<br /><br /> - 96000 : 896 <= bitrate <= 1024|  
|`HEAACV1`|1:<br /><br /> - 22050 : bitrate = 8<br /><br /> - 24000 : 8 <= bitrate <= 10<br /><br /> - 32000 : 12 <= bitrate <= 64<br /><br /> - 44100 : 20 <= bitrate <= 64<br /><br /> - 48000 : 20 <= bitrate <= 64<br /><br /> - 88200 : bitrate = 64<br /><br /> 2:<br /><br /> - 32000 : 16 <= bitrate <= 128<br /><br /> - 44100 : 16 <= bitrate <= 128<br /><br /> - 48000 : 16 <= bitrate <= 128<br /><br /> - 88200 : 96 <= bitrate <= 128<br /><br /> - 96000 : 96 <= bitrate <= 128<br /><br /> 5/6:<br /><br /> - 32000 : 64 <= bitrate <= 320<br /><br /> - 44100 : 64 <= bitrate <= 320<br /><br /> - 48000 : 64 <= bitrate <= 320<br /><br /> - 88200 : 256 <= bitrate <= 320<br /><br /> - 96000 : 256 <= bitrate <= 320<br /><br /> 8:<br /><br /> - 32000 : 96 <= bitrate <= 448<br /><br /> - 44100 : 96 <= bitrate <= 448<br /><br /> - 48000 : 96 <= bitrate <= 448<br /><br /> - 88200 : 384 <= bitrate <= 448<br /><br /> - 96000 : 384 <= bitrate <= 448|  
|`HEAACV2`|2:<br /><br /> - 22050 : 8 <= bitrate <= 10<br /><br /> - 24000 : 8 <= bitrate <= 10<br /><br /> - 32000 : 12 <= bitrate <= 64<br /><br /> - 44100 : 20 <= bitrate <= 64<br /><br /> - 48000 : 20 <= bitrate <= 64<br /><br /> - 88200 : 64 <= bitrate <= 64|  
  
##  <a name="Clip"></a> Clip  
  
### Attributes  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`StartTime`|`xs:duration`|Specifies the start time of a presentation. The value of StartTime needs to match the absolute timestamps of the input video. For example, if the first frame of the input video has a timestamp of 12:00:10.000, then StartTime should be at least 12:00:10.000 or greater.|  
|`Duration`|`xs:duration`|Specifies the duration of a presentation (for example, appearance of an overlay in the video).|  
  
##  <a name="Output"></a> Output  
  
### Attributes  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`FileName`|`xs:string`|The name of the output file.<br /><br /> You can use macros described in the following table to build the output file names. For example:<br /><br /> `"Outputs": [      {       "FileName": "{Basename}_{Resolution}_{Bitrate}.mp4",       "Format": {         "Type": "MP4Format"       }     }   ]`|  
  
### Macros  
  
|Macro|Description|  
|-----------|-----------------|  
|`{Basename}`|If you are doing VoD encoding, the {Basename} is the first 32 characters of the AssetFile.Name property of the primary file in the input asset.<br /><br /> If the input asset is a live archive, then the {Basename} is derived from the trackName attributes in the server manifest. If you are submitting a subclip job using the TopBitrate, as in: “<VideoStream\>TopBitrate</VideoStream\>”, and the output file contains video, then the {Basename} is the first 32 characters of the trackName of the video layer with the highest bitrate.<br /><br /> If instead you are submitting a subclip job using all of the input bitrates, such as “<VideoStream\>*</VideoStream\>”, and the output file contains video, then {Basename} is the first 32 characters of the trackName of the corresponding video layer.|  
|`{Codec}`|Maps to “H264” for video and “AAC” for audio.|  
|`{Bitrate}`|The target video bitrate if the output file contains video and audio, or target audio bitrate if the output file contains audio only. The value used is the bitrate in kbps.|  
|`{Channel}`|Audio channel count if the file contains audio.|  
|`{Width}`|Width of the video, in pixels, in the output file, if the file contains video.|  
|`{Height}`|Height of the video, in pixels, in the output file, if the file contains video.|  
|`{Extension}`|Inherits from the “Type” property for the output file. The output file name will have an extension which is one of : “mp4”, “ts”, “jpg”, “png” or “bmp”.|  
|`{Index}`|Mandatory for thumbnail. Should only be present once.|  
  
##  <a name="H264Format"></a> H264Format (complex type inherits from Format)  
  
##  <a name="BmpFormat"></a> BmpFormat (complex type inherits from Format)  
  
##  <a name="PngFormat"></a> PngFormat (complex type inherits from Format)  
  
##  <a name="JpgFormat"></a> JpgFormat (complex type inherits from Format)  
  
##  <a name="Video"></a> Video (complex type inherits from Codec)  
  
### Attributes  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Start`|`xs:string`||  
|`Step`|`xs:string`||  
|`Range`|`xs:string`||  
|`PreserveResolutionAfterRotation`|`xs:boolean`|For detailed explanation, see the following section: [PreserveResolutionAfterRotation](#PreserveResolutionAfterRotation)|  
  
###  <a name="PreserveResolutionAfterRotation"></a> PreserveResolutionAfterRotation  
 It is recommended to use the PreserveResolutionAfterRotation flag in combination with resolution values expressed in percentage terms (Width=”100%” , Height = “100%”).  
  
 By default, the encode resolution settings (Width, Height) in the Media Encoder Standard (MES) presets are targeted at videos with 0 degree rotation. For example, if your input video is 1280x720 with zero degree rotation, then the default presets ensure that the output has the same resolution. See picture below.  
  
 ![AMS&#95;MESRoation1](../MediaServices/media/AMS_MESRoation1.png "AMS_MESRoation1")  
  
 However, this means that if the input video has been captured with non-zero rotation (eg. a smartphone or tablet held vertically), then MES by default will apply the encode resolution settings (Width, Height) to the input video, and then compensate for the rotation. For example, see the picture below. The preset uses Width = “100%”, Height = “100%”, which MES interprets as requiring the output to be 1280 pixels wide and 720 pixels tall. After rotating the video, it then shrinks the picture to fit into that window, leading to pillar-box areas on the left and right.  
  
 ![AMS&#95;MESRoation2](../MediaServices/media/AMS_MESRoation2.png "AMS_MESRoation2")  
  
 If the above is not the desired behavior, then you can make use of the PreserveResolutionAfterRotation  flag and set it to “true” (default is “false”). So if your preset has Width = “100%”, Height = “100%” and PreserveResolutionAfterRotation  set to “true”,  an input video which is 1280 pixels wide and 720 pixels tall with 90 degree rotation will produce an output with zero degree rotation, but 720 pixels wide and 1280 pixels tall. See the picture below.  
  
 ![AMS&#95;MESRoation3](../MediaServices/media/AMS_MESRoation3.png "AMS_MESRoation3")  
  
##  <a name="FormatGroup"></a> FormatGroup (group)  
  
### Elements  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`BmpFormat`|[BmpFormat](#BmpFormat)||  
|`PngFormat`|[PngFormat](#PngFormat)||  
|`JpgFormat`|[JpgFormat](#JpgFormat)||  
  
##  <a name="BmpLayer"></a> BmpLayer  
  
### Element  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Width`<br /><br /> minOccurs="0"|`xs:int`||  
|`Height`<br /><br /> minOccurs="0"|`xs:int`||  
  
### Attributes  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Condition`|`xs:string`||  
  
##  <a name="PngLayer"></a> PngLayer  
  
### Element  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Width`<br /><br /> minOccurs="0"|`xs:int`||  
|`Height`<br /><br /> minOccurs="0"|`xs:int`||  
  
### Attributes  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Condition`|`xs:string`||  
  
##  <a name="JpgLayer"></a> JpgLayer  
  
### Element  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Width`<br /><br /> minOccurs="0"|`xs:int`||  
|`Height`<br /><br /> minOccurs="0"|`xs:int`||  
|`Quality`<br /><br /> minOccurs="0"|`xs:int`|Valid values: 1(worst)-100(best)|  
  
### Attributes  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Condition`|`xs:string`||  
  
##  <a name="PngLayers"></a> PngLayers  
  
### Elements  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`PngLayer`<br /><br /> minOccurs="0" maxOccurs="unbounded"|[PngLayer](#PngLayer)||  
  
##  <a name="BmpLayers"></a> BmpLayers  
  
### Elements  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`BmpLayer`<br /><br /> minOccurs="0" maxOccurs="unbounded"|[BmpLayer](#BmpLayer)||  
  
##  <a name="JpgLayers"></a> JpgLayers  
  
### Elements  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`JpgLayer`<br /><br /> minOccurs="0" maxOccurs="unbounded"|[JpgLayer](#JpgLayer)||  
  
##  <a name="BmpImage"></a> BmpImage (complex type inherits from Video)  
  
### Elements  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`PngLayers`<br /><br /> minOccurs="0"|[PngLayers](#PngLayers)|Png layers|  
  
##  <a name="JpgImage"></a> JpgImage (complex type inherits from Video)  
  
### Elements  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`PngLayers`<br /><br /> minOccurs="0"|[PngLayers](#PngLayers)|Png layers|  
  
##  <a name="PngImage"></a> PngImage (complex type inherits from Video)  
  
### Elements  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`PngLayers`<br /><br /> minOccurs="0"|[PngLayers](#PngLayers)|Png layers|  
  
## Examples  
 See examples of XML presets that are built based on this schema, see [Task Presets for MES (Media Encoder Standard)](../MediaServices/Task-Presets-for-MES--Media-Encoder-Standard-.md).
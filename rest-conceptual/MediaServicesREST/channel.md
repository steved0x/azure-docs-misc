---
title: "Channel"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 79aedfcd-4420-4023-bf47-05ef0006ddeb
caps.latest.revision: 19
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
# Channel
In Azure Media Services (AMS), the Channel entity represents a pipeline for processing live streaming content. A Channel receives live input streams in one of two ways:  
  
-   An on-premises live encoder sends multi-bitrate `RTMP` or `Smooth Streaming` (Fragmented MP4) to the Channel. You can use the following live encoders that output multi-bitrate Smooth Streaming: Elemental, Envivio, Cisco. The following live encoders output RTMP: Adobe Flash Live, Telestream Wirecast, and Tricaster transcoders. The ingested streams pass through Channels without any further processing. When requested, Media Services delivers the stream to customers.  
  
-   A single bitrate stream (in one of the following formats: `RTP` (MPEG-TS), `RTMP`, or `Smooth Streaming` (Fragmented MP4)) is sent to the `Channel` that is enabled to perform live encoding with Media Services. The `Channel` then performs live encoding of the incoming single bitrate stream to a multi-bitrate (adaptive) video stream. When requested, Media Services delivers the stream to customers.  
  
 Starting with the Media Services 2.10 release, when you create a Channel, you can specify in which way you want for your channel to receive the input stream and whether or not you want for the channel to perform live encoding of your stream. You have two options:  
  
-   `None` – Specify this value, if you plan to use an on-premises live encoder which will output multi-bitrate stream. In this case, the incoming stream passed through to the output without any encoding. This is the behavior of a Channel prior to 2.10 release. For more detailed information about working with channels of this type, see [Working with Channels that Receive Multi-bitrate Live Stream from On-premises Encoders](http://azure.microsoft.com/documentation/articles/media-services-manage-channels-overview/).  
  
-   `Standard` – If you plan to use Media Services to encode your single bitrate live stream to multi-bitrate stream, choose this value.  
  
    > [!NOTE]
    >  Be aware that there is a billing impact for live encoding and you should remember that leaving a live encoding channel in the "Running" state will incur billing charges.  It is recommended that you immediately stop your running channels after your live streaming event is complete to avoid extra hourly charges. For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](http://azure.microsoft.com/documentation/articles/media-services-manage-live-encoder-enabled-channels/).  
  
 For more information on Live Streaming and managing channels, see [Delivering Live Streaming with Azure Media Services](http://azure.microsoft.com/en-us/documentation/articles/media-services-live-streaming-workflow/).  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://msdn.microsoft.com/en-us/42ae6204-93bc-4797-bf40-1c68512cfb73).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
 This topic gives an overview of the `Channel` entity and also demonstrates how to execute various operations with the Media Services REST API.  
  
-   [Create Channels](#create_channels)  
  
-   [Start Channels](#start_channels)  
  
-   [Stop Channels](#stop_channels)  
  
-   [List Channels](#list_channels)  
  
-   [Reset Channels](#reset_channels)  
  
-   [Update Channels](#update_channels)  
  
-   [Start Advertisement](#StartAdvertisement)  
  
-   [End Advertisement](#EndAdvertisement)  
  
-   [Show Slate](#ShowSlate)  
  
-   [Hide Slate](#HideSlate)  
  
-   [Delete Channels](#delete_channels)  
  
## Channel Entity  
 The `Channel` entity contains the following properties.  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|`Id`<br /><br /> Read-only. Set by Media Services.|Edm.String|The Channel ID, assigned upon creation. The format is:<br /><br /> nb:chid:UUID:\<GUID>.|  
|`Name`|Edm.String|The Channel name.<br /><br /> 1.  Must be unique within your Media Services account.<br />2.  Maximum length = 32 characters.<br />3.  Cannot contain spaces.<br />4.  Hyphens and alphanumeric characters only.<br />5.  Cannot begin or end with a hyphen.|  
|`Created`<br /><br /> Read-only. Set by Media Services.|Edm.DateTime|A UTC date/time value that indicates the time of creation.|  
|`Description`|Edm.String|User provided description. The maximum length is 256 characters.|  
|`LastModified`<br /><br /> Read-only. Set by Media Services.|Edm.DateTime|The date and time of the last update to the channel.|  
|`State`<br /><br /> Read-only. Set by Media Services.|Edm.String|The current state of channel. Possible values include:<br /><br /> -   Stopped. This is the initial state of the Channel after its creation. In this state, the Channel properties can be updated but streaming is not allowed.<br />-   Starting. Channel is being started. No updates or streaming is allowed during this state. If an error occurs, the Channel returns to the **Stopped** state.<br />-   Running. The Channel is capable of processing live streams.<br />-   Stopping. The channel is being stopped. No updates or streaming is allowed during this state.<br />-   Deleting. The Channel is being deleted. No updates or streaming is allowed during this state.|  
|`Input`|[ChannelInput ComplexType](#ChannelInput)|Channel input (ingest) settings.|  
|`Output`|[ChannelOutput ComplexType](#ChannelOutput)|Channel output settings.|  
|`Preview`|[ChannelPreview ComplexType](#ChannelPreview)|Channel preview settings.|  
|`CrossSiteAccessPolicies`|[CrossSiteAccessPolicies](../MediaServicesREST/crosssiteaccesspolicies.md)|Cross site access policies.|  
|`Programs`<br /><br /> Read-only. Set by Media Services.|A collection of [Program](../MediaServicesREST/program.md)s.|A reference to the collection of programs associated with the channel.|  
|`EncodingType`|Edm.String|`Optional`. Describes the configuration of the Channel. Allowed values are:<br /><br /> -   `None` – This is the default value. When you select this value, the incoming stream passed through to the output without any encoding (this is the behavior of a Channel prior to 2.10 release).<br />-   `Standard` – The incoming single bitrate stream is sent to the Channel and transcoded into a multi-bitrate stream using [System presets](#SystemPreset)|  
|`Encoding`|[Encoding ComplexType](#encoding)|Azure live encoder settings.|  
|`Slate`|[Slate](#slate)|This setting is supported only when the `Encoding Type` of the Channel is set to `Standard`.<br /><br /> The live encoder within the Channel can be signaled to switch to a slate image. It can also be signaled to end an on-going slate.<br /><br /> The live encoder can be configured to switch to a slate image and mask the incoming video signal in certain situations – for example, during an ad break. If such a slate is not configured, input video is not masked during that ad break.|  
  
###  <a name="ChannelInput"></a> ChannelInput ComplexType  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`KeyFrameInterval`|Edm.Time|This value is ignored if `EncoderType` is set to `Standard`.<br /><br /> When using an on-premises live encoder to generate multi-bitrate stream, the keyf rame interval specifies GOP duration (as used by that external encoder). Once this incoming stream is received by the Channel, you can then deliver your live stream to client playback applications in any of the following formats: Smooth Streaming, DASH and HLS. When doing live streaming, HLS is always packaged dynamically. By default, Media Services automatically calculates HLS segment packaging ratio (fragments per segment) based on the key frame interval, also referred to as Group of Pictures – GOP, that is received from the live encoder.|  
|`StreamingProtocol`<br /><br /> Read-only.|Edm.String|After you set the encoder type, you can set an ingest protocol.<br /><br /> If the `Encoder Type` is set to `None`, valid options are:<br /><br /> -   Multi-bitrate Fragmented MP4 (Smooth Streaming)<br />-   Multi-bitrate RTMP<br /><br /> When your `Encoder Type` is set to `None`, it is valid, but undesirable, for a single bitrate RTMP or Smooth Streaming live stream to be sent. The channel does not do any processing with the stream, so it will pass through, but the client applications will get a single bitrate stream.<br /><br /> If the `Encoder Type` is set to `Standard`, valid options are:<br /><br /> 1.  Single bitrate Fragmented MP4 (Smooth Streaming)<br />2.  Single bitrate RTMP<br />3.  RTP (MPEG-TS): MPEG-2 Transport Stream over RTP.|  
|`AccessControl`|[ChannelInputAccessControl ComplexType](#ChannelInputAccessControl)|Channel input access control settings.|  
|`Endpoints`<br /><br /> Read-only.|[ChannelEndpoint ComplexType](#ChannelEndpoint)|Channel input endpoints.<br /><br /> A Channel provides input endpoints (ingest URLs) that you then use to ingest your live stream. The channel receives live input streams and makes the output streams available for streaming through one or more streaming endpoints.|  
  
###  <a name="ChannelPreview"></a> ChannelPreview ComplexType  
 For more detailed information about this type and its properties, see [Overview of Channels that are enabled for Live Encoding](http://azure.microsoft.com/documentation/articles/media-services-manage-live-encoder-enabled-channels/).  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`AccessControl`|[ChannelPreviewAccessControl ComplexType](#ChannelPreviewAccessControl)|Channel preview access control settings.|  
|`Endpoints`<br /><br /> Read-only.|[ChannelEndpoint ComplexType](#ChannelEndpoint)|Channel preview endpoints.|  
  
###  <a name="ChannelInputAccessControl "></a> ChannelInputAccessControl ComplexType  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`IP`|[IPAccessControl](#IPAccessControl)|IP addresses that are allowed to connect to channel input endpoints.|  
  
###  <a name="ChannelPreviewAccessControl "></a> ChannelPreviewAccessControl ComplexType  
 For more detailed information about this type and its properties, see [Overview of Channels that are enabled for Live Encoding](http://azure.microsoft.com/documentation/articles/media-services-manage-live-encoder-enabled-channels/).  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`IP`|[IPAccessControl](#IPAccessControl)|IP addresses that are allowed to connect to channel input endpoints.|  
  
###  <a name="IPAccessControl"></a> IPAccessControl  
 For more detailed information about this type and its properties, see [Overview of Channels that are enabled for Live Encoding](http://azure.microsoft.com/documentation/articles/media-services-manage-live-encoder-enabled-channels/).  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|Allow|[IPRange ComplexType](#IPRange)|IP addresses that are allowed to connect to channel input endpoints. **Note:**  Setting this value to null allows all IP source addresses to connect. Setting it to an empty string (“”) allows no one to connect.|  
  
###  <a name="IPRange"></a> IPRange ComplexType  
 For more detailed information about this type and its properties, see [Overview of Channels that are enabled for Live Encoding](http://azure.microsoft.com/documentation/articles/media-services-manage-live-encoder-enabled-channels/).  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Name`|Edm.String|A friendly name for this IP Range.|  
|`Address`|Edm.String|The base IP address for the subnet representation (for example:192.168.0.1).|  
|`SubnetPrefixLength`|Edm.Int32|The number of significant bits for the subnet mask (for example, in the following IP address 192.168.0.1/24, 24 represents the number of significant bits).|  
  
###  <a name="ChannelEndpoint"></a> ChannelEndpoint ComplexType  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Protocol`|Edm.String|The channel streaming endpoint protocol.|  
|`Url`|Edm.String|The channel streaming endpoint URL.|  
  
###  <a name="ChannelOutput"></a> ChannelOutput ComplexType  
 For more detailed information about this type and its properties, see [Overview of Channels that are enabled for Live Encoding](http://azure.microsoft.com/documentation/articles/media-services-manage-live-encoder-enabled-channels/)  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Hls`|[ChannelOutputHls ComplexType](#ChannelOutputHls)|The HLS specific settings.|  
  
###  <a name="ChannelOutputHls"></a> ChannelOutputHls ComplexType  
 For more detailed information about this type and its properties, see [Overview of Channels that are enabled for Live Encoding](http://azure.microsoft.com/documentation/articles/media-services-manage-live-encoder-enabled-channels/).  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`FragmentsPerSegment`|Edm.Int16|The amount of fragments per HTTP Live Streaming (HLS) segment.|  
  
###  <a name="encoding"></a> Encoding ComplexType  
 For more detailed information about this type and its properties, see [Overview of Channels that are enabled for Live Encoding](http://azure.microsoft.com/documentation/articles/media-services-manage-live-encoder-enabled-channels/).  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`AdMarkerSource`|Edm.String|You can specify the source for ad markers signals. Default value is `Api`, which indicates that the live encoder within the Channel should listen to an asynchronous `Ad Marker API`.The other valid option is `Scte35` (allowed only if the ingest streaming protocol is set to `RTP (MPEG-TS).` When `Scte35` is specified, the encoder will parse `SCTE-35` signals from the input RTP (MPEG-TS) stream.|  
|`IgnoreCea708ClosedCaptions`|Edm.bool|`Optional`. An optional flag which tells the live encoder to ignore any CEA 708 captions data embedded in the incoming video. When the flag is set to false (default), the encoder will detect and re-insert CEA 708 data into the output video streams.|  
|`VideoStream`|[VideoStream](#VideoStream)|`Optional`. Describes the input video stream. If this field is not specified, the default value is used. This setting is allowed only if the input streaming protocol is set to RTP (MPEG-TS).|  
|`AudioStreams`|[AudioStreams](#AudioStreams)|`Optional`. Describes the input audio streams. If this field is not specified, the default values specified apply. This setting is allowed only if the input streaming protocol is set to RTP (MPEG-TS).|  
|`SystemPreset`|Edm.String|Specifies the encoder preset to be used for this Channel. Currently, the only allowed value is `Default720p` (default).<br /><br /> For more details see [SystemPreset](#SystemPreset)|  
  
####  <a name="SystemPreset"></a> SystemPreset  
 `Default720p` specifies to encode the video to the following 7 layers.  
  
|BitRate|Width|Height|MaxFPS|Profile|Output Stream Name|  
|-------------|-----------|------------|------------|-------------|------------------------|  
|3500|1280|720|30|High|Video_1280x720_3500kbps|  
|2200|960|540|30|Main|Video_960x540_2200kbps|  
|1350|704|396|30|Main|Video_704x396_1350kbps|  
|850|512|288|30|Main|Video_512x288_850kbps|  
|550|384|216|30|Main|Video_384x216_550kbps|  
|350|340|192|30|Baseline|Video_340x192_350kbps|  
|200|340|192|30|Baseline|Video_340x192_200kbps|  
  
 Audio is encoded to stereo AAC-LC at 64 kbps, sampling rate of 44.1 kHz.  
  
 For more detailed information about this type and its properties, see [Overview of Channels that are enabled for Live Encoding](http://azure.microsoft.com/documentation/articles/media-services-manage-live-encoder-enabled-channels/).  
  
###  <a name="VideoStream"></a> VideoStream  
 Describes the input video stream. If this field is not specified, the default value is used. This setting is allowed only if the input streaming protocol is set to RTP (MPEG-TS).  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Index`|Edm.Int1|A zero-based index that specifies which input video stream should be processed by the live encoder within the Channel. This setting applies only if ingest streaming protocol is RTP (MPEG-TS).<br /><br /> Default value is zero. It is recommended to send in a single program transport stream (SPTS). If the input stream contains multiple programs, the live encoder parses the Program Map Table (PMT) in the input, identifies the inputs that have a stream type name of MPEG-2 Video or H.264, and arranges them in the order specified in the PMT. The zero-based index is then used to pick up the n-th entry in that arrangement.|  
|`Name`|Edm.String|`Optional`. Descriptive tag for this input video stream.|  
  
 For more detailed information about this type and its properties, see [Overview of Channels that are enabled for Live Encoding](http://azure.microsoft.com/documentation/articles/media-services-manage-live-encoder-enabled-channels/).  
  
###  <a name="AudioStreams"></a> AudioStreams  
 Describes the input audio streams. If this field is not specified, the default values specified apply. This setting is allowed only if the input streaming protocol is set to RTP (MPEG-TS).  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`Index`|Edm.Int16|It is recommended to send in a single program transport stream (SPTS). If the input stream contains multiple programs, the live encoder within the Channel parses the Program Map Table (PMT) in the input, identifies the inputs that have a stream type name of MPEG-2 AAC ADTS or AC-3 System-A or AC-3 System-B or MPEG-2 Private PES or MPEG-1 Audio or MPEG-2 Audio, and arranges them in the order specified in the PMT. The zero-based index is then used to pick up the n-th entry in that arrangement.|  
|`Name`|Edm.String|`Optional`. Descriptive tag for this input audio stream.|  
|`Language`|Edm.String|`Optional`. The language identifier of the audio stream, conforming to ISO 639-2, such as ENG. If not present, the default is UND (undefined).<br /><br /> There can be up to 8 audio stream sets specified if the input to the Channel is MPEG-2 TS over RTP. However, there can be no two entries with the same value of Index.|  
  
 There can be up to 8 {Index, Name, Language} sets specified if the input to the encoder is MPEG-2 TS over RTP. However, there can be no two entries with the same value of Index. If the input to the encoder is RTMP or HTTP (Smooth Streaming), then there can only be one audio stream in the input.  
  
###  <a name="slate"></a> Slate  
 This setting is supported only when the `Encoding Type` of the Channel is set to `Standard`.  
  
 The live encoder within the Channel can be signaled to switch to a slate image. It can also be signaled to end an on-going slate.  
  
 The live encoder can be configured to switch to a slate image and mask the incoming video signal in certain situations – for example, during an ad break. If such a slate is not configured, input video is not masked during that ad break.  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`InsertSlateOnAdMarker`|Edm.Bool|When set to True, this setting configures the live encoder to insert a slate image during an ad break. The default value is true.|  
|`DefaultSlateAssetId`|Edm.String|`Optional`. Specifies the Asset Id of the Media Services Asset which contains the slate image. Default is null.<br /><br /> Before creating the Channel, the slate image, of 1920x1080 maximum resolution, in JPEG format, and at most 3 Mbytes in size, should be uploaded as a dedicated asset (no other files should be in this asset). The file name should have a *.jpg extension, and this AssetFile should be marked as the primary file for that asset. This Asset cannot be storage encr2ypted.<br /><br /> If the default slate Asset Id is not specified, and insert slate on ad marker is set to true, a default Azure Media Services image will be used to mask the input stream.|  
  
 For more detailed information about this type and its properties, see [Overview of Channels that are enabled for Live Encoding](http://azure.microsoft.com/documentation/articles/media-services-manage-live-encoder-enabled-channels/).  
  
##  <a name="create_channels"></a> Create Channels  
 Channels can be created using a POST HTTP request and specifying property values.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/api/Channels|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
POST https://testrest.cloudapp.net/api/Channels HTTP/1.1  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json;odata=minimalmetadata  
Accept-Charset: UTF-8  
x-ms-version: 2.11  
Content-Type: application/json;odata=minimalmetadata  
Host: <redirected host URI>  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
  
```  
  
 The following request body shows how to create a channel that is enabled for live encoding.  
  
```  
{  
   "Id":null,  
   "Name":"testchannel001",     
   "Description":"",  
   "EncoderType":"Standard",  
   "Created":"0001-01-01T00:00:00",  
   "LastModified":"0001-01-01T00:00:00",  
   "State":null,  
   "Input":  
   {  
      "StreamingProtocol":"RTPMPEG2TS",  
      "AccessControl":  
      {  
         "IP":  
         {  
         "Allow":  
            [  
               {  
                  "Name":"testName1",  
                  "Address":"1.1.1.1",  
                  "SubnetPrefixLength":24  
               }  
            ]  
         }  
      },  
      "Endpoints":[]  
   },  
   "Encoding":  
   {  
      "SystemPreset":"Default720p",  
      "IgnoreCea708ClosedCaptions": false,  
      "AdMarkerSource": "Api"  
      "VideoStream":  
      {  
         "Index":1,  
         "Name":"Video stream"  
      },  
      "AudioStreams":  
      [  
         {  
            "Index":0,  
            "Name":"English audio stream",  
            "Language":"ENG"  
         },  
         {  
            "Index":1,  
            "Name":"Spanish audio stream",  
            "Language":"SPA"  
         }  
      ]  
   },  
   "EncodingType": "Standard",  
   "Slate":  
   {  
      "InsertOnAdMarker":true,  
      "DefaultSlateAssetId": "nb:cid:UUID:01234567-0123-0123-0123-01234567"  
   },  
   "Preview":  
   {  
      "AccessControl":  
      {  
         "IP":  
         {  
            "Allow":  
            [  
               {  
                  "Name":"testName1",  
                  "Address":"1.1.1.1",  
                  "SubnetPrefixLength":24  
               }  
            ]  
         }  
      },  
      "Endpoints":[]  
   }  
}  
  
```  
  
 The following request body shows how to create a channel in the account that is not enabled for live encoding.  
  
```  
{  
"Id":null,  
"Name":"testchannel001",  
"Description":"",  
"Created":"0001-01-01T00:00:00",  
"LastModified":"0001-01-01T00:00:00",  
"State":null,  
"Input":  
   {  
   "KeyFrameInterval":null,  
   "StreamingProtocol":"FragmentedMP4",  
   "AccessControl":  
      {  
         "IP":  
         {  
            "Allow":[{"Name":"testName1","Address":"1.1.1.1","SubnetPrefixLength":24}]  
         }  
      },  
   "Endpoints":[]  
   },  
"Preview":  
   {  
   "AccessControl":  
      {  
         "IP":  
         {  
            "Allow":[{"Name":"testName1","Address":"1.1.1.1","SubnetPrefixLength":24}]  
         }  
      },  
      "Endpoints":[]  
   },  
"Output":  
   {  
   "Hls":  
      {  
         "FragmentsPerSegment":1  
      }  
   },  
"CrossSiteAccessPolicies":  
   {  
      "ClientAccessPolicy":null,  
      "CrossDomainPolicy":null  
   }  
}  
```  
  
 If successful, a **202 Accepted** status code is returned along with a representation of the created entity in the response body.  
  
 The **202 Accepted** status code indicates an asynchronous operation, in which case the operation-id header value is also provided for use in polling and tracking the status of long-running operations, such as starting or stopping a Channel. Pass the operation-id header value into the Operation Entity to retrieve the status. For more information, see [Manually Polling Long-Running Operations](http://msdn.microsoft.com/en-us/3f8c9717-b557-47b8-bbef-18f867e98019).  
  
##  <a name="start_channels"></a> Start Channels  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/api/Channels(‘*channelid*’)/Start|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
POST https://testrest.cloudapp.net/api/Channels('nb:chid:UUID:2c30f424-ab90-40c6-ba41-52a993e9d393')/Start HTTP/1.1  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json;odata=minimalmetadata  
Accept-Charset: UTF-8  
x-ms-version: 2.11  
Content-Type: application/json;odata=minimalmetadata  
Host: <redirected host URI>  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
  
```  
  
 If successful, a **202 Accepted** status code is returned. The **202 Accepted** status code indicates an asynchronous operation, in which case the operation-id header value is also provided for use in polling and tracking the status of long-running operations, such as starting or stopping a Channel. Pass the operation-id header value into the Operation Entity to retrieve the status. For more information, see [Manually Polling Long-Running Operations](http://msdn.microsoft.com/en-us/3f8c9717-b557-47b8-bbef-18f867e98019).  
  
##  <a name="stop_channels"></a> Stop Channels  
 A channel can be stopped only when it is in the **Running** state, and all programs on the channel have been stopped.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/api/Channels(‘*channelid*’)/Stop|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
POST https://testrest.cloudapp.net/api/Channels('nb:chid:UUID:2c30f424-ab90-40c6-ba41-52a993e9d393')/Stop HTTP/1.1  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json;odata=minimalmetadata  
Accept-Charset: UTF-8  
x-ms-version: 2.11  
Content-Type: application/json;odata=minimalmetadata  
Host: <redirected host URI>  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
  
```  
  
 If successful, a **202 Accepted** status code is returned. The **202 Accepted** status code indicates an asynchronous operation, in which case the operation-id header value is also provided for use in polling and tracking the status of long-running operations, such as starting or stopping a Channel. Pass the operation-id header value into the Operation Entity to retrieve the status. For more information, see [Manually Polling Long-Running Operations](http://msdn.microsoft.com/en-us/3f8c9717-b557-47b8-bbef-18f867e98019).  
  
##  <a name="list_channels"></a> List Channels  
 Channels can be retrieved using a GET HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|Get all Channels:<br /><br /> https://media.windows.net/api/Channels<br /><br /> Get a specified Channel.<br /><br /> https://media.windows.net/api/Channels('*channelid*')|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
GET https://testrest.cloudapp.net/api/Channels HTTP/1.1  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json;odata=minimalmetadata  
Accept-Charset: UTF-8  
x-ms-version: 2.11  
Content-Type: application/json;odata=minimalmetadata  
Host: <redirected host URI>  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
  
```  
  
 If successful, this operation returns a **200 OK** status code and a list of all of the Channels created in your Media Services account.  
  
##  <a name="reset_channels"></a> Reset Channels  
 Resets runtime Channel state maintained throughout the streaming of a live presentation and allows for the reuse of a Channel in case of presentation resets or encoder reconfiguration.  Stop all Programs before calling Reset. Reset can be called on a Channel that is in the running state.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/api/Channels(‘*channelid*’)/Reset|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
POST https://testrest.cloudapp.net/api/Channels('nb:chid:UUID:2c30f424-ab90-40c6-ba41-52a993e9d393')/Reset HTTP/1.1  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json;odata=minimalmetadata  
Accept-Charset: UTF-8  
x-ms-version: 2.11  
Content-Type: application/json;odata=minimalmetadata  
Host: <redirected host URI>  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
  
```  
  
 If successful, a **202 Accepted** status code is returned. The **202 Accepted** status code indicates an asynchronous operation, in which case the operation-id header value is also provided for use in polling and tracking the status of long-running operations, such as starting or stopping a Channel. Pass the operation-id header value into the Operation Entity to retrieve the status. For more information, see [Manually Polling Long-Running Operations](http://msdn.microsoft.com/en-us/3f8c9717-b557-47b8-bbef-18f867e98019).  
  
##  <a name="update_channels"></a> Update Channels  
 Updates properties on an existing Channel. The Channel must be in the **Stopped** state.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|PATCH/PUT/MERGE<br /><br /> For more information about these operations, see [PATCH/PUT/MERGE](http://msdn.microsoft.com/en-us/library/dd541276.aspx).|https://media.windows.net/api/Channels(‘*channelid*’)|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
PATCH https://testrest.cloudapp.net/api/Channels('nb:chid:UUID:2c30f424-ab90-40c6-ba41-52a993e9d393') HTTP/1.1  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json;odata=minimalmetadata  
Accept-Charset: UTF-8  
x-ms-version: 2.11  
Content-Type: application/json;odata=minimalmetadata  
Host: <redirected host URI>  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
  
```  
  
 Request body:  
  
```  
"Encoding":{"IgnoreCea708ClosedCaptions": true}  
```  
  
 If the update completes synchronously, it returns a **204 No Content** status code; otherwise it returns a **202 Accepted** status code. The **202 Accepted** status code indicates an asynchronous operation, in which case the operation-id header value is also provided for use in polling and tracking the status of long-running operations, such as starting or stopping a Channel. Pass the operation-id header value into the Operation Entity to retrieve the status. For more information, see [Manually Polling Long-Running Operations](http://msdn.microsoft.com/en-us/3f8c9717-b557-47b8-bbef-18f867e98019).  
  
##  <a name="StartAdvertisement"></a> Start Advertisement  
 The live encoder can be signaled to start an advertisement or commercial break using a POST HTTP request and specifying property values of the in the [StartAdvertisement Entity](#StartAdvertisementEntity) entity in the body of the request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/api/Channels(‘*channeled*’)/StartAdvertisement|HTTP/1.1|  
  
 For more information, see [Overview of Channels that are enabled for Live Encoding](http://azure.microsoft.com/documentation/articles/media-services-manage-live-encoder-enabled-channels/).  
  
###  <a name="StartAdvertisementEntity"></a> StartAdvertisement Entity  
 This entity represents the start-of-advertisement API – it is an asynchronous call to the live encoder to insert an advertisement or commercial breaks in the output stream.  
  
 For more information, see [Overview of Channels that are enabled for Live Encoding](http://azure.microsoft.com/documentation/articles/media-services-manage-live-encoder-enabled-channels/).  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`duration`|Edm.Duration|The duration, in seconds, of the commercial break. This has to be a non-zero positive value in order to start the commercial break. When a commercial break is in progress, and the duration is set to zero with the CueId matching the on-going commercial break, then that break is canceled.|  
|`cueId`|Edm.Int|Unique ID for the commercial break, to be used by downstream application to take appropriate action(s). Needs to be a positive integer.|  
|`showSlate`|Edm.Bool|`Optional`. Indicates to the live encoder within the Channel that it needs to switch to the default slate image during the commercial break (and mask the incoming video feed). Default is false.<br /><br /> The image used will be the one specified via the default slate asset Id property at the time of the channel creation.|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
POST https://testrest.cloudapp.net/api/Channels('nb:chid:UUID:2c30f424-ab90-40c6-ba41-52a993e9d393')/StartAdvertisement HTTP/1.1  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json;odata=minimalmetadata  
Accept-Charset: UTF-8  
x-ms-version: 2.11  
Content-Type: application/json;odata=minimalmetadata  
Host: <redirected host URI>  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
  
```  
  
 Body  
  
```  
{  
   "duration":"PT45S",  
   "cueId":"67520935",  
   "showSlate":"true"  
}  
  
```  
  
 If successful, a **202 Accepted** status code is returned.  
  
##  <a name="EndAdvertisement"></a> End Advertisement  
 The live encoder can be signaled to end an on-going advertisement or commercial break using a POST HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/api/Channels(‘*channeled*’)/EndAdvertisement|HTTP/1.1|  
  
 This call should only be invoked when there is an on-going advertisement.  
  
 For more information, see [Overview of Channels that are enabled for Live Encoding](http://azure.microsoft.com/documentation/articles/media-services-manage-live-encoder-enabled-channels/).  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
POST https://testrest.cloudapp.net/api/Channels('nb:chid:UUID:2c30f424-ab90-40c6-ba41-52a993e9d393')/EndAdvertisement HTTP/1.1  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json;odata=minimalmetadata  
Accept-Charset: UTF-8  
x-ms-version: 2.11  
Content-Type: application/json;odata=minimalmetadata  
Host: <redirected host URI>  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
  
```  
  
 If successful, a **202 Accepted** status code is returned.  
  
##  <a name="ShowSlate"></a> Show Slate  
 Indicates to the live encoder within the Channel that it needs to switch to the default slate image during the commercial break (and mask the incoming video feed). Default is false. The image used will be the one specified via the default slate asset Id property at the time of the channel creation.  
  
 Use properties of [ShowSlate Entity](#ShowSlateEntity) in the body of the HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/api/Channels(‘*channeled*’)/ShowSlate|HTTP/1.1|  
  
 For more information, see [Overview of Channels that are enabled for Live Encoding](http://azure.microsoft.com/documentation/articles/media-services-manage-live-encoder-enabled-channels/).  
  
###  <a name="ShowSlateEntity"></a> ShowSlate Entity  
 For more information, see [Overview of Channels that are enabled for Live Encoding](http://azure.microsoft.com/documentation/articles/media-services-manage-live-encoder-enabled-channels/).  
  
|Name|Type|Description|  
|----------|----------|-----------------|  
|`duration`|Edm.Duration|The duration, in seconds, of the slate. This has to be a non-zero positive value in order to start the slate. If there is an on-going slate, and duration of zero is specified, then that on-going slate will be terminated.|  
|`assetId`|Edm.String|Specifies the Asset Id of the Media Services Asset which contains the slate image.<br /><br /> Before creating the Channel, the slate image, of 1920x1080 resolution, in JPEG format, and at most 3 Mbytes in size, should be uploaded as a dedicated Asset (no other files should be in this Asset).<br /><br /> The encoder can be signaled to switch to any arbitrary slate image (and not just the one specified via the DefaultSlateAssetId property at time of creating the Channel).|  
  
 If the `DefaultSlateAssetId` property is specified, and `AssetId` is not specified, then the `DefaultSlateAssetId` image will be used to mask the input stream.  For more information, see [Slate](#slate).  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
POST https://testrest.cloudapp.net/api/Channels('nb:chid:UUID:2c30f424-ab90-40c6-ba41-52a993e9d393')/ShowSlate HTTP/1.1  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json;odata=minimalmetadata  
Accept-Charset: UTF-8  
x-ms-version: 2.11  
Content-Type: application/json;odata=minimalmetadata  
Host: <redirected host URI>  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
  
```  
  
 Body  
  
```  
{  
   "duration":"PT45S",  
   "assetId":"nb:cid:UUID:01234567-ABCD-ABCD-EFEF-01234567"  
}  
  
```  
  
 If successful, a **202 Accepted** status code is returned.  
  
##  <a name="HideSlate"></a> Hide Slate  
 The live encoder can be signaled to end an on-going slate using a POST HTTP request.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|POST|https://media.windows.net/api/Channels(‘*channelid*’)/HideSlate|HTTP/1.1|  
  
 This call should only be invoked when there is an on-going slate.  
  
 For more information, see [Overview of Channels that are enabled for Live Encoding](http://azure.microsoft.com/documentation/articles/media-services-manage-live-encoder-enabled-channels/).  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
POST https://testrest.cloudapp.net/api/Channels('nb:chid:UUID:2c30f424-ab90-40c6-ba41-52a993e9d393')/HideSlate HTTP/1.1  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json;odata=minimalmetadata  
Accept-Charset: UTF-8  
x-ms-version: 2.11  
Content-Type: application/json;odata=minimalmetadata  
Host: <redirected host URI>  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
  
```  
  
 If successful, a **202 Accepted** status code is returned. The **202 Accepted** status code indicates an asynchronous operation, in which case the operation-id header value is also provided for use in polling and tracking the status of long-running operations, such as starting or stopping a Channel. Pass the operation-id header value into the Operation Entity to retrieve the status. For more information, see [Manually Polling Long-Running Operations](http://msdn.microsoft.com/en-us/3f8c9717-b557-47b8-bbef-18f867e98019).  
  
##  <a name="delete_channels"></a> Delete Channels  
 Delete a channel.  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|DELETE|https://media.windows.net/api/Channels(‘*channelid*’)|HTTP/1.1|  
  
### Sample Request  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 You can try out the following example in the [Fiddler](http://www.telerik.com/download/fiddler)’s Composer tab. Make sure to use valid redirected host URI and authorization bearer token values.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
 Request headers:  
  
```  
DELETE https://testrest.cloudapp.net/api/Channels('nb:chid:UUID:2c30f424-ab90-40c6-ba41-52a993e9d393') HTTP/1.1  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Accept: application/json;odata=minimalmetadata  
Accept-Charset: UTF-8  
x-ms-version: 2.11  
Content-Type: application/json;odata=minimalmetadata  
Host: <redirected host URI>  
User-Agent: Microsoft ADO.NET Data Services  
Authorization: Bearer <token value>  
  
```  
  
 If successful, a **202 Accepted** status code is returned. The **202 Accepted** status code indicates an asynchronous operation, in which case the operation-id header value is also provided for use in polling and tracking the status of long-running operations, such as starting or stopping a Channel. Pass the operation-id header value into the Operation Entity to retrieve the status. For more information, see [Manually Polling Long-Running Operations](http://msdn.microsoft.com/en-us/3f8c9717-b557-47b8-bbef-18f867e98019).  
  
## See Also  
 [Delivering Live Streaming with Azure Media Services](http://azure.microsoft.com/en-us/documentation/articles/media-services-live-streaming-workflow/)   
 [Origin](../MediaServicesREST/origin1.md)   
 [Program](../MediaServicesREST/program.md)
---
title: "Task Preset for Azure Media Encryptor"
ms.custom: na
ms.date: 2016-07-13
ms.prod: azure
ms.reviewer: na
ms.service: media-services
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 05a9360d-fa41-4b44-b329-ef854e539505
caps.latest.revision: 40
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
# Task Preset for Azure Media Encryptor
> [!NOTE]
>  The end of life date for Windows Azure Media Packager and Windows Azure Media Encryptor has been extended to March 1, 2017. Before that date, the functionalities of these processors will be added to Media Encoder Standard (MES). Customers will be provided with instructions on how to migrate their workflows to send Jobs to MES. Format conversion and encryption capabilities may also be available through dynamic packaging and dynamic encryption.  
  
 When you run Microsoft Azure Media Services processing tasks such as encoding and encryption, you can use task preset files to store configuration settings for the tasks. The task configuration file described in this topic is used by the Windows Azure Media Encryptor processor. This processor enables you to encrypt media assets using PlayReady Protection. You would use this task when doing [static encryption to protect your content with PlayReady](http://azure.microsoft.com/documentation/articles/media-services-static-packaging/). However, it is recommended to use dynamic encryption.  
  
 Media Services now provides a service for delivering Microsoft PlayReady licenses. To sign up for PlayReady License Delivery Service do the following:  
  
 Follow instructions described in [Preview features](http://azure.microsoft.com/services/preview/).  
  
 In the [Azure Management Portal](http://go.microsoft.com/fwlink/?LinkID=256666&clcid=0x409), go to the **CONTENT PROTECTION** tab and add a row to the **Branding Reporting** table. The Media Services PlayReady license service will be enabled a few minutes after you press **SAVE**.  
  
 Once you sign up for PlayReady license deliver service, you can use the [Azure Management Portal](https://manage.windowsazure.com) to configure your PlayReady license service policy. Media Services also provides APIs that let you configure the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user is trying to play back protected content. For more information, see [Using PlayReady Dynamic Encryption and License Delivery Service](assetId:///c5460a07-ef81-4765-9812-226a7ad6e07c).  
  
 You can also choose to implement your own or use a third-party provider. For more information about implementing your own PlayReady license server see: [Microsoft PlayReady Overview](http://www.microsoft.com/playready/overview/).  
  
## Azure Media Encryptor Preset  
 In the PlayReady Protection task, Microsoft Smooth Streaming files (.ismv, .isma) are encrypted per the MPEG Common Encryption (CENC) specification (ISO 23001-7:2011) for use by Microsoft PlayReady and the client manifest is updated for use by Smooth Streaming clients.  
  
 To deliver MPEG DASH encrypted with PlayReady, make sure to use CENC options by setting the `useSencBox` and `adjustSubSamples` properties (described later in this topic) to `true`.  
  
 Copy the following configuration xml and use it to create a file named `MediaEncryptor_PlayReadyProtection.xml` on your local computer. Then update the configuration file with the required settings. Ask your licensing provider for the appropriate values to use.  
  
 To make the sample configuration file work with a task, provide the following values:  
  
-   A `licenseAcquisitionUrl` value.  You must specify values for the `licenseAquisitionURL` setting of your PlayReady license server.  
  
-   A `keyId` value and a `contentKey` value.  The `keyId` value can be a randomly generated guid (you can generate a guid for a `keyId` in code, or by using tools in Visual Studio). Key Ids must be unique and could only be associated with one content key.  
  
     It is recommended to use `keySeedValue` and `keyId` values to generate a `contentKey` value. The `keySeedValue` value is provided with a PlayReady license server, or for testing you can obtain a default value on the PlayReady test site. You can use the [Microsoft.WindowsAzure.MediaServices.Client.CommonEncryption.GeneratePlayReadyContentKey](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.commonencryption.generateplayreadycontentkey\(v=azure.10\).aspx) method to generate the content key based on keySeedValue and keyId. Once you generate the content key value, add the `keyId` and the associated `contentKey` to the configuration file.  
  
     As an alternative to using `keyId` and `contentKey`, you can add a `keySeedValue` directly in the configuration file. Adding `keySeedValue` to the configuration file should only be done for testing purposes.  
  
    > [!IMPORTANT]
    >  Using a `keySeedValue` in a task configuration file is not recommended for production applications. Because the key seed is used to generate content keys for your PlayReady protected content, there is a security risk involved with storing it in configuration. For production PlayReady applications, the recommended practice is to use a `keyId` with a generated `contentKey`.  
  
 If you want to test using the `keySeedValue` and `licenseAcquisitionUrl` values provided by the [PlayReady test server](http://playready.directtaps.net/pr/doc/customrights/). Use the following:.  
  
```  
. . .   
    <property name="keySeedValue" value="XVBovsmzhP9gRIZxWfFta3VVRPzVEWmJsazEJ46I" />  
    <property name="licenseAcquisitionUrl" value="http://playready.directtaps.net/pr/svc/rightsmanager.asmx" />  
. . .  
```  
  
 The [Using Static Encryption to Protect your Smooth and MPEG DASH with PlayReady](http://azure.microsoft.com/documentation/articles/media-services-static-packaging/) topic demonstrates how to do static encryption using the Media Services PlayReady license delivery service.  
  
```  
<taskDefinition xmlns="http://schemas.microsoft.com/iis/media/v4/TM/TaskDefinition#">  
  <name>PlayReady Protection</name>  
  <id>9A3BFEAC-F8AE-41CA-87FA-D639E4D1C753</id>  
  <description xml:lang="en" />  
  <properties namespace="http://schemas.microsoft.com/iis/media/v4/SharedData#" prefix="sd">  
    <property name="adjustSubSamples" value="true" />  
    <property name="contentKey" value="" />  
    <property name="customAttributes" value="" />  
    <property name="dataFormats" value="h264, avc1, mp4a, vc1, wma, owma, ovc1, aacl, aach, ac-3, ec-3, mlpa, dtsc, dtsh, dtsl, dtse" />  
    <property name="keyId" value="" />  
    <property name="keySeedValue" value="" />  
    <property name="licenseAcquisitionUrl" value="" />  
    <property name="useSencBox" value="true" />  
    <property name="serviceId" value="" />  
  </properties>  
  <inputFolder/>  
  <outputFolder>Protected</outputFolder>  
  <taskCode>  
    <type>Microsoft.Web.Media.TransformManager.DigitalRightsManagementTask, Microsoft.Web.Media.TransformManager.DigitalRightsManagement, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35</type>  
  </taskCode>  
</taskDefinition>  
  
```  
  
 The configuration file must conform to the syntax rules of a well formed xml file.  
  
 The following table explains the properties of the `Azure Media Encryptor` xml:  
  
|Name|Required|Description|  
|----------|--------------|-----------------|  
|adjustSubSamples|false|When encrypting subsamples on H.264 tracks, adjusts the clear space at the beginning of each subsample so that a whole number of encryption blocks is used. This leaves slightly more of the sample data unencrypted but maximizes player compatibility.|  
|contentKey|false|A base64-encoded 16-byte value, which is produced by the key seed in conjunction with the key ID and is used to encrypt content. You must enter a content key value if no key seed value is specified.|  
|customAttributes|false|A comma-delimited list of name:value pairs (in the form name1:value1,name2:value2,name3:value3) to be included in the CUSTOMATTRIBUTES section of the WRM header. The WRM header is XML metadata added to encrypted content and included in the client manifest. It is also included in license challenges made to license servers.|  
|dataFormats|false|A comma-delimited list of four-character codes (FourCCs) that specify the data formats to be encrypted. If no value is specified, all data formats are encrypted.|  
|keyId|false|A globally unique identifier (GUID) that uniquely identifies content for the purposes of licensing. Key Ids must be unique and could only be associated with one content key. If no value is specified, a random value is used.|  
|keySeedValue|true, if a contentKey is not specified. Otherwise, false.|A fixed, base64-encoded 30-byte value that enables a protection task to auto-generate the key for each content item. A key seed is used together with a key ID to generate a content key. Typically, one key seed is used with many key IDs to protect multiple files or sets of files; for example, all files issued by a license server or perhaps all files by a particular artist. Key seeds are stored on license servers.<br /><br /> You can use the following Media Services SDK for .NET method to generate the content key based on the keySeedValue: [Microsoft.WindowsAzure.MediaServices.Client.CommonEncryption.GeneratePlayReadyContentKey](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.commonencryption.generateplayreadycontentkey\(v=azure.10\).aspx).|  
|licenseAcquisitionUrl|true|The Web page address of a license server (for example, a PlayReady license server). A client player uses the URL to contact the license server and obtain a license to decrypt the content for playback.|  
|useSencBox|false|Use a 'senc' box to hold encryption metadata instead of a Protected Interoperable File Format (PIFF) 1.1 'uuid' box.|  
|serviceId|false|The service ID to include in the PlayReady header that is added to each file and in the client manifest (.ismc). This value must be a globally unique identifier (GUID) in Little Endian string form (like this 237A4EB1-9D01-4F4A-A2D2-79E51468014D)|
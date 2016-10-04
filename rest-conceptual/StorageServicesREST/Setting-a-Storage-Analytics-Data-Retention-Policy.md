---
title: "Setting a Storage Analytics Data Retention Policy"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 03869817-29fb-4d56-8a9c-3995b5b4ecaa
caps.latest.revision: 14
author: tamram
manager: carolz
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
# Setting a Storage Analytics Data Retention Policy
By default, Storage Analytics will not delete any logging or metrics data. Blobs and table entities will continue to be written until the shared 20TB limit is reached. Once the 20TB limit is reached, Storage Analytics will stop writing new data and will not resume until free space is available. This 20TB limit is independent of the total limit for your storage account. For more information on storage account limits, see [Azure Storage Scalability and Performance Targets](assetId:///26df4d89-8289-4b31-aaa0-df971cab9b52).  
  
 There are two ways to delete Storage Analytics data: by manually making deletion requests or by setting a data retention policy. Manual requests to delete Storage Analytics data are billable, but delete requests resulting from a retention policy are not billable.  
  
> [!IMPORTANT]
>  To avoid unnecessary charges, set a retention policy for logging and metrics.  
  
## Setting a Data Retention Policy  
 You can configure two data retention policies: one for logging and one for metrics. When enabled for both, Storage Analytics will delete logs and table entries older than the specified number of days. The maximum retention period is 365 days (1 year).  
  
> [!NOTE]
>  When you make any changes to your retention policy, it may take several minutes for your settings to be applied.  
  
 To set up a policy that deletes both logging and metrics data after 7 days, make a request to the [Set Blob Service Properties](../StorageServicesREST/Set-Blob-Service-Properties.md), [Set Table Service Properties](../StorageServicesREST/Set-Table-Service-Properties.md), or [Set Queue Service Properties](../StorageServicesREST/Set-Queue-Service-Properties.md) operation with the `<RetentionPolicy>` nodes configured like shown:  
  
```  
…  
<RetentionPolicy>  
    <Enabled>true</Enabled>  
    <Days>7</Days>  
</RetentionPolicy>  
…  
```  
  
 The following XML shows the `<RetentionPolicy>` nodes in the context of complete payload for a Set Blob Service Properties request:  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<StorageServiceProperties>  
    <Logging>  
        <Version>1.0</Version>  
        <Delete>true</Delete>  
        <Read>false</Read>  
        <Write>true </Write>  
        <RetentionPolicy>  
            <Enabled>true</Enabled>  
            <Days>7</Days>  
        </RetentionPolicy>  
    </Logging>  
    <HourMetrics>  
        <Version>1.0</Version>  
        <Enabled>true</Enabled>  
        <IncludeAPIs>false</IncludeAPIs>  
        <RetentionPolicy>  
            <Enabled>true</Enabled>  
            <Days>7</Days>  
        </RetentionPolicy>  
    </HourMetrics>  
    <MinuteMetrics>  
        <Version>1.0</Version>  
        <Enabled>true</Enabled>  
        <IncludeAPIs>false</IncludeAPIs>  
        <RetentionPolicy>  
            <Enabled>true</Enabled>  
            <Days>7</Days>  
        </RetentionPolicy>  
    </MinuteMetrics>  
    <DefaultServiceVersion>2013-08-15</DefaultServiceVersion>  
</StorageServiceProperties>  
```  
  
 You can also configure a retention policy that uses different periods for logging and metrics. To disable a retention policy in the future, call the Set Blob Service Properties operation with the `<Enabled>` node inside set to **false**, as shown below:  
  
```  
…  
<RetentionPolicy>  
    <Enabled>false</Enabled>  
    <Days>7</Days>  
</RetentionPolicy>  
…  
```  
  
> [!NOTE]
>  If you disable Storage Analytics for a storage service but a data retention policy is enabled, your old data will continue to get deleted. To avoid accidental data loss, ensure that you configure your data retention policy when enabling and disabling Storage Analytics.  
  
## See Also  
 [Set Blob Service Properties](../StorageServicesREST/Set-Blob-Service-Properties.md)   
 [Get Blob Service Properties](../StorageServicesREST/Get-Blob-Service-Properties.md)   
 [Set Table Service Properties](../StorageServicesREST/Set-Table-Service-Properties.md)   
 [Get Table Service Properties](../StorageServicesREST/Get-Table-Service-Properties.md)   
 [Set Queue Service Properties](../StorageServicesREST/Set-Queue-Service-Properties.md)   
 [Get Queue Service Properties](../StorageServicesREST/Get-Queue-Service-Properties.md)
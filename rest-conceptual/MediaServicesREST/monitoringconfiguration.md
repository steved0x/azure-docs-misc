---
title: "MonitoringConfiguration"
ms.custom: ""
ms.date: "2016-07-14"
ms.prod: "azure"
ms.reviewer: ""
ms.service: "media-services"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 635d48e8-c9bd-422a-8cc7-e22376fab7bc
caps.latest.revision: 3
author: "Juliako"
ms.author: "juliako"
manager: "erikre"
---
# MonitoringConfiguration
This topic gives an overview of the Azure Media Services telemetry/monitoring REST types: `MonitoringConfiguration` and `ComponentMonitoringSettings`. These types were added in Media Services version 2.13.  
  
 Media Services telemetry/monitoring allows Media Services customers to access metrics data for its services. The current version supports telemetry data for "Channel" and "StreamingEndpoint" entities. You can configure telemetry on a component level granularity. There are two detail levels "Normal" and "Verbose". The current version only supports "Normal".  
  
 Telemetry is written to a storage table in an Azure  Storage account provided by the customer (the storage account must be attached to the Media Services account). Telemetry system will create a separate table for each new day based at 00:00 UTC. As an example "TelemetryMetrics20160321" where "20160321" is date of table created. For each day there will be a separate table.  
  
 Note that the telemetry system does not manage data retention. You can remove the old telemetry data by deleting the storage tables.  
  
 To enable telemetry for the specified AMS account you have to do the following:  
  
-   Get the credentials of the storage account attached to the Media Services account.  
  
-   Create a Notification Endpoint with EndPointType set to AzureTable (2) and endPontAddress pointing to the storage table (for example, https://telemetryvalidationstore.table.core.windows.net/). For information about how to create notification endpoint see  [NotificationEndPoint](../MediaServicesREST/notificationendpoint.md) topic.  
  
-   Create a monitoring configuration settings for the services you want to monitor. No more than one monitoring configuration settings is allowed. For details, see [Monitoring configuration operations](#MonitoringConfiguration) section.  
  
 For details on how to consume telemetry, see [Consuming telemetry information](#ConsumingTelemetry) section.  
  
> [!IMPORTANT]
>  When working with the Media Services REST API, the following considerations apply:  
>   
>  -   When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](http://msdn.microsoft.com/en-us/42ae6204-93bc-4797-bf40-1c68512cfb73).  
> -   After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
>   
>      For more information, see [Connecting to Media Services with the Media Services REST API](http://msdn.microsoft.com/en-us/426d52db-1ac1-4ede-85be-da8ff5a7973f).  
  
##  <a name="job_entity_properties"></a> MonitoringConfiguration Entity Properties  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|Id<br /><br /> Read-only. Set by Media Services at creation time.|Edm.String|Unique identifier. Format: "nb:mcid:UUID:\<GUID>.|  
|NotificationEndPointId|Edm.String|The notification endpoint ID of the endpoint that you want to associate with this monitoring configuration.|  
|Created<br /><br /> Read-only. Set by Media Services at creation time.|Edm.DateTime|This value is set by Media Services at creation time.|  
|LastModified|Edm.Int32|The last modified time of the item.|  
|Settings|[ComponentMonitoringSettings](#ComponentMonitoringSettings)|The component monitoring settings.|  
  
##  <a name="ComponentMonitoringSettings"></a> ComponentMonitoringSettings  
  
|Property|Type|Description|  
|--------------|----------|-----------------|  
|Component|Edm.String|The monitoring component. Valid values are:<br /><br /> -   Channel (0) - specify to monitor a channel.<br />-   StreamingEndpoint (1) - specify to monitor a streaming endpoint.|  
|Level|Edm.String|The monitoring level. Valid values are:<br /><br /> -   Disabled (0) - output will contain no Monitoring messages.<br />-   Normal (1) - output will contain informational Monitoring messages.<br />-   Verbose(2) - output will contain detailed Monitoring messages.|  
  
##  <a name="MonitoringConfiguration"></a> Monitoring configuration operations  
  
> [!IMPORTANT]
>  After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI.  
  
 To get the latest `x-ms-version:`, see [Media Services REST](../MediaServicesREST/azure-media-services-rest-api-reference.md).  
  
### Get  monitoring configurations  
 **Request**  
  
```  
GET https://wamsbnp1clus001rest-hs.cloudapp.net/api/MonitoringConfigurations HTTP/1.1  
x-ms-version: 2.13  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
Accept: application/json; odata=verbose  
Authorization: (redacted)  
Host: wamsbnp1clus001rest-hs.cloudapp.net  
```  
  
 **Response**  
  
```  
HTTP/1.1 200 OK  
Cache-Control: no-cache  
Content-Length: 20  
Content-Type: application/json;odata=verbose;charset=utf-8  
Server: Microsoft-IIS/8.5  
request-id: 00a3ee37-bb19-4fca-b5c7-a92b629d4416  
x-ms-request-id: 00a3ee37-bb19-4fca-b5c7-a92b629d4416  
X-Content-Type-Options: nosniff  
DataServiceVersion: 3.0;  
access-control-expose-headers: request-id, x-ms-request-id  
X-Powered-By: ASP.NET  
Strict-Transport-Security: max-age=31536000; includeSubDomains  
Date: Wed, 02 Dec 2015 05:10:42 GMT  
{"d":{"results":[]}}  
```  
  
### Add a monitoring configuration  
 **Request**  
  
```  
POST https://wamsbnp1clus001rest-hs.cloudapp.net/api/MonitoringConfigurations HTTP/1.1  
x-ms-version: 2.13  
DataServiceVersion: 3.0  
MaxDataServiceVersion: 3.0  
Accept: application/json; odata=verbose  
Authorization: (redacted)  
Content-Type: application/json; charset=utf-8  
Host: wamsbnp1clus001rest-hs.cloudapp.net  
Content-Length: 133  
{"NotificationEndPointId":"nb:nepid:UUID:76bb4faf-ea29-4815-840a-9a8e20102fc4","Settings":[{"Component":"Channel","Level":"Normal"}]}  
```  
  
 **Response**  
  
```  
HTTP/1.1 201 Created  
Cache-Control: no-cache  
Content-Length: 825  
Content-Type: application/json;odata=verbose;charset=utf-8  
Location: https://wamsbnp1clus001rest-hs.cloudapp.net/api/MonitoringConfigurations('nb%3Amcid%3AUUID%3A1a8931ae-799f-45fd-8aeb-9641740295c2')  
Server: Microsoft-IIS/8.5  
request-id: daede9cb-8684-41b0-a921-a3af66430cbe  
x-ms-request-id: daede9cb-8684-41b0-a921-a3af66430cbe  
X-Content-Type-Options: nosniff  
DataServiceVersion: 3.0;  
access-control-expose-headers: request-id, x-ms-request-id  
X-Powered-By: ASP.NET  
Strict-Transport-Security: max-age=31536000; includeSubDomains  
Date: Wed, 02 Dec 2015 05:10:43 GMT  
{"d":{"__metadata":{"id":"https://wamsbnp1clus001rest-hs.cloudapp.net/api/MonitoringConfigurations('nb%3Amcid%3AUUID%3A1a8931ae-799f-45fd-8aeb-9641740295c2')","uri":"https://wamsbnp1clus001rest-hs.cloudapp.net/api/MonitoringConfigurations('nb%3Amcid%3AUUID%3A1a8931ae-799f-45fd-8aeb-9641740295c2')","type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.MonitoringConfiguration"},"Id":"nb:mcid:UUID:1a8931ae-799f-45fd-8aeb-9641740295c2","NotificationEndPointId":"nb:nepid:UUID:76bb4faf-ea29-4815-840a-9a8e20102fc4","Created":"2015-12-02T05:10:43.7680396Z","LastModified":"2015-12-02T05:10:43.7680396Z","Settings":{"__metadata":{"type":"Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.ComponentMonitoringSettings)"},"results":[{"Component":"Channel","Level":"Normal"},{"Component":"StreamingEndpoint","Level":"Disabled"}]}}}  
```  
  
##  <a name="ConsumingTelemetry"></a> Consuming telemetry information  
 Telemetry is written to an Azure Storage Table in the storage account specified when configuring telemetry for the Media Services account. Telemetry system will create a separate table for each new day based at 00:00 UTC. As an example "TelemetryMetrics20160321" where "20160321" is date of table created. For each day there will be separate table.  
  
 You can query the storage tables for the following metrics information.  
  
### StreamingEndpoint log  
  
|Property|Description|Sample value|  
|--------------|-----------------|------------------|  
|PartitionKey|Gets the partition key of the record. The format is: {account ID}_{service ID}.<br /><br /> The account ID is included in the partition key to simplify workflows where multiple Media Services accounts are writing to the same storage account. It is a combination of accountID_ServiceID|60b71b0f6a0e4d869eb0645c16d708e1_6efed125eef44fb5b61916edc80e6e23|  
|RowKey|Gets the row key of the record. The format is: {seconds to midnight}_{random value}.<br /><br /> The row key starts with the number of seconds to midnight to allow top n style queries within a partition (see [this](https://azure.microsoft.com/en-us/documentation/articles/storage-table-design-guide/#log-tail-pattern) article for details).|00959_00000|  
|Timestamp|The observed time is provided by the entity sending the telemetry (for example a streaming endpoint). There might be clock synchronization problems and this value is approximate. The format is: Date/Time- Auto value from Azure Table(inserted date/time).|3/31/2016 22:50|  
|BytesSent|Aggregated bytes sent.|2987358|  
|E2ELatency|The average end to end latency.|250|  
|HostName|The Streaming Endpoint host name.|builddemoserver.origin.mediaservices.windows.net|  
|Name|The metrics name.|StreamingEndpointRequestLog|  
|ObservedTime|The observed time of the metric.|1/20/16 23:44:01|  
|RequestCount|Total request in the aggregation.|3|  
|ResultCode|The result code.|S_OK|  
|ServerLatency|The server latency (including storage).|0|  
|ServiceId|The entity ServiceID.|6efed125-eef4-4fb5-b619-16edc80e6e23|  
|StatusCode|The HTTP status code.|200|  
|Type|The source entity type.|StreamingEndpoint|  
  
### Live channel heartbeat  
  
|Property|Description|Sample value|  
|--------------|-----------------|------------------|  
|PartitionKey|Gets the partition key of the record. Format is: {account ID}_{service ID}.<br /><br /> The account ID is included in the partition key to simplify workflows where multiple Media Services accounts are writing to the same storage account. It is a combination of accountID_ServiceID|60b71b0f6a0e4d869eb0645c16d708e1_6efed125eef44fb5b61916edc80e6e23|  
|RowKey|Gets the row key of the record. The format is: {seconds to midnight}_{random value}.<br /><br /> The row key starts with the number of seconds to midnight to allow top n style queries within a partition (see [this](https://azure.microsoft.com/en-us/documentation/articles/storage-table-design-guide/#log-tail-pattern) article for details).|00959_00000|  
|Timestamp|The observed time is provided by the entity sending the telemetry (for example a channel). There might be clock synchronization problems and this value is approximate. The format is: Date/Time- Auto value from Azure Table(inserted date/time).|7/18/2016 23:05|  
|Bitrate|The track bitrate.|785000|  
|CustomAttributes|The custom attributes.||  
|DiscontinuityCount|The discontinuity count.|0|  
|IncomingBitrate|The actual incoming bitrate.|784548|  
|LastTimestamp|The last ingested data timestamp.|1800488800|  
|Name|The metrics name.|ChannelHeartbeat|  
|ObservedTime|The observed time of the metric.|1/20/16 23:44:01|  
|OverlapCount|The overlap count in the ingest.|0|  
|ServiceId|The entity ServiceID.|6bf8b8e0-327f-47f3-979c-6b185e0a6a21|  
|TrackType|Type of track video/audio/text.|video|  
|TrackName|The track name.|video|  
|Type|The source entity type.|Channel|  
  
### Additional information  
 The schema is designed to give good performance within the limits of Azure Table Storage. In particular:  
  
-   Data is partitioned by account ID and service ID to allow telemetry from each service to be queried independently.  
  
-   Data is written to different tables for each day in UTC start.  
  
-   Row keys are in reverse time order to allow the most recent telemetry items to be queried for a given service.  
  
 The schema is optimized for many of the common queries to be efficient:  
  
-   Parallel, independent downloading of data for separate services.  
  
-   Retrieving all data for a given service in a date range.  
  
-   Retrieving the most recent data for a service.
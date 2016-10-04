---
title: "Stream Analytics Query Language Reference"
ms.custom: na
ms.date: 2016-04-22
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
applies_to: 
  - Azure
ms.assetid: 0e0c5249-5d88-49b6-a4ec-89a9d57a3885
caps.latest.revision: 14
author: jeffstokes72
manager: jhubbard
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
# Stream Analytics Query Language Reference
  Azure Stream Analytics offers a SQL-like query language for performing transformations and computations over streams of events.  
  
## Stream Analytics Query Language, a subset of T-SQL syntax  
 This document describes the syntax, usage and best practices for the Stream Analytics query language. All the examples used in this document rely on a toll booth scenario as described below.  
  
 Stream Analytics query language is a subset of standard T-SQL syntax for doing Streaming computations.  
  
### The toll booth scenario  
 A tolling station is a common phenomenon – we encounter them in many expressways, bridges, and tunnels across the world. Each toll station has multiple toll booths, which may be manual – meaning that you stop to pay the toll to an attendant, or automated – where a sensor placed on top of the booth scans an RFID card affixed to the windshield of your vehicle as you pass the toll booth. It is easy to visualize the passage of vehicles through these toll stations as an event stream over which interesting operations can be performed.  
  
### Arrival Time Vs Application Time  
 In any temporal system like Azure Stream Analytics, it’s essential to understand the progress of time. Every event that flows through the system comes with a timestamp that can be accessed via [System.Timestamp](../streamAnalyticsQueryLanguage/System.Timestamp---Stream-Analytics-.md). In other words every event in our system depicts a point in time. This timestamp can either be an application time which the user can specify in the query or the system can assign based on arrival time. The arrival time has different meanings based on the input sources.  For the events from Azure Service Bus Event Hub, the arrival time is the timestamp given by the Event Hub; for Blob storage, it is the blob’s last modified time. The timestamp is the point in time that is relevant for capturing or analyzing data. If the user wants to use an application time, they can do so using the [TIMESTAMP BY](../streamAnalyticsQueryLanguage/TIMESTAMP-BY--Azure-Stream-Analytics-.md) keyword. In the above scenario, it is the entry of the vehicle to the toll booth. It is critical to identify the “timestamp” in the incoming stream of data, one should ensure that the time captured also confirms the occurrence of an event. For example, if one is monitoring cash counters and wants to count the number of customers billed, then ideally the event timestamp should be “payment successful” rather than “bill generated” time.  
  
### TIMESTAMP BY  
 In Azure Stream Analytics, all events have a well-defined timestamp. If the user wants to use application time, they can use the TIMESTAMP BY keyword to specify the column in the payload which should be used to timestamp every incoming event to perform any temporal computation like Windowing, Joins etc.  We recommend using TIMESTAMP BY over arrival time as a best practice.  TIMESTAMP BY can be used on any column of type datetime and all ISO 8601 formats are supported. System.timestamp can only be used in [Select](../streamAnalyticsQueryLanguage/SELECT--Azure-Stream-Analytics-.md).  
  
 The following is a TIMESTAMP BY example which uses the EntryTime column as the application time for events:  
  
```  
  
SELECT TollId, EntryTime AS VehicleEntryTime, LicensePlate, State, Make, Model, VehicleType, VehicleWeight, Toll, Tag   
FROM TollTagEntry TIMESTAMP BY EntryTime  
  
```  
  
### Field Name Case Sensitivity  
 All field names referenced in the query are case insensitive. For input formats that support case sensitive schema, for example JSON, you may construct events that has duplicate fields when field names are compared in a case insensitivity manner. Such events are considered invalid events, and are dropped during processing.  
  
## In this section  
 Refer to the following topics for guidance on using the Stream Analytics query language.  
  
-   [Built-in Functions &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/Built-in-Functions--Azure-Stream-Analytics-.md)  
  
-   [Data Types &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/Data-Types--Azure-Stream-Analytics-.md)  
  
-   [Query Language Elements &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/Query-Language-Elements--Azure-Stream-Analytics-.md)  
  
-   [Time Management &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/Time-Management--Azure-Stream-Analytics-.md)  
  
-   [Windowing &#40;Azure Stream Analytics&#41;](../streamAnalyticsQueryLanguage/Windowing--Azure-Stream-Analytics-.md)  
  
## See Also  
  
-   [Stream Analytics REST API](../Topic/Stream%20Analytics%20REST%20API.md)  
  
  
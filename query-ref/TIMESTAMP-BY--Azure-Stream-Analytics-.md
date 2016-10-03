---
title: "TIMESTAMP BY (Azure Stream Analytics)"
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
ms.assetid: 89418f9a-c874-4f25-aa2d-ae066c460ce2
caps.latest.revision: 15
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
# TIMESTAMP BY (Azure Stream Analytics)
  In Azure Stream Analytics, all data stream events have a timestamp associated with them. By default, events are timestamped based on their  arrival time to the input source. For the events from Service Bus Event Hub, the arrival time is the timestamp when the event was received by the Event Hub; for Blob storage, it is the blob’s last modified time.  Note that this means that the timestamp of an event doesn’t change if you re-start or re-run your job.  
  
 Many streaming applications require using the exact timestamp that an event occurred, rather than the arrival time.  For example, in a Point of Sales application one may need event timestamps corresponding to the time a payment was logged, rather than the time a payment event reaches the event ingestor.   Additionally, geo-distributed systems and network latencies may contribute to unpredictable arrival times, making the use of an application time more reliable in a streaming application.  For these cases, the TIMESTAMP BY clause allows specifying custom timestamp values. The value can be any field from the event payload or expression of type **DATETIME**. String values conforming to any of **ISO 8601** formats are also supported.  
  
 Event timestamp can be retrieved in the SELECT statement in any part of the query using [System.Timestamp](../query-ref/System.Timestamp---Stream-Analytics-.md) property.  
  
 Note that using a custom timestamp (TIMESTAMP BY clause) may cause Azure Stream Analytics to ingest events out of order with respect to their timestamps, in other words, events may arrive “late”.  Azure Stream Analytics lets users control how long to wait for late-arriving events and what to do with them when they arrive using policies defined in the Configure tab.  
  
 **Synatax**  
  
```  
TIMESTAMP BY scalar_expression  
  
```  
  
## Examples  
 **Example 1 – Access a timestamp field from the payload**  
  
 Use ‘EntryTime’ field from the payload as event timestamp  
  
```  
  
SELECT  
      EntryTime,  
      LicensePlate,  
      State   
FROM input TIMESTAMP BY EntryTime  
  
```  
  
 **Example 2 – Use UNIX time from the payload as event timestamp**  
  
 UNIX systems often use POSIX (or Epoch) time defined as the number of milliseconds that have elapsed since 00:00:00 Coordinated Universal Time (UTC), Thursday, 1 January 1970.  
  
 This example shows how to use numeric ‘epochtime’ field containing Epoch time as event timestamp.  
  
```  
  
SELECT  
      System.Timestamp,  
      LicensePlate,  
      State  
FROM input TIMESTAMP BY DATEADD(millisecond, epochtime, '1970-01-01T00:00:00Z')  
  
```  
  
 **Example 3 – Heterogeneous timestamps**  
  
 Imagine processing heterogeneous streams of data containing two type of events ‘A’ and ‘B’. Events ‘A’ have timestamp data in the field ‘timestampA’ and events ‘B’ have timestamp in the field ‘timestampB’.  
  
 This example shows how to write TIMESTAMP BY to be able to work with both types of events/timestamps.  
  
```  
  
SELECT  
      System.Timestamp,  
      eventType,  
      eventValue,  
FROM input TIMESTAMP BY  
      (CASE eventType   
            WHEN 'A' THEN timestampA  
            WHEN 'B' THEN timestampB  
      ELSE NULL END)  
  
```  
  
## See Also  
 [System.Timestamp](../query-ref/System.Timestamp---Stream-Analytics-.md)   
 [Time Skew Policies](../query-ref/Time-Skew-Policies--Azure-Stream-Analytics-.md)   
 [Unix Time](https://en.wikipedia.org/wiki/Unix_time)  
  
  
---
title: "Query Language Elements (Azure Stream Analytics)"
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
ms.assetid: a1971269-c7a9-4b62-a3de-b771cc2669e0
caps.latest.revision: 12
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
# Query Language Elements (Azure Stream Analytics)
  Azure Stream Analytics provides a variety of  elements for building queries. They are summarized below.  
  
|Element|Summary|  
|-------------|-------------|  
|[APPLY](../streamAnalyticsQueryLanguage/APPLY--Azure-Stream-Analytics-.md)|The APPLY operator allows you to invoke a table-valued function for each row returned by an outer table expression of a query. There are two forms of APPLY:<br /><br /> CROSS APPLY returns only rows from the outer table that produce a result set from the table-valued function.<br /><br /> OUTER APPLY returns both rows that produce a result set, and rows that do not, with NULL values in the columns produced by the table-valued function.|  
|[CASE](../streamAnalyticsQueryLanguage/CASE--Azure-Stream-Analytics-.md)|CASE evaluates a list of conditions and returns one of multiple possible result expressions|  
|[CREATE TABLE](../streamAnalyticsQueryLanguage/CREATE-TABLE--Stream-Analytics-.md)|CREATE TABLE is used to define the schema of the payload of the events coming into Azure Stream Analytics.|  
|[FROM](../streamAnalyticsQueryLanguage/FROM--Azure-Stream-Analytics-.md)|FROM specifies the input stream or a step name associated in a WITH clause. The FROM clause is **always** required for any SELECT statement.|  
|[GROUP BY](../streamAnalyticsQueryLanguage/GROUP-BY--Azure-Stream-Analytics-.md)|GROUP BY groups a selected set of rows into a set of summary rows grouped by the values of one or more columns or expressions.|  
|[HAVING](../streamAnalyticsQueryLanguage/HAVING--Azure-Stream-Analytics-.md)|HAVING specifies a search condition for a group or an aggregate. HAVING can be used **only** with the SELECT expression.|  
|[INTO](../streamAnalyticsQueryLanguage/INTO--Azure-Stream-Analytics-.md)|INTO explicitly specifies an output stream, and is **always** associated with an SELECT expression.  If not specified, the default output stream is “output”.|  
|[JOIN](../streamAnalyticsQueryLanguage/JOIN--Azure-Stream-Analytics-.md) and<br /><br /> [Reference Data JOIN](../streamAnalyticsQueryLanguage/Reference-Data-JOIN--Azure-Stream-Analytics-.md)|JOIN is used to combine records from two or more input sources.  JOIN is temporal in nature, meaning that each JOIN must define how far the matching rows can be separated in time.<br /><br /> JOIN is also used to   correlate persisted historical data or a slow changing dataset (aka. reference data) with the real-time event stream to make smarter decisions about the system. For example, join an event stream to a static dataset which maps IP Addresses to locations. This is the **only** JOIN supported in Stream Analytics where a temporal bound is not necessary.|  
|[SELECT](../streamAnalyticsQueryLanguage/SELECT--Azure-Stream-Analytics-.md)|SELECT is used to retrieve rows from input streams and enables the selection of one or many columns from one or many input streams in Azure Stream Analytics.|  
|[UNION](../streamAnalyticsQueryLanguage/UNION--Azure-Stream-Analytics-.md)|UNION combines two or more queries into a single result set that includes all the rows that belong to all queries in the union.|  
|[WHERE](../streamAnalyticsQueryLanguage/WHERE--Azure-Stream-Analytics-.md)|WHERE specifies the search condition for the rows returned by the query.|  
|[WITH](../streamAnalyticsQueryLanguage/WITH--Azure-Stream-Analytics-.md)|WITH specifies a temporary named result set which can be referenced by a FROM clause in the query. This is defined within the execution scope of a single SELECT statement.|  
  
## See Also  
 [Built-In Functions](../streamAnalyticsQueryLanguage/Built-in-Functions--Azure-Stream-Analytics-.md)   
 [Data Types](../streamAnalyticsQueryLanguage/Data-Types--Azure-Stream-Analytics-.md)   
 [Time Management](../streamAnalyticsQueryLanguage/Time-Management--Azure-Stream-Analytics-.md)  
  
  
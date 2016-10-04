---
title: "Designing a Scalable Partitioning Strategy for Azure Table Storage"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: bd3c42d9-95fc-4110-abf4-4ba32af33df2
caps.latest.revision: 9
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
# Designing a Scalable Partitioning Strategy for Azure Table Storage
**Author:**  [RBA Consulting](https://msdn.microsoft.com/en-us/library/azure/hh307529.aspx)  
  
 ![Referenced Image](../StorageServicesREST/media/RBALogo.gif "RBALogo")  
  
 Learn more about [RBA Consulting](http://www.rbaconsulting.com).  
  
 **Summary** This article discusses topics related to partitioning an Azure Table and the strategies used to ensure efficient scalability.  
  
 Azure provides cloud storage that is highly available and scalable. The underlying storage system for Azure is provided through a set of services, including the Blob, Table, Queue, and File services. The Azure Table service is designed for storing structured data. The Azure Storage service supports an unlimited number of tables, and each table can scale to massive levels, providing terabytes of physical storage. To take best advantage of tables, you will need to partition your data optimally. This article explores strategies that allow you to efficiently partition data for Azure Table storage.  
  
##  <a name="uyi"></a> Table Entities  
 Table entities represent the units of data stored in a table and are similar to rows in a typical relational database table. Each entity defines a collection of properties. Each property is key/value pair defined by its name, value, and the value's data type. Entities must define the following three system properties as part of the property collection:  
  
-   **PartitionKey** – The PartitionKey property stores string values that identify the partition that an entity belongs to. Partitions, as discussed later, are integral to the scalability of the table. Entities with the same PartitionKey values are stored in the same partition.  
  
-   **RowKey** – The RowKey property stores string values that uniquely identify entities within each partition. The PartitionKey and the RowKey together form the primary key for the entity  
  
-   **Timestamp** – The Timestamp property provides traceability for an entity. A timestamp is a DateTime value that tells you the last time the entity was modified. A timestamp is sometimes referred to as the entity's version. Modifications to timestamps are ignored because the table service maintains the value for this property during all inserts and update operations.  
  
##  <a name="yyy"></a> Table Primary Key  
 The primary key for an Azure entity consists of the combined PartitionKey and RowKey properties,  forming a single clustered index within the table. The PartitionKey and RowKey properties can store up to 1 KB of string values. Empty strings are also permitted; however, null values are not. The clustered index is sorted by the PartitionKey in ascending order and then by RowKey also in ascending order. The sort order is observed in all query responses. Lexical comparisons are used during the sorting operation. Therefore, a string value of "111" will appear before a string value of "2". In some cases, you may want the order to be numeric. To sort in a numeric and ascending order, you will need to use fixed-length, zero-padded strings. In the previous example, using "002" will allow it to appear before "111".  
  
 The clustered index sorts by the PartitionKey in ascending order and then by RowKey in ascending order. The sort order is observed in all query responses. Lexical comparisons are used during the sorting operation. Therefore, a string value of "111" will appear before a string value of "2". In some cases, you may want the order to be numeric. To sort in a numeric and ascending order, you will need to use fixed-length, zero-padded strings. In the previous example, using "002" will allow it to appear before "111".  
  
##  <a name="uyuyuyuyuy"></a> Table Partitions  
 Partitions represent a collection of entities with the same PartitionKey values. Partitions are always served from one partition server and each partition server can serve one or more partitions. A partition server has a rate limit of the number of entities it can serve from one partition over time. Specifically, a partition has a scalability target of 500 entities per second. This throughput may be higher during minimal load on the storage node, but it will be throttled down when the node becomes hot or very active. To better illustrate the concept of partitioning, the following figure illustrates a table that contains a small subset of data for footrace event registrations. It presents a conceptual view of partitioning where the PartitionKey contains three different values comprised of the event's name and distance. In this example, there are two partition servers. Server A contains registrations for the half-marathon and 10 Km distances while Server B contains only the full-marathon distances. The RowKey values are shown to provide context but are not meaningful for this example.  
  
 ![Referenced Screen](../StorageServicesREST/media/AZU_CH03_Figure1.png "AZU_CH03_Figure1")  
A table with three partitions  
  
### Scalability  
 Because a partition is always served from a single partition server and each partition server can serve one or more partitions, the efficiency of serving entities is correlated with the health of the server. Servers that encounter high traffic for their partitions may not be able to sustain a high throughput. For example, in the figure above, if there are many requests for "2011 New York City Marathon__Half", server A may become too hot. To increase the throughput of the server, the storage system load-balances the partitions to other servers. The result is that the traffic is distributed across many other servers. For optimal load balancing of traffic, you should use more partitions, so that  the Azure Table service can distribute the partitions to more partition servers.  
  
### Entity Group Transactions  
 An entity group transaction is a set of storage operations that are implemented atomically on entities with the same PartitionKey value. If any storage operation in the entity group fails, then all the storage operations in it are rolled back. An entity group transaction comprises no more than 100 storage operations and may be no more than 4 MB in size. Entity group transactions provide Azure Table with a limited form of the atomicity, consistency, isolation, durability (ACID) semantics provided by relational databases. Entity group transactions improve throughput since they reduce the number of individual storage operations that must be submitted to the Azure Table service. They also provide an economic benefit since an entity group transaction is billed as a single storage operation regardless of how many storage operations it contains. Since all the storage operations in an entity group transaction affect entities with the same PartitionKey value, a need to use entity group transactions can drive the selection of PartitionKey value.  
  
### Range Partitions  
 If you are using unique PartitionKey values for your entities, then each entity will belong in its own partition. If the unique values you are using are increasing or decreasing in value, it is possible that Azure will create range partitions. Range partitions group entities that have sequential unique PartitionKey values to improve the performance of range queries. Without range partitions, a range query will need to cross partition boundaries or server boundaries, which can decrease the query performance. Consider an application that uses the following table with an increasing sequence value for the PartitionKey.  
  
|||  
|-|-|  
|**PartitionKey**|**RowKey**|  
|"0001"|-|  
|"0002"|-|  
|"0003"|-|  
|"0004"|-|  
|"0005"|-|  
|"0006"|-|  
  
 Azure may group the first three entities into a range partition. If you apply a range query to this table that uses the PartitionKey as the critiera and requests entities from "0001" to "0003,", the query may perform efficiently because they will be served from a single partition server. There is no guarantee when and how a range partition will be created.  
  
 The existence of range partitions for your table can affect the performance of your insert operations if you are inserting entities with increasing, or decreasing, PartitionKey values. Inserting entities with increasing PartitionKey values is called an Append Only pattern, and inserting with decreasing values is called a Prepend Only pattern. You should consider not using such patterns because the overall throughput of your insert requests will be limited by a single partition server. This is because, if range partitions exists, then the first and last (range) partitions will contain the least and greatest PartitionKey values, respectively. Therefore, the insert of a new entity, with a sequentially lower or higher PartitionKey value, will target one of the end partitions. The following figure shows a possible set of range partitions based on the previous example. If a set of "0007", "0008" and "0009" entities were inserted, they would be assigned to the last (orange) partition.  
  
 ![Referenced Screen](../StorageServicesREST/media/AZU_CH03_Figure2.png "AZU_CH03_Figure2")  
Set of range partitions  
  
 It is important to note that there is no negative effect on performance if the insert operations are using more scattered PartitionKey values.  
  
##  <a name="yre"></a> Analyzing Data  
 Unlike a table in relational databases that allow you to manage indexes, Azure tables can only have one index which is always comprised of the PartitionKey and RowKey properties. You are not afforded the luxury of performance-tuning your table by adding more indexes or altering an existing one after you have rolled it out. Therefore, you must analyze the data as you design your table. The most important aspects to consider for optimal scalability and query  and insert efficiency are the PartitionKey and RowKey values. This article places more stress on how to choose the PartitionKey because it directly relates to how tables are partitioned.  
  
###  <a name="dft"></a> Partition Sizing  
 Partition sizing refers to the number of entities a partition contains. As was mentioned in the "Scalability"section, more partitions mean better load balancing. The granularity of the PartitionKey value affects the size of the partitions. At the coarsest level, if a single value is used as the PartitionKey, all the entities are in a single, very large, partition. Alternatively, at the finest level of granularity, the PartitionKey can contain unique values for each entity. The result is that there is a partition for each entity. The following table shows the advantages and disadvantages for the range of granularities.  
  
|||||  
|-|-|-|-|  
|**PartitionKey Granularity**|**Partition Size**|**Advantages**|**Disadvantages**|  
|Single value|Small number of entities|Batch transactions are possible with any entity<br /><br /> All entities are local and served from the same storage node||  
|Single value|Large number of entities|Entity Group Transactions may be possible with any entity. See  [http://msdn.microsoft.com/library/dd894038.aspx](http://msdn.microsoft.com/library/dd894038.aspx)for more information on the limits of entity group transactions|Scaling is limited.<br /><br /> Throughput is limited to the performance of a single server.|  
|Multiple values|There are multiple partitions<br /><br /> Partition sizes depend on entity distribution|Batch transactions are possible on some entities<br /><br /> Dynamic partitioning is possible<br /><br /> Single-request queries possible (no continuation tokens)<br /><br /> Load balancing across more partition servers possible|A highly uneven distribution of entities across partitions may limit the performance of the larger and more active partitions|  
|Unique values|There are many small partitions.|The table is highly scalable<br /><br /> Range partitions may improve the performance of cross-partition range queries|Queries that involve ranges may require visits to more than one server.<br /><br /> Batch transactions are not possible.<br /><br /> Append or prepend-only patterns can affect insert-throughput|  
  
 This table shows how scaling is affected by the PartitionKey values. It is a best practice to favor smaller partitions because they offer better load balancing. Larger partitions may be appropriate in some scenarios, and are not necessarily disadvantageous. For example, if your application does not require scalability, a single large partition may be appropriate.  
  
###  <a name="ytrus"></a> Determining Queries  
 Queries retrieve data from tables. When you analyze the data for an Azure table, it is important to consider which queries the application will use. If an application has several queries, you may need to prioritize them, although your decisions might be somewhat subjective. In many cases, dominant queries are discernable from the other queries. In terms of performance, queries fall into different categories. Because a table only has one index, query performance is usually related to the PartitionKey and RowKey properties. The following table shows the different types of queries and their performance ratings.  
  
|||||  
|-|-|-|-|  
|**Query Type**|**PartitionKey Match**|**RowKey Match**|**Performance Rating**|  
|Point|Exact|Exact|Best|  
|Row range scan|Exact|Partial|Better with smaller-sized partitions<br /><br /> Bad with very large-sized partitions|  
|Partition range scan|Partial|Partial|Good with a small number of partition servers being touched<br /><br /> Worse with more servers being touched|  
|Full table scan|Partial, none|Partial, none|Worse with a subset of partitions being scanned<br /><br /> Worst with all partitions being scanned|  
  
> [!NOTE]
>  The table defines performance ratings relative to each other. The number and size of the partitions may ultimately dictate how the query performs. For example, a partition range scan for a table with many and large partitions may perform poorly compared to a full table scan for a table with few and small partitions.  
  
 The query types listed in this table show a progression from the best types of queries to use to the worst types, based on their performance ratings. Point queries are the best types of queries to use because they fully use the table's clustered index.  The following point query uses the data from the footraces registration table.  
  
```  
http://<account>.windows.core.net/registrations(PartitionKey=”2011 New York City Marathon__Full”,RowKey=”1234__John__M__55”)  
  
```  
  
 If the application uses multiple queries, not all of them can be point queries. In terms of performance, range queries follow point queries. There are two types of range queries: the row range scan and the partition range scan. The row range scan specifies a single partition. Because the operation occurs on a single partition server, row range scans are generally more efficient then partition range scans. However, one key factor in the performance of row range scans is how selective a query is. Query selectivity dictates how many rows must be iterated to find the matching rows. More selective queries are more efficient during row range scans.  
  
 To assess the priorities of your queries, you need to consider the frequency and response time requirements for each query. Queries that are frequently executed may be prioritized higher. However, an important but rarely used query may have low latency requirements that could rank it higher on the priority list.  
  
##  <a name="gdft"></a> Choosing the PartitionKey  
 The core of any table's design is based on its scalability, the queries used to access it, and storage operation requirements. The PartitionKey values you choose will dictate how a table will be partitioned and the type of queries that can be used. Storage operations, in particular inserts, can also affect your choice of PartitionKey values. The PartitionKey values can range from single values to unique values and also can be composed from multiple values. Entity properties can be composed to form the PartitionKey value. Additionally, the application can compute the value.  
  
###  <a name="ttt"></a> Considering Entity Group Transactions  
 Developers should first consider if the application will use entity group transactions (batch updates). Entity group transactions require entities to have the same PartitionKey value. Also, because batch updates are for an entire group, the choices for PartitionKey values can be limited. For example, a banking application that maintains cash transactions must insert cash transactions into the table atomically. This is because cash transactions represent both the debit and the credit sides and must net to zero. This requirement means that the account number cannot be used as any part of the PartitionKey because each side of the transaction uses different account numbers. Instead, a transaction ID may be a more natural choice.  
  
###  <a name="trtr"></a> Considering Partitions  
 Partition numbers and sizes affect the scalability of a table that is under load and are controlled by how granular the PartitionKey values are. It can be challenging to determine the PartitionKey based on the partition size, especially if the distribution of values is hard to predict. A good rule of thumb is to use multiple, smaller partitions. Many table partitions make it easier for the Azure Table service to manage the storage nodes in which the partitions are served from.  
  
 Choosing unique or finer values for the PartitionKey will result in smaller but many partitions. This is generally favorable because the system can load balance the many partitions to distribute the load across many partitions. However, you should consider the effect of having many partitions on cross-partition range queries. These type of queries must visit multiple partitions to satisfy the query. It is possible that the partitions are distributed across many partition servers. If a query crosses a server boundary, continuation tokens must be returned. Continuation tokens specify the next PartitionKey or RowKey values that will retrieve the next set of data for the query. In other words, continuation tokens represent at least one more request to the service which can degrade the overall performance of the query. Query selectivity is another factor that can affect the performance of the query. Query selectivity is a measure of how many rows must be iterated for each partition. The more selective a query is, the more efficient it is at returning the desired rows. The overall performance of range queries may depend on the number of partition servers that must be touched or how selective the query is. You also should avoid using the append or prepend only patterns when inserting data into your table. Using such patterns, despite creating small and many partitions, can limit the throughput of your insert operations. The append and prepend only patterns are discussed in "Range Partitions" section.  
  
###  <a name="r"></a> Considering Queries  
 Knowing the queries that you will be using  will allow you to determine which properties are important to consider for the PartitionKey. The properties that are used in the queries are candidates for the PartitionKey. The following table provides a general guideline of how to determine the PartitionKey.  
  
|||  
|-|-|  
|**If the entity…**|**Action**|  
|Has one key property|Use it as the PartitionKey|  
|Has two key properties|Use one as the PartitionKey and the other as the RowKey|  
|Has more than two key properties|Use a composite key of concatenated values|  
  
 If there is more than one equally dominant query, you can insert the information multiple times with different RowKey values that you need. The secondary (or tertiary, etc) rows will be managed by your application. This pattern will allow you to satisfy the performance requirements of your queries. The following example uses the data from the footrace registration example. It has two dominant queries. They are:  
  
-   Query by bib number  
  
-   Query by age  
  
 To serve both dominant queries, insert two rows as an entity group transaction. The following table shows the Partitionkey and RowKey properties for this scenario. The RowKey values provide a prefix for the bib and age to enable the application to distinguish from the two values.  
  
|||  
|-|-|  
|**PartitionKey**|**RowKey**|  
|2011 New York City Marathon__Full|BIB:01234__John__M__55|  
|2011 New York City Marathon__Full|AGE:055__1234__John__M|  
  
 In this example, an entity group transaction is possible because the PartitionKey values are the same. The group transaction provide atomicity of the insert operation. Although it is possible to use this pattern with different PartitionKey values, it is recommended that you use the same values to gain this benefit. Otherwise, you may have to write extra logic to ensure atomic transactions with different PartitonKey values.  
  
###  <a name="trtrruyu"></a> Considering Storage Operations  
 Azure tables can encounter load not just from queries, but also storage operations such as inserts, updates, and deletes. You need to consider what type of storage operations you will be performing on the table and at what rate. If you are performing these operations infrequently, then you may not need to worry about them. However, for very frequent operations such as performing many inserts in a short period, you will need to consider how those operations are served as a result of the PartitionKey values that you choose. One important example is the append or prepend-only patterns. These patterns were discussed in the previous section "Range Partitions." When the append or prepend-only pattern is used, it means that you are using unique ascending or descending values for the PartitionKey on subsequent insertions. If you combine this pattern with frequent insert operations, then your table will not be able service the insert operations with great scalability. The scalability of your table is affected because Azure will not be able to load balance the operation requests to other partition servers. Therefore, in this case, you may want to consider using values that are random, such as GUID values. This will allow your partition sizes to remain small while maintaining load balancing during storage operations.  
  
##  <a name="trea"></a> Table Partition Stress Testing  
 When the PartitionKey value is complex or requires comparisons to other PartitionKey mappings, you may need to test the table's performance. The test should examine how well a partition performs under peak loads.  
  
 **To perform a stress test**  
  
1.  Create a test table.  
  
2.  Load the test table with data so that it contains entities with the PartitionKey that you will be targeting.  
  
3.  Use the application to simulate peak load to the table, and target a single partition by using the PartitionKey from step 2. This step is different for every application, but the simulation should include all the necessary queries and storage operations. The application may need to be tweaked so that it targets a single partition.  
  
4.  Examine the throughput of the GET or PUT operations on the table.  
  
 To examine the throughput, compare the actual values to the specified limit of a single partition on a single server. Partitions are limited to 500 entities per second. If the throughput exceeds 500 entities per second for a partition, the server may run too hot in a production setting. In this case, the PartitionKey values may be too coarse, so that there are not enough partitions or the partitions are too large. You may need to modify the PartitionKey value so that the partitions can be distributed among more servers.  
  
##  <a name="aserrd"></a> Load Balancing  
 Load balancing at the partition layer occurs when a partition gets too hot, which means the partition, specifically the partition server, is operating beyond its target scalability. For Azure storage, each partition has a scalability target of 500 entities per second. Load balancing also occurs at the Distributed File System layer, or DFS layer. The load balancing at the DFS layer deals with I/O load, and is outside the scope of this article. Load balancing at the partition layer does not immediately occur after exceeding the scalability target. Instead, the system waits a few minutes before beginning the load balancing process. This ensures that a partition has truly become hot. It is not necessary to prime partitions with generated load that triggers load balancing because the system will automatically perform the task. It may be possible that if a table was primed with a certain load, the system will balance the partitions based on actual load, which results in a very different distribution of the partitions. Instead of priming partitions, you should consider writing code that handles the Timeout and Server Busy errors. Such errors are returned when the system is performing load balancing. By handling those errors using a retry strategy, your application can better handle peak load. Retry strategies are discussed in more detail in the following section. When load balancing occurs, the partition will become offline for a few seconds. During the offline period, the system is reassigning the partition to a different partition server. It is important to note that your data is not stored by the partition servers. Instead, the partition servers serve entities from the DFS layer. Because your data is not stored at the partition layer, moving partitions to different servers is a fast process. This greatly limits the period of downtime, if any, that your application may encounter.  
  
##  <a name="qqqq"></a> Using a Retry Strategy  
 It is important for your application to handle storage operation failures to ensure that you do not lose any data updates. Some failures do not require a retry strategy. For example, updates that return a 401 Unauthorized error will not benefit from retrying the operation because it is likely the application state will not change between retries that will resolve the 401 error. However, certain errors, such as Server Busy or Timeout, are related to the load balancing features of Azure that provide table scalability. When the storage nodes serving your entities become hot, Azure will balance the load by moving partitions to other nodes. During this time, the partition may be inaccessible which results in the Server Busy or Timeout errors. Eventually, the partition will be reenabled and updates can resume. A retry strategy is appropriate for busy and timeout errors. In most cases, you can exclude 400-level errors and some 500-level errors from the retry logic, such as 501 Not Implemented or 505 HTTP Version Not Supported, and implement a retry strategy for some 500-level errors, such as Server Busy (503) and Timeout (504).  
  
 There are three common retry strategies that you can use for your application. The following is a list of those retry strategies and their descriptions:  
  
-   No Retry – No retry attempt is made  
  
-   Fixed Backoff – The operation is retried N times with a constant backoff value  
  
-   Exponential Backoff – The operation is retried N times with an exponential backoff value  
  
 The No Retry strategy is a simple (and evasive) way to handle operation failures. However it is not very useful. Not imposing any retry attempts poses obvious risks with data not being stored correctly after failed operations. Therefore, a better strategy is to use the Fixed Backoff strategy that provides the ability to retry operations with the same backoff duration. However, this strategy is not optimized for handling highly scalable tables because if many threads or processes are waiting for the same duration, collisions can occur. The recommended retry strategy is one that uses an exponential backoff where each retry attempt is longer than the last attempt. It is similar to the collision avoidance (CA) algorithm used in computer networks, such as Ethernet. The exponential backoff uses a random factor to provide an additional variance to the resulting interval. The backoff value is then constrained to minimum and maximum limits. The following formula can be used for calculating the next backoff value using an exponential algorithm:  
  
 y = Rand(0.8z, 1.2z)(2<sup>x</sup>-1  
  
 y = Min(zmin + y, zmax  
  
 Where:  
  
 z = default backoff in milliseconds  
  
 zmin = default minimum backoff in milliseconds  
  
 zmax = default maximum backoff in milliseconds  
  
 x = the number of retries  
  
 y = the backoff value in milliseconds  
  
 The 0.8 and 1.2 multipliers used in the Rand (random) function produces a random variance of the default backoff within ±20% of the original value. The ±20% range is acceptable for most retry strategies and prevents further collisions. The formula can be implemented using the following code:  
  
```  
int retries = 1;  
  
// Initialize variables with default values  
var defaultBackoff = TimeSpan.FromSeconds(30);  
var backoffMin = TimeSpan.FromSeconds(3);  
var backoffMax = TimeSpan.FromSeconds(90);  
  
var random = new Random();  
  
double backoff = random.Next(  
    (int)(0.8D * defaultBackoff.TotalMilliseconds),   
    (int)(1.2D * defaultBackoff.TotalMilliseconds));  
backoff *= (Math.Pow(2, retries) - 1);  
backoff = Math.Min(  
    backoffMin.TotalMilliseconds + backoff,   
    backoffMax.TotalMilliseconds);  
  
```  
  
###  <a name="qwr"></a> Using the Storage Client Library  
 If you are developing your application using the Azure Managed Library, you can leverage the included retry policies in the Storage Client Library. The retry mechanism in the library also allows you to extend the functionality with your custom retry policies. The **RetryPolicies** class in the **Microsoft.WindowsAzure.StorageClient** namespace provides static methods that return a RetryPolicy object. The RetryPolicy object is used in conjunction with the **SaveChangesWithRetries** method in the **TableServiceContext** class. The default policy that a TableServiceContext object uses is an instance of a RetryExponential class constructed using the RetryPolicies.DefaultClientRetryCount and RetryPolicies.DefaultClientBackoff values. The following code shows how to construct a TableServiceContext class with a different RetryPolicy.  
  
```  
class MyTableServiceContext : TableServiceContext  
{  
    public MyTableServiceContext(string baseAddress, CloudStorageAccount account)  
        : base(baseAddress, account)  
    {  
        int retryCount = 5; // Default is 3  
        var backoff = TimeSpan.FromSeconds(45); // Default is 30 seconds  
  
        RetryPolicy = RetryPolicies.RetryExponential(retryCount, backoff);  
    }  
    ...  
}  
  
```  
  
##  <a name="qwertyfd"></a> Summary  
 Azure Table Storage allows applications to store a massive amount of data because it manages and reassigns partitions across many storage nodes. You can use data partitioning to control the table’s scalability. Plan ahead when you define a table's schema to ensure efficient partitioning strategies. Specifically, analyze the application’s requirements, data, and queries before you select PartitionKey values. Each partition may be reassigned to different storage nodes as the system responds to traffic. Use a partition stress test to ensure that the table has the correct PartitionKey values. This test will allow you to recognize when partitions are too hot and to make the necessary partition adjustments. To ensure that your application handles intermittent errors and you data is persisted, a retry strategy with backoff should be used. The default retry policy that the Azure Storage Client Library uses is one with an exponential backoff that avoids collisions and maximized the throughput of your application.
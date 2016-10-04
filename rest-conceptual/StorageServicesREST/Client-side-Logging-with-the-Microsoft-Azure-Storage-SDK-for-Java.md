---
title: "Client-side Logging with the Microsoft Azure Storage SDK for Java"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: fd9c3147-3a3f-4708-8c1a-7ea3da353552
caps.latest.revision: 5
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
# Client-side Logging with the Microsoft Azure Storage SDK for Java
For instructions on how to install the binaries for the Microsoft Azure storage libraries in your Java project, see the readme file for the project on GitHub: [https://github.com/Azure/azure-storage-java](https://github.com/Azure/azure-storage-java). This file documents any additional dependencies you must install.  
  
 You must install the optional SLF4J dependency if you are planning to use client-side logging. SLF4J is a logging façade that enables you to use many common Java logging frameworks easily from a client application: for more information about SLF4J, see the [SLF4J user manual](http://www.slf4j.org/manual.html). For a simple test of how to use SLF4J with the storage SDK, place the **slf4j-api** and **slf4j-simple** JAR files in the build path for your storage client project: this will direct all storage log messages to the console.  
  
 The following sample Java code shows how to switch storage client logging off by default by calling the static method **setLoggingEnabledByDefault**, and then use an **OperationContext** object to enable logging for a specific request:  
  
```java  
// Set logging off by default.  
OperationContext.setLoggingEnabledByDefault(false);  
OperationContext ctx = new OperationContext();  
ctx.setLoggingEnabled(true);  
  
// Create an operation to add a new customer to the people table.  
TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);  
  
// Submit the operation to the table service.  
table.execute(insertCustomer1, null, ctx);  
  
```  
  
 The following is a sample of the log messages that slf4j-simple writes to the console:  
  
```  
[main] INFO ROOT - {ceba5ec6...}: {Starting operation.}  
[main] INFO ROOT - {ceba5ec6...}: {Starting operation with location 'PRIMARY' per location mode 'PRIMARY_ONLY'.}  
[main] INFO ROOT - {ceba5ec6...}: {Starting request to 'http://storageaccountname2.table.core.windows.net/people(PartitionKey='Harp',RowKey='Walter')' at 'Tue, 08 Jul 2014 15:07:43 GMT'.}  
[main] INFO ROOT - {ceba5ec6...}: {Writing request data.}  
[main] INFO ROOT - {ceba5ec6...}: {Request data was written successfully.}  
[main] INFO ROOT - {ceba5ec6...}: {Waiting for response.}  
[main] INFO ROOT - {ceba5ec6...}: {Response received. Status code = '204', Request ID = '8f6ce566-3760-4733-a8da-a090e642286a', Content-MD5 = 'null', ETag = 'W/"datetime'2014-07-08T15%3A07%3A41.1177234Z'"'.}  
[main] INFO ROOT - {ceba5ec6...}: {Processing response headers.}  
[main] INFO ROOT - {ceba5ec6...}: {Response headers were processed successfully.}  
[main] INFO ROOT - {ceba5ec6...}: {Processing response body.}  
[main] INFO ROOT - {ceba5ec6...}: {Response body was parsed successfully.}  
[main] INFO ROOT - {ceba5ec6...}: {Operation completed.}  
  
```  
  
 The GUID (ceba5ec6... in the sample) is the client request id assigned to the storage operation by the client-side storage library. For more information about the content of the message contained in the second pair of braces on each line, see the topic .
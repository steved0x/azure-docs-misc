---
title: "Delete Entity1"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
H1: Delete Entity
ms.assetid: e477539a-d36a-49cc-b3be-916a372d9c92
caps.latest.revision: 53
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
# Delete Entity1
The `Delete Entity` operation deletes an existing entity in a table.  
  
## Request  
 The `Delete Entity` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account, `mytable` with the name of your table, and *myPartitionKey* and *myRowKey* with the name of the partition key and row key identifying the entity to be deleted:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`DELETE`|`https://myaccount.table.core.windows.net/mytable(PartitionKey='myPartitionKey', RowKey='myRowKey')`|HTTP/1.1|  
  
 The address of the entity to be updated may take a number of forms on the request URI. See the [OData Protocol](http://www.odata.org/) for additional details.  
  
### Emulated Storage Service URI  
 When making a request against the emulated storage service, specify the emulator hostname and Table service port as `127.0.0.1:10002`, followed by the emulated storage account name:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`DELETE`|`http://127.0.0.1:10002/devstoreaccount1/myentity(PartitionKey='myPartitionKey', RowKey='myRowKey')`|HTTP/1.1|  
  
 The Table service in the storage emulator differs from the Windows® Azure™ Table service in several ways. For more information, see [Differences Between the Storage Emulator and Azure Storage Services](assetId:///c60f2090-c0f4-4817-8559-e98786461dbe).  
  
### URI Parameters  
 None.  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Optional. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`If-Match`|Required. The client may specify the ETag for the entity on the request in order to compare to the ETag maintained by the service for the purpose of optimistic concurrency. The delete operation will be performed only if the ETag sent by the client matches the value maintained by the server, indicating that the entity has not been modified since it was retrieved by the client.<br /><br /> To force an unconditional delete, set `If-Match` to the wildcard character (*).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
### Request Body  
 None.  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 204 (No Content).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md) and [Table Service Error Codes](../StorageServicesREST/Table-Service-Error-Codes.md).  
  
### Response Headers  
 The response includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Table service used to execute the request. This header is returned for requests made against version 2009-09-19 and later.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
### Response Body  
 None.  
  
## Authorization  
 This operation can be performed by the account owner and by anyone with a shared access signature that has permission to perform this operation.  
  
## Remarks  
 When an entity is successfully deleted, the entity is immediately marked for deletion and is no longer accessible to clients. The entity is later removed from the Table service during garbage collection.  
  
 An entity's ETag provides default optimistic concurrency for delete operations. The ETag value is opaque and should not be read or relied upon. Before a delete operation occurs, the Table service verifies that the entity's current ETag value is identical to the ETag value included with the delete request in the `If-Match` header. If the values are identical, the Table service determines that the entity has not been modified since it was retrieved, and the delete operation proceeds.  
  
 If the entity's ETag differs from that specified with the delete request, the delete operation fails with status code 412 (Precondition Failed). This error indicates that the entity has been changed on the server since it was retrieved. To resolve this error, retrieve the entity again and reissue the request.  
  
 To force an unconditional delete operation, set the value of the `If-Match` header to the wildcard character (*) on the request. Passing this value to the operation will override the default optimistic concurrency and ignore any mismatch in ETag values.  
  
 If the `If-Match` header is missing from the request, the service returns status code 400 (Bad Request). A request malformed in other ways may also return 400; for more information, see [Table Service Error Codes](../StorageServicesREST/Table-Service-Error-Codes.md).  
  
 Any application that can authenticate and send an HTTP DELETE request can delete an entity. For more information about constructing a query by using HTTP DELETE, see [How to: Add, Modify, and Delete Entities](http://msdn.microsoft.com/library/dd756368.aspx).  
  
 For information about performing batch delete operations, see [Performing Entity Group Transactions](../StorageServicesREST/Performing-Entity-Group-Transactions.md).  
  
## See Also  
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Setting the OData Data Service Version Headers](../StorageServicesREST/Setting-the-OData-Data-Service-Version-Headers.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Table Service Error Codes](../StorageServicesREST/Table-Service-Error-Codes.md)
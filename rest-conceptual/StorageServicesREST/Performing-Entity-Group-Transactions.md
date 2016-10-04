---
title: "Performing Entity Group Transactions"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: b10963c6-ced3-4fcc-abee-58a9e1c2b83a
caps.latest.revision: 38
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
# Performing Entity Group Transactions
The Table service supports batch transactions on entities that are in the same table and belong to the same partition group. Multiple [Insert Entity](../StorageServicesREST/Insert-Entity.md), [Update Entity](../StorageServicesREST/Update-Entity2.md), [Merge Entity](../StorageServicesREST/Merge-Entity.md), [Delete Entity](../StorageServicesREST/Delete-Entity1.md), [Insert Or Replace Entity](../StorageServicesREST/Insert-Or-Replace-Entity.md), and [Insert Or Merge Entity](../StorageServicesREST/Insert-Or-Merge-Entity.md) operations are supported within a single transaction.  
  
## Requirements for Entity Group Transactions  
 An entity group transaction must meet the following requirements:  
  
-   All entities subject to operations as part of the transaction must have the same `PartitionKey` value.  
  
-   An entity can appear only once in the transaction, and only one operation may be performed against it.  
  
-   The transaction can include at most 100 entities, and its total payload may be no more than 4 MB in size.  
  
-   All entities are subject to the limitations described in [Understanding the Table Service Data Model](../StorageServicesREST/Understanding-the-Table-Service-Data-Model.md).  
  
## Table Service Support for OData Batch Requests  
 The semantics for entity group transactions are defined by the [OData Protocol Specification](http://www.odata.org/). The OData specification defines the following concepts for batch requests:  
  
-   A *change set* is a group of one or more insert, update, or delete operations.  
  
-   A *batch* is a container of operations, including one or more change sets and query operations.  
  
 The Table service supports a subset of the functionality defined by the OData specification:  
  
-   The Table service supports only a single change set within a batch. The change set can include multiple insert, update, and delete operations. If a batch includes more than one change set, the first change set will be processed by the service, and additional change sets will be rejected with status code 400 (Bad Request).  
  
> [!IMPORTANT]
>  Multiple operations against a single entity are not permitted within a change set.  
  
-   Note that a query operation is not permitted within a batch that contains insert, update, or delete operations; it must be submitted singly in the batch.  
  
-   Operations within a change set are processed atomically; that is, all operations in the change set either succeed or fail. Operations are processed in the order they are specified in the change set.  
  
-   The Table service does not support linking operations in a change set.  
  
-   The Table service supports a maximum of 100 operations in a change set.  
  
## Entity Group Transactions via REST  
 The following sections describe how to construct a batch request and how to interpret the batch response, and show samples of each.  
  
### Batch Request Syntax  
 To perform a batch request via REST, specify the `$batch` option on the request URI. For example:  
  
```  
https://myaccount.table.core.windows.net/$batch  
```  
  
 Note that the request URI does not include the table name.  
  
 A batch request is sent to the server with a single POST directive. This request must include the `x-ms-version` header; the header's value must be set to `2009-04-14` or newer.  
  
 The XML payload is a multi-part MIME message containing the batch and the change set. The payload includes two MIME boundaries:  
  
-   A batch boundary encompasses the change set.  
  
-   A change set boundary separates individual insert, update, and delete operations in the batch.  
  
 An individual request within the change set is identical to a request made when that operation is being called by itself. For example:  
  
-   To specify the `If-Match` header on an update, merge, or delete operation, include the header in the set of request headers for the appropriate operation in the change set.  
  
-   To specify the payload format (JSON or ATOM) for each operation in the change set, include the appropriate `Content-Type`, `Accept`, `Version` and `DataServiceVersion` headers, as explained in details in [Payload Format for Table Service Operations](../StorageServicesREST/Payload-Format-for-Table-Service-Operations.md).  
  
-   To suppress the response content echo for the [Insert Entity](../StorageServicesREST/Insert-Entity.md), specify the `Prefer` header with the `return-no-content` value for each insert operation in the change set. For more information about the `Prefer` header, see [Summary of Table Service Functionality](../StorageServicesREST/Summary-of-Table-Service-Functionality.md).  
  
#### Sample Request for Insert, Update, and Delete Operations  
 The following examples show batch requests containing two [Insert Entity](../StorageServicesREST/Insert-Entity.md) operations and a [Merge Entity](../StorageServicesREST/Merge-Entity.md) operation. In these examples, since we are not interested in the echo payload in the response for the insert operations, we include the `Prefer:``return-no-content` header.  
  
> [!NOTE]
>  JSON is the recommended payload format, and is the only format supported for versions 2015-12-11 and later.  
  
##### JSON (versions 2013-08-15 and later)  
 The following example shows a batch request with a JSON payload.  
  
```  
  
POST https://myaccount.table.core.windows.net/$batch HTTP/1.1  
x-ms-version: 2013-08-15  
Accept-Charset: UTF-8  
DataServiceVersion: 3.0;  
MaxDataServiceVersion: 3.0;NetFx  
Content-Type: multipart/mixed; boundary=batch_a1e9d677-b28b-435e-a89e-87e6a768a431  
x-ms-date: Mon, 14 Oct 2013 18:25:49 GMT  
Authorization: SharedKey myaccount:50daR38MtfezvbMdKrGJVN+8sjDSn+AaA=  
Host: 127.0.0.1:10002  
Content-Length: 1323  
Connection: Keep-Alive  
  
--batch_a1e9d677-b28b-435e-a89e-87e6a768a431  
Content-Type: multipart/mixed; boundary=changeset_8a28b620-b4bb-458c-a177-0959fb14c977  
  
--changeset_8a28b620-b4bb-458c-a177-0959fb14c977  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
POST https://myaccount.table.core.windows.net/Blogs HTTP/1.1  
Content-Type: application/json  
Accept: application/json;odata=minimalmetadata  
Prefer: return-no-content  
DataServiceVersion: 3.0;  
  
{"PartitionKey":"Channel_19", "RowKey":"1", "Rating":9, "Text":".NET..."}  
--changeset_8a28b620-b4bb-458c-a177-0959fb14c977  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
POST https://myaccount.table.core.windows.net/Blogs HTTP/1.1  
Content-Type: application/json  
Accept: application/json;odata=minimalmetadata  
Prefer: return-no-content  
DataServiceVersion: 3.0;  
  
{"PartitionKey":"Channel_17", "RowKey":"2", "Rating":9, "Text":"Azure..."}  
--changeset_8a28b620-b4bb-458c-a177-0959fb14c977  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
MERGE https://myaccount.table.core.windows.net/Blogs(PartitionKey='Channel_17', RowKey='3') HTTP/1.1  
Content-Type: application/json  
Accept: application/json;odata=minimalmetadata  
DataServiceVersion: 3.0;  
  
{"PartitionKey":"Channel_19", "RowKey":"3", "Rating":9, "Text":"PDC 2008..."}  
  
--changeset_8a28b620-b4bb-458c-a177-0959fb14c977--  
--batch_a1e9d677-b28b-435e-a89e-87e6a768a431  
  
```  
  
##### Atom Feed (versions prior to 2015-12-11)  
 The following example shows a batch request with an Atom payload.  
  
```  
POST /$batch HTTP/1.1  
User-Agent: Microsoft ADO.NET Data Services  
x-ms-version: 2013-08-15  
x-ms-date: Thu, 30 Aug 2013 20:45:13 GMT  
Authorization: SharedKeyLite myaccount:asOEzsCDS7YEe6oi+bx47KMwbXL0lYZCOlR/oc3FReQ=  
Accept: application/atom+xml,application/xml  
Accept-Charset: UTF-8  
DataServiceVersion: 1.0;NetFx  
MaxDataServiceVersion: 2.0;NetFx  
Content-Type: multipart/mixed; boundary=batch_a1e9d677-b28b-435e-a89e-87e6a768a431  
Host: MyHostName:10002  
Prefer: return-no-content  
Content-Length: ###  
  
--batch_a1e9d677-b28b-435e-a89e-87e6a768a431  
Content-Type: multipart/mixed; boundary=changeset_8a28b620-b4bb-458c-a177-0959fb14c977  
  
--changeset_8a28b620-b4bb-458c-a177-0959fb14c977  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
POST https://myaccount.table.core.windows.net/Blogs HTTP/1.1  
Content-ID: 1  
Content-Type: application/atom+xml;type=entry  
Content-Length: ###  
  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<entry xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">  
  <title />  
  <author>  
    <name />  
  </author>  
  <id />  
  <content type="application/xml">  
    <m:properties>  
      <d:PartitionKey>Channel_19</d:PartitionKey>  
      <d:RowKey>1</d:RowKey>  
      <d:Rating m:type="Edm.Int32">9</d:Rating>  
      <d:Text>.NET...</d:Title>  
    </m:properties>  
  </content>  
</entry>  
--changeset_8a28b620-b4bb-458c-a177-0959fb14c977  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
POST https://myaccount.table.core.windows.net/Blogs HTTP/1.1  
Content-ID: 2  
Content-Type: application/atom+xml;type=entry  
Prefer: return-no-content  
Content-Length: ###  
  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<entry xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">  
  <title />  
  <author>  
    <name />  
  </author>  
  <id />  
  <content type="application/xml">  
    <m:properties>  
      <d:PartitionKey>Channel_19</d:PartitionKey>  
      <d:RowKey>2</d:RowKey>  
      <d:Rating m:type="Edm.Int32">9</d:Rating>  
      <d:Text>Azure...</d:Title>  
    </m:properties>  
  </content>  
</entry>  
--changeset_8a28b620-b4bb-458c-a177-0959fb14c977  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
MERGE https://myaccount.table.core.windows.net/Blogs(PartitionKey='Channel_19', RowKey='3') HTTP/1.1  
Content-ID: 3  
Content-Type: application/atom+xml;type=entry  
Content-Length: ###  
  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<entry xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">  
  <title />  
  <author>  
    <name />  
  </author>  
  <id>https://myaccount.table.core.windows.net/Blogs(PartitionKey='Channel_19',RowKey='3')</id>  
  
  <content type="application/xml">  
    <m:properties>  
      <d:PartitionKey>Channel_19</d:PartitionKey>  
      <d:RowKey>3</d:RowKey>  
      <d:Rating m:type="Edm.Int32">9</d:Rating>  
      <d:Text>PDC 2008...</d:Title>  
    </m:properties>  
  </content>  
</entry>  
--changeset_8a28b620-b4bb-458c-a177-0959fb14c977--  
--batch_a1e9d677-b28b-435e-a89e-87e6a768a431—  
  
```  
  
#### Sample Request for Queries  
 The following examples show a batch request for a query. Note that only a single query may be included in the change set.  
  
> [!NOTE]
>  JSON is the recommended payload format, and is the only format supported for versions 2015-12-11 and later.  
  
##### JSON (versions 2013-08-15 and later)  
 The following example shows a batch request with a JSON payload.  
  
```  
POST https://myaccount.table.core.windows.net/$batch HTTP/1.1  
x-ms-version: 2013-08-15  
Accept-Charset: UTF-8  
DataServiceVersion: 3.0;  
MaxDataServiceVersion: 3.0;NetFx  
Content-Type: multipart/mixed; boundary=batch_f351702c-c8c8-48c6-af2c-91b809c651ce  
x-ms-date: Mon, 14 Oct 2013 19:03:55 GMT  
Authorization: SharedKey testaccount1:y6TxCsXeRiR4l1KqihwRJ05Qb5zBk=  
Host: 127.0.0.1:10002  
Content-Length: 255  
Connection: Keep-Alive  
  
--batch_f351702c-c8c8-48c6-af2c-91b809c651ce  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
GET https://myaccount.table.core.windows.net/Blogs(PartitionKey='Channel_19',RowKey='2') HTTP/1.1  
Accept: application/json;odata=minimalmetadata  
  
--batch_f351702c-c8c8-48c6-af2c-91b809c651ce  
  
```  
  
##### Atom Feed (versions prior to 2015-12-11)  
 The following example shows a batch request with an Atom payload.  
  
```  
POST /$batch HTTP/1.1  
User-Agent: Microsoft ADO.NET Data Services  
x-ms-version: 2013-08-15  
x-ms-date: Thu, 30 Aug 2013 20:45:13 GMT  
Authorization: SharedKeyLite myaccount:asOEzsCDS7YEe6oi+bx47KMwbXL0lYZCOlR/oc3FReQ=  
Accept: application/atom+xml,application/xml  
Accept-Charset: UTF-8  
DataServiceVersion: 3.0;NetFx  
MaxDataServiceVersion: 3.0;NetFx  
Content-Type: multipart/mixed; boundary=batch_f351702c-c8c8-48c6-af2c-91b809c651ce  
Content-Length: ###  
  
--batch_f351702c-c8c8-48c6-af2c-91b809c651ce  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
GET https://myaccount.table.core.windows.net/Blogs(PartitionKey='Channel_19',RowKey='2') HTTP/1.1  
  
--batch_f351702c-c8c8-48c6-af2c-91b809c651ce—  
  
```  
  
### Batch Response Syntax  
 The response returns an overall status code for the batch request, and individual status codes and result fragments for each operation in the change set. The response is a multi-part MIME message that includes a batch boundary and a change set boundary.  
  
 The Table service returns a status code for the entire batch request, and one or more status codes for the operations in the change set, depending on whether they succeeded or failed.  
  
 Assuming that the batch request has been properly authenticated and has been successfully received by the Table service, the batch request returns status code 202 (Accepted), even if one of the operations in the change set fails. If the batch request itself fails, it fails before any operation in the change set is executed. For example, the batch request may fail due to an authentication error, in which case the status code will indicate that failure.  
  
 The operations in a change set are processed atomically; that is, either all operations in the batch succeed, or the entire batch fails. The Table service continues processing operations in the change set until one fails. If an operation fails, all preceding operations in the batch are rolled back. Additionally, entity group transactions execute with snapshot isolation.  
  
 The status code for an individual operation within a change set appears within the change set response. When an individual operation fails, the response for the change set indicates status code 400 (`Bad Request`). Additional error information within the response indicates which operation failed by returning the index of that operation. The index is the sequence number of the command in the payload.  
  
 For an example, see the sample error response below.  
  
#### Sample Response for Create, Update, and Delete Operations  
 The following examples show the responses for the batch operations sent in the sample requests shown above.  
  
##### JSON (versions 2013-08-15 and later)  
 The following example shows a response for a request made with a JSON payload.  
  
```  
HTTP/1.1 202 Accepted  
Cache-Control: no-cache  
Content-Type: multipart/mixed; boundary=batchresponse_e69b1c6c-62ff-471e-ab88-9a4aeef0a880  
Server: Windows-Azure-Table/1.0 Microsoft-HTTPAPI/2.0  
x-ms-request-id: ed9c96eb-9473-4fd9-abf6-fa4dcf0d6295  
x-ms-version: 2013-08-15  
X-Content-Type-Options: nosniff  
Date: Mon, 14 Oct 2013 18:25:49 GMT  
Content-Length: 1647  
  
--batchresponse_e69b1c6c-62ff-471e-ab88-9a4aeef0a880  
Content-Type: multipart/mixed; boundary=changesetresponse_a6253244-7e21-42a8-a149-479ee9e94a25  
  
--changesetresponse_a6253244-7e21-42a8-a149-479ee9e94a25  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
HTTP/1.1 204 No Content  
Content-ID: 1  
X-Content-Type-Options: nosniff  
Cache-Control: no-cache  
Preference-Applied: return-no-content  
DataServiceVersion: 3.0;  
Location: https://myaccount.table.core.windows.net/Blogs(PartitionKey='Channel_19',RowKey='1')  
DataServiceId: https://myaccount.table.core.windows.net/Blogs (PartitionKey='Channel_19',RowKey='1')  
ETag: W/"0x8D101F7E4B662C4"  
  
--changesetresponse_a6253244-7e21-42a8-a149-479ee9e94a25  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
HTTP/1.1 204 No Content  
Content-ID: 2  
X-Content-Type-Options: nosniff  
Cache-Control: no-cache  
Preference-Applied: return-no-content  
DataServiceVersion: 3.0;  
Location: https://myaccount.table.core.windows.net/Blogs (PartitionKey='Channel_19',RowKey='2')  
DataServiceId: https://myaccount.table.core.windows.net/Blogs (PartitionKey='Channel_19',RowKey='2')  
ETag: W/"0x8C134F7A4B692D8"  
  
--changesetresponse_a6253244-7e21-42a8-a149-479ee9e94a25  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
HTTP/1.1 204 No Content  
Content-ID: 3  
X-Content-Type-Options: nosniff  
Cache-Control: no-cache  
DataServiceVersion: 1.0;  
ETag: W/"0x8A541B7C4D699D7"  
  
--changesetresponse_a6253244-7e21-42a8-a149-479ee9e94a25--  
--batchresponse_e69b1c6c-62ff-471e-ab88-9a4aeef0a880--  
  
```  
  
##### Atom Feed (versions prior to 2015-12-11)  
 The following example shows a response for a request made with an Atom payload.  
  
```  
HTTP/1.1 202 Accepted  
Cache-Control: no-cache  
Transfer-Encoding: chunked  
Content-Type: multipart/mixed; boundary=batchresponse_dc0fea8c-ed83-4aa8-ac9b-bf56a2d46dfb  
Server: Windows-Azure-Table/1.0 Microsoft-HTTPAPI/2.0  
x-ms-request-id: b4b49b3e-19a9-4091-a280-da76a09da8d4  
Date: Thu, 30 Aug 2013 20:44:09 GMT  
  
334  
batchresponse_dc0fea8c-ed83-4aa8-ac9b-bf56a2d46dfb   
Content-Type: multipart/mixed; boundary=--changesetresponse_8a28b620-b4bb-458c-a177-0959fb14c977  
  
--changesetresponse_8a28b620-b4bb-458c-a177-0959fb14c977  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
HTTP/1.1 204 No Content  
Content-ID: 1  
Cache-Control: no-cache  
Preference-Applied: return-no-content  
ETag: W/"0x8D101F7E4B662C4"  
Location: https://myaccount.table.core.windows.net/Blogs(PartitionKey='Channel_19',RowKey='1')  
DataServiceVersion: 3.0;  
  
--changesetresponse_8a28b620-b4bb-458c-a177-0959fb14c977  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
HTTP/1.1 204 No Content  
Content-ID: 2  
Cache-Control: no-cache  
Preference-Applied: return-no-content  
ETag: W/"0x8C134F7A4B692D8"  
Location: https://myaccount.table.core.windows.net/Blogs(PartitionKey='Channel_19',RowKey='2')  
DataServiceVersion: 3.0;  
  
--changesetresponse_8a28b620-b4bb-458c-a177-0959fb14c977  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
HTTP/1.1 204 No Content  
Content-ID: 3  
Cache-Control: no-cache  
ETag: W/"0x8A541B7C4D699D7"  
DataServiceVersion: 3.0;  
  
--changesetresponse_8a28b620-b4bb-458c-a177-0959fb14c977--  
--batchresponse_4c637ba4-b2f8-40f8-8856-c2d10d163a83--  
```  
  
#### Sample Response for Queries  
 The following examples show the responses for the queries sent in the sample requests shown above.  
  
##### JSON (versions 2013-08-15 and later)  
 The following example shows a response for a request made with a JSON payload.  
  
```  
HTTP/1.1 202 Accepted  
Cache-Control: no-cache  
Content-Type: multipart/mixed; boundary=batchresponse_0a568496-fb38-4a83-9984-5908d7f4c63d  
Server: Windows-Azure-Table/1.0 Microsoft-HTTPAPI/2.0  
x-ms-request-id: 6f2aafa3-19e9-434c-85f2-d178941c2d4b  
x-ms-version: 2013-08-15  
X-Content-Type-Options: nosniff  
Date: Mon, 14 Oct 2013 19:13:30 GMT  
Content-Length: 615  
  
--batchresponse_0a568496-fb38-4a83-9984-5908d7f4c63d  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
HTTP/1.1 200 OK  
DataServiceVersion: 3.0;  
Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8  
X-Content-Type-Options: nosniff  
Cache-Control: no-cache  
ETag: W/"0x5B168C7B6E589D2"  
  
{"odata.metadata":" https://myaccount.table.core.windows.net/Blogs/$metadata#Blogs/@Element","PartitionKey":"Channel_19","RowKey":"2","Timestamp":"2013-10-14T18:25:49.8922467Z","Rating":9,"Text":"Azure..."}  
--batchresponse_0a568496-fb38-4a83-9984-5908d7f4c63d--  
```  
  
##### Atom Feed (versions prior to 2015-12-11)  
 The following example shows a response for a request made with an Atom payload.  
  
```  
HTTP/1.1 202 Accepted  
Cache-Control: no-cache  
Transfer-Encoding: chunked  
Content-Type: multipart/mixed; boundary=batchresponse_4c637ba4-b2f8-40f8-8856-c2d10d163a83  
Server: Windows-Azure-Table/1.0 Microsoft-HTTPAPI/2.0  
x-ms-request-id: 9202c4a1-43af-4dc0-baca-aa71f7a7407b  
Date: Thu, 30 Aug 2013 20:44:10 GMT  
  
--batchresponse_4c637ba4-b2f8-40f8-8856-c2d10d163a83  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
HTTP/1.1 200 OK  
Content-Type: application/atom+xml;charset=utf-8  
Cache-Control: no-cache  
ETag: W/"0x5B168C7B6E589D2"  
DataServiceVersion: 3.0;  
  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<entry xml:base="http://127.0.0.1:10002/testaccount1/" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" m:etag="W/"0x5B168C7B6E589D2"" xmlns="http://www.w3.org/2005/Atom">  
    <id> https://myaccount.table.core.windows.net/Blogs(PartitionKey='Channel_19',RowKey='1')</id>  
  <title type="text"></title>  
  <updated>2013-08-30T20:44:10Z</updated>  
  <author>  
    <name />  
  </author>  
  <link rel="edit" title="Blogs" href=" Blogs(PartitionKey='Channel_19',RowKey='2')" />  
  <category term="myaccount.Blogs" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />  
  <content type="application/xml">  
    <m:properties>  
      <d:PartitionKey>Channel_19</d:PartitionKey>  
       <d:RowKey>2</d:RowKey>  
       <d:Timestamp m:type="Edm.DateTime">2013-08-30T20:44:09.5789464Z</d:Timestamp>  
       <d:Text>.Net...</d:RowKey>  
      <d:Rating m:type="Edm.Int32">9</d:Rating>  
    </m:properties>  
  </content>  
</entry>  
--batchresponse_4c637ba4-b2f8-40f8-8856-c2d10d163a83--  
  
```  
  
#### Sample Error Response  
 The following examples show responses from batch requests containing an operation that failed. Note that the batch response returns status code 202 (Accepted), but the individual operation that failed returns status code 400 (Bad Request). The additional error information is included in the response body for the failed operation. The `code` element specifies the storage service error code, whereas the `message` element begins with the index of the failed operation, followed by the error message string. To determine which operation failed, parse the index value from the message. Operations are indexed beginning at zero.  
  
##### Error Response for Request in JSON Format  
 In the JSON example, note that the operation that failed was the first operation in the change set. Within the `message` name/value pair, the message begins with the numeral `0`, followed by the extended error information.  
  
```  
HTTP/1.1 202 Accepted  
Cache-Control: no-cache  
Content-Type: multipart/mixed; boundary=batchresponse_4e1c04af-af2b-4cfc-9e35-7677a5efcfca  
Server: Windows-Azure-Table/1.0 Microsoft-HTTPAPI/2.0  
x-ms-request-id: 8abd3c55-a72e-47ba-ae0b-ba43abeb76ae  
x-ms-version: 2013-08-15  
X-Content-Type-Options: nosniff  
Date: Mon, 14 Oct 2013 19:21:58 GMT  
Content-Length: 1051  
  
--batchresponse_4e1c04af-af2b-4cfc-9e35-7677a5efcfca  
Content-Type: multipart/mixed; boundary=changesetresponse_e2a26601-bba8-4c1a-8a8c-bb66badcbca1  
  
--changesetresponse_e2a26601-bba8-4c1a-8a8c-bb66badcbca1  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
HTTP/1.1 400 Bad Request  
Content-ID: 1  
X-Content-Type-Options: nosniff  
DataServiceVersion: 3.0;  
Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8  
  
{"odata.error":{"code":"OutOfRangeInput","message":{"lang":"en-US","value":"0:One of the request inputs is out of range.\nRequestId:8abd3c55-a72e-47ba-ae0b-ba43abeb76ae\nTime:2013-10-14T19:21:58.0890048Z}}}  
--changesetresponse_e2a26601-bba8-4c1a-8a8c-bb66badcbca1--  
--batchresponse_4e1c04af-af2b-4cfc-9e35-7677a5efcfca--  
  
```  
  
##### Error Response for Request in Atom Format  
 In the Atom example, note that the operation that failed was the fourth operation in the change set. Within the `message` element, the message begins with the numeral `3`, followed by the extended error information.  
  
```  
<message xml:lang="en-US">3:One of the request inputs is not valid.</message>  
```  
  
 Here is the complete response:  
  
```  
HTTP/1.1 202 Accepted  
Cache-Control: no-cache  
Transfer-Encoding: chunked  
Content-Type: multipart/mixed; boundary=batchresponse_7ab1553a-7dd6-44e7-8107-bf1ea1ab1876  
Server: Windows-Azure-Table/1.0 Microsoft-HTTPAPI/2.0  
x-ms-request-id: 45ac953e-a4a5-42ba-9b4d-97bf74a8a32e  
Date: Thu, 30 Apr 2009 20:45:13 GMT  
  
6E7  
--batchresponse_7ab1553a-7dd6-44e7-8107-bf1ea1ab1876  
Content-Type: multipart/mixed; boundary=changesetresponse_6cc856b4-8cb9-41eb-b8d2-bb73475c6cec  
  
--changesetresponse_6cc856b4-8cb9-41eb-b8d2-bb73475c6cec  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
HTTP/1.1 400 Bad Request  
Content-ID: 4  
Content-Type: application/xml  
Cache-Control: no-cache  
DataServiceVersion: 1.0;  
  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<error xmlns="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">  
  <code>InvalidInput</code>  
  <message xml:lang="en-US">3:One of the request inputs is not valid.</message>  
</error>  
--changesetresponse_6cc856b4-8cb9-41eb-b8d2-bb73475c6cec--  
--batchresponse_7ab1553a-7dd6-44e7-8107-bf1ea1ab1876--  
  
```  
  
## See Also  
 [OData Specification](http://www.odata.org/)   
 [Table Service Concepts](../StorageServicesREST/Table-Service-Concepts.md)
---
title: "Service SAS Examples"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 4acc4449-8967-4701-bab5-c13f18fa7d7d
caps.latest.revision: 11
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
# Service SAS Examples
This topic shows sample uses of shared access signatures with the REST API. Shared access signatures permit you to provide access rights to containers and blobs, tables, queues, or files. By providing a shared access signature, you can grant users restricted access to a specific container, blob, queue, table, or table entity range for a specified period of time. For complete details on constructing, parsing, and using shared access signatures, see [Delegating Access with a Shared Access Signature](../StorageServicesREST/Delegating-Access-with-a-Shared-Access-Signature.md). For information about using the .NET storage client library to create shared access signatures, see [Create and Use a Shared Access Signature](assetId:///b41f98e9-14ab-499a-9fd2-fb9202c9ccd2).  
  
## Blob Examples  
 This section contains examples that demonstrate shared access signatures for REST operations on blobs.  
  
### Example: Get a Blob using a Container’s Shared Access Signature  
 **Versions Prior to 2013-08-15**  
  
 The following example shows how to construct a shared access signature for read access on a container.  
  
 The signed signature fields that will comprise the URL include:  
  
```  
  
signedstart=2009-02-09  
signedexpiry=2009-02-10  
signedresource=c  
signedpermissions=r  
signature=dD80ihBh5jfNpymO5Hg1IdiJIEvHcJpCMiCMnN/RnbI=  
signedidentifier=YWJjZGVmZw==  
signedversion=2012-02-12  
  
```  
  
 The signature is constructed as follows:  
  
```  
  
StringToSign = r + \n   
               2009-02-09 + \n  
               2009-02-10 + \n  
               /myaccount/pictures + \n  
               YWJjZGVmZw== + \n  
               2012-02-12  
  
HMAC-SHA256(URL.Decode(UTF8.Encode(StringToSign))) = dD80ihBh5jfNpymO5Hg1IdiJIEvHcJpCMiCMnN/RnbI=  
  
```  
  
 The request URL specifies read permissions on the `pictures` container for the designated interval. Note that the resource represented by the request URL is a blob, but the shared access signature is specified on the container. It's also possible to specify it on the blob itself.  
  
```  
GET https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2012-02-12&st=2009-02-09&se=2009-02-10&sr=c&sp=r&si=YWJjZGVmZw%3d%3d&sig=dD80ihBh5jfNpymO5Hg1IdiJIEvHcJpCMiCMnN%2fRnbI%3d   
HTTP/1.1  
Host: myaccount.blob.core.windows.net  
x-ms-date: <date>  
  
```  
  
 **Version 2013-08-15 and Later**  
  
 The following example shows how to construct a shared access signature for read access on a container using version 2013-08-15 of the storage services.  
  
 Version 2013-08-15 introduces new query parameters that enable the client issuing the request to override response headers for this shared access signature only.  
  
 The response headers and corresponding query parameters are as follows:  
  
|Response header name|Corresponding SAS query parameter|  
|--------------------------|---------------------------------------|  
|`Cache-Control`|`rscc`|  
|`Content-Disposition`|`rscd`|  
|`Content-Encoding`|`rsce`|  
|`Content-Language`|`rscl`|  
|`Content-Type`|`rsct`|  
  
 The fields that comprise the string-to-sign for the signature include:  
  
```  
signedstart=2013-08-16  
signedexpiry=2013-08-17  
signedresource=c  
signedpermissions=r  
signature=dD80ihBh5jfNpymO5Hg1IdiJIEvHcJpCMiCMnN/RnbI=  
signedidentifier=YWJjZGVmZw==  
signedversion=2013-08-15  
responsecontent-disposition=file; attachment  
responsecontent-type=binary  
```  
  
 The string-to-sign is constructed as follows:  
  
```  
StringToSign = r + \n   
               2013-08-16 + \n  
               2013-08-17 + \n  
               /myaccount/pictures + \n  
               YWJjZGVmZw== + \n  
               2013-08-15 + \n  
               + \n    
               file; attachment + \n  
               + \n  
               + \n  
               binary  
  
HMAC-SHA256(URL.Decode(UTF8.Encode(StringToSign))) = a39+YozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ=  
```  
  
 The shared access signature specifies read permissions on the **pictures** container for the designated interval. Note that the resource represented by the request URL is a blob, but the shared access signature is specified on the container. It's also possible to specify it on the blob itself.  
  
```  
GET https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d HTTP/1.1  
  
```  
  
 For a client making a request with this signatures, the [Get Blob](../StorageServicesREST/Get-Blob.md) operation will be executed if the following criteria are met:  
  
-   The signature in the request successfully authenticates against the storage account.  
  
-   The request is made within the time frame specified by the shared access signature.  
  
-   The request does not violate any term of an associated stored access policy.  
  
-   The blob specified by the request (**/myaccount/pictures/profile.jpg**) resides within the container specified as the signed resource (**/myaccount/pictures**).  
  
 Note that specifying `rsct=binary` and `rscd=file; attachment` on the shared access signature overrides the content-type and content-disposition headers in the response, respectively.  
  
 A successful response for a request made using this shared access signature will be similar to the following:  
  
```  
Status Response:  
HTTP/1.1 200 OK  
  
Response Headers:  
x-ms-blob-type: BlockBlob  
Content-Length: 11  
Content-Type: binary  
Content-Disposition: file; attachment  
ETag: "0x8CB171DBEAD6A6B"  
x-ms-version: 2013-08-15  
Server: Windows-Azure-Blob/1.0 Microsoft-HTTPAPI/2.0  
```  
  
### Example: Upload a Blob using a Container’s Shared Access Signature  
 The following example shows how to construct a shared access signature for writing a blob. In this example, we construct a signature that grants write permissions for all blobs in the container. Then we use the shared access signature to write to a blob in the container.  
  
 The signed signature fields that will comprise the URL include:  
  
```  
  
signedstart=2015-07-01T08:49Z  
signedexpiry=2015-07-02T08:49Z  
signedresource=c  
signedpermissions=w  
signature= Rcp6gQRfV7WDlURdVTqCa+qEArnfJxDgE+KH3TCChIs=  
signedidentifier=YWJjZGVmZw==  
signedversion=2015-02-21  
  
```  
  
 The signature is constructed as follows:  
  
```  
  
StringToSign = w + \n   
               2015-07-01T08:49Z + \n  
               2015-07-02T08:49Z + \n  
               /myaccount/pictures + \n  
               YWJjZGVmZw== + \n  
               2013-08-15  
  
HMAC-SHA256(URL.Decode(UTF8.Encode(StringToSign))) = Rcp6gQRfV7WDlURdVTqCa+qEArnfJxDgE+KH3TCChIs=  
  
```  
  
 The request URL specifies write permissions on the `pictures` container for the designated interval. Note that the resource represented by the request URL is a blob, but the shared access signature is specified on the container. It's also possible to specify it on the blob itself.  
  
```  
PUT https://myaccount.blob.core.windows.net/pictures/photo.jpg?sv=2015-02-21&st=2015-07-01T08%3a49Z&se=2015-07-02T08%3a49Z&  
sr=c&sp=w&si=YWJjZGVmZw%3d%3d&sig=Rcp6gQRfV7WDlURdVTqCa%2bqEArnfJxDgE%2bKH3TCChIs%3d HTTP/1.1  
Host: myaccount.blob.core.windows.net  
  
Content-Length: 12  
  
Hello World.  
  
```  
  
 With this signature, [Put Blob](../StorageServicesREST/Put-Blob.md) will be called if the following criteria are met:  
  
-   The signature in the request successfully authenticates against the storage account.  
  
-   The request is made within the time frame specified by the shared access signature.  
  
-   The request does not violate any term of an associated stored access policy.  
  
-   The blob specified by the request (/myaccount/pictures/photo.jpg) is in the container specified as the signed resource (/myaccount/pictures).  
  
### Example: Delete Blob using a Blob’s Shared Access Signature  
 The following example shows how to construct a shared access signature that grants delete permissions for a blob, and deletes a blob.  
  
> [!CAUTION]
>  Note that a shared access signature for a DELETE operation should be distributed judiciously, as permitting a client to delete data may have unintended consequences.  
  
 The signed signature fields that will comprise the URL include:  
  
```  
  
signedstart=2015-07-01T08:49:37.0000000Z  
signedexpiry=2015-07-02T08:49:37.0000000Z  
signedresource=b  
signedpermissions=d  
signature=+SzBm0wi8xECuGkKw97wnkSZ/62sxU+6Hq6a7qojIVE=  
signedidentifier=YWJjZGVmZw==  
signedversion=2015-02-21  
  
```  
  
 The signature is constructed as follows:  
  
```  
  
StringToSign = d + \n   
               2015-07-01T08:49:37.0000000Z + \n  
               2015-07-02T08:49:37.0000000Z + \n  
               blob/myaccount/pictures/profile.jpg + \n  
               YWJjZGVmZw==  
               2015-02-21  
  
HMAC-SHA256(URL.Decode(UTF8.Encode(StringToSign))) = +SzBm0wi8xECuGkKw97wnkSZ/62sxU+6Hq6a7qojIVE=  
  
```  
  
 The request URL specifies delete permissions on the pictures container for the designated interval. Note that the resource represented by the request URL is a blob, and the shared access signature is specified on that blob. It's also possible to specify it on the blob’s container to grant permission to delete any blob in the container.  
  
```  
  
DELETE https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2015-02-21&st=2015-07-01T08%3a49%3a37.0000000Z&se=2015-07-02T08%3a49%3a37.0000000Z&sr=b&sp=d&si=YWJjZGVmZw%3d%3d&sig=%2bSzBm0wi8xECuGkKw97wnkSZ%2f62sxU%2b6Hq6a7qojIVE%3d HTTP/1.1  
Host: myaccount.blob.core.windows.net  
Content-Length: 0  
  
```  
  
 With this signature, [Delete Blob](../StorageServicesREST/Delete-Blob.md) will be called if the following criteria are met:  
  
-   The signature in the request successfully authenticates against the storage account.  
  
-   The request is made within the time frame specified by the shared access signature.  
  
-   The request does not violate any term of an associated stored access policy.  
  
-   The blob specified by the request (/myaccount/pictures/profile.jpg) matches the blob specified as the signed resource.  
  
## File Examples  
 This section contains examples that demonstrate shared access signatures for REST operations on files.  
  
### Example: Get a File using a Share’s Shared Access Signature  
 The following example shows how to construct a shared access signature for read access on a share.  
  
 Few query parameters can enable the client issuing the request to override response headers for this shared access signature.  
  
 The response headers and corresponding query parameters are as follows:  
  
|Response header name|Corresponding SAS query parameter|  
|--------------------------|---------------------------------------|  
|`Cache-Control`|rscc|  
|`Content-Disposition`|rscd|  
|`Content-Encoding`|rsce|  
|`Content-Language`|rscl|  
|`Content-Type`|rsct|  
  
 The fields that comprise the string-to-sign for the signature include:  
  
```  
signedstart=2015-07-01T08:49Z  
signedexpiry=2015-07-02T08:49Z  
signedresource=c  
signedpermissions=r  
signature=dD80ihBh5jfNpymO5Hg1IdiJIEvHcJpCMiCMnN/RnbI=  
signedidentifier=YWJjZGVmZw==  
signedversion=2015—02-21  
responsecontent-disposition=file; attachment  
responsecontent-type=binary  
```  
  
 The string-to-sign is constructed as follows:  
  
```  
StringToSign = r + \n   
               2015-07-01T08:49Z + \n  
               2015-07-02T08:49Z + \n  
               file/myaccount/pictures + \n  
               YWJjZGVmZw== + \n  
               2015—02-21 + \n  
               + \n    
               file; attachment + \n  
               + \n  
               + \n  
               binary  
  
HMAC-SHA256(URL.Decode(UTF8.Encode(StringToSign))) = a39+YozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ=  
```  
  
 The shared access signature specifies read permissions on the `pictures` share for the designated interval. Note that the resource represented by the request URL is a file, but the shared access signature is specified on the share. It's also possible to specify it on the file itself.  
  
```  
GET https://myaccount.file.core.windows.net/pictures/profile.jpg?sv=2015-02-21&st=2015-07-01T08:49Z&se=2015-07-02T08:49Z&sr=c&sp=r&rscd=file;%20attachment&rsct=binary&sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d  
  
```  
  
 For a client making a request with this signature, the [Get File](../StorageServicesREST/Get-File.md) operation will be executed if the following criteria are met:  
  
-   The signature in the request successfully authenticates against the storage account.  
  
-   The request is made within the time frame specified by the shared access signature.  
  
-   The request does not violate any term of an associated stored access policy.  
  
-   The file specified by the request **(/myaccount/pictures/profile.jpg**) resides within the share specified as the signed resource **(/myaccount/pictures**).  
  
 Note that specifying `rsct=binary` and `rscd=file; attachment` on the shared access signature overrides the `content-type` and `content-disposition` headers in the response, respectively.  
  
 A successful response for a request made using this shared access signature will be similar to the following:  
  
```  
Status Response:  
HTTP/1.1 200 OK  
  
Response Headers:  
Content-Length: 11  
Content-Type: binary  
Content-Disposition: file; attachment  
ETag: "0x8CB171DBEAD6A6B"  
x-ms-version: 2015-02-21  
Server: Windows-Azure-Blob/1.0 Microsoft-HTTPAPI/2.0  
```  
  
### Example: Upload a File using a Shared Access Signature on a Share  
 The following example shows how to construct a shared access signature for writing a file. In this example, we construct a signature that grants write permissions for all files in the share. Then we use the shared access signature to write to a file in the share.  
  
 The signed signature fields that will comprise the URL include:  
  
```  
signedstart2015-07-01T08:49Z  
signedexpiry=2015-07-02T08:49Z  
signedresource=c  
signedpermissions=w  
signature= Rcp6gQRfV7WDlURdVTqCa+qEArnfJxDgE+KH3TCChIs=  
signedidentifier=YWJjZGVmZw==  
signedversion=2015-02-21  
```  
  
 The signature is constructed as follows:  
  
```  
StringToSign = w + \n   
               2015-07-01T08:49Z + \n  
               2015-07-02T08:49Z + \n  
               file/myaccount/pictures + \n  
               YWJjZGVmZw== + \n  
               2015-02-21  
  
HMAC-SHA256(URL.Decode(UTF8.Encode(StringToSign))) = Rcp6gQRfV7WDlURdVTqCa+qEArnfJxDgE+KH3TCChIs=  
```  
  
 The request URL specifies write permissions on the `pictures` container for the designated interval. Note that the resource represented by the request URL is a blob, but the shared access signature is specified on the container. It's also possible to specify it on the blob itself.  
  
```  
PUT https://myaccount.file.core.windows.net/pictures/photo.jpg?sv=2015-02-21&st=2015-07-01T08%3a49Z&se=2015-07-01T08%3a49Z&  
sr=c&sp=w&si=YWJjZGVmZw%3d%3d&sig=Rcp6gQRfV7WDlURdVTqCa%2bqEArnfJxDgE%2bKH3TCChIs%3d HTTP/1.1  
Host: myaccount.blob.core.windows.net  
Content-Length: 12  
  
Hello World.  
```  
  
 With this signature, [Upload File](../Topic/Upload%20File.md) will be called if the following criteria are met:  
  
-   The signature in the request successfully authenticates against the storage account.  
  
-   The request is made within the time frame specified by the shared access signature.  
  
-   The request does not violate any term of an associated stored access policy.  
  
-   The file specified by the request (/myaccount/pictures/photo.jpg) is in the share specified as the signed resource (/myaccount/pictures).  
  
### Example: Delete File using a File’s Shared Access Signature  
 The following example shows how to construct a shared access signature that grants delete permissions for a file, then uses the shared access signature to delete the file.  
  
> [!CAUTION]
>  A shared access signature for a DELETE operation should be distributed judiciously, as permitting a client to delete data may have unintended consequences.  
  
 The signed signature fields that will comprise the URL include:  
  
```  
signedstart=2015-07-01T08:49:37.0000000Z  
signedexpiry=2015-07-02T08:49:37.0000000Z  
signedresource=b  
signedpermissions=d  
signature=+SzBm0wi8xECuGkKw97wnkSZ/62sxU+6Hq6a7qojIVE=  
signedidentifier=YWJjZGVmZw==  
signedversion=2015-02-21  
```  
  
 The signature is constructed as follows:  
  
```  
StringToSign = d + \n   
               2015-07-01T08:49:37.0000000Z + \n  
               2015-07-02T08:49:37.0000000Z + \n  
               file/myaccount/pictures/profile.jpg + \n  
               YWJjZGVmZw==  
               2015-02-21  
  
HMAC-SHA256(URL.Decode(UTF8.Encode(StringToSign))) = +SzBm0wi8xECuGkKw97wnkSZ/62sxU+6Hq6a7qojIVE=  
```  
  
 The request URL specifies delete permissions on the pictures share for the designated interval. Note that the resource represented by the request URL is a file, and the shared access signature is specified on that file. It's also possible to specify it on the file’s share to grant permission to delete any file in the share.  
  
```  
DELETE https://myaccount.file.core.windows.net/pictures/profile.jpg?sv=2015-02-21&st=2015-07-01T08%3a49%3a37.0000000Z&se=2015-07-02T08%3a49%3a37.0000000Z&sr=b&sp=d&si=YWJjZGVmZw%3d%3d&sig=%2bSzBm0wi8xECuGkKw97wnkSZ%2f62sxU%2b6Hq6a7qojIVE%3d HTTP/1.1  
Host: myaccount.blob.core.windows.net  
Content-Length: 0  
```  
  
 With this signature, [Delete File](../StorageServicesREST/Delete-File2.md) will be called if the following criteria are met:  
  
-   The signature in the request successfully authenticates against the storage account.  
  
-   The request is made within the time frame specified by the shared access signature.  
  
-   The request does not violate any term of an associated stored access policy.  
  
-   The file specified by the request (/myaccount/pictures/profile.jpg) matches the file specified as the signed resource.  
  
## Queue Examples  
 This section contains examples that demonstrate shared access signatures for REST operations on queues. In these examples, the Queue service operation only runs after the following criteria are met:  
  
-   The signature in the request successfully authenticates against the storage account.  
  
-   The request is made within the time frame specified by the shared access signature.  
  
-   The request does not violate any term of an associated stored access policy.  
  
-   The queue specified by the request is the same queue authorized by the shared access signature.  
  
### Example: Retrieve Messages using a Shared Access Signature  
 The following example shows how to construct a shared access signature for retrieving messages from a queue. This signature grants message processing permissions for the queue. Finally, this example uses the shared access signature to retrieve a message from the queue.  
  
 Examine the following signed signature fields, the construction of the StringToSign string, and the construction of the URL that calls the Get Messages operation after the shared access signature authenticates:  
  
```  
signedstart=2015-07-01T08:49Z  
signedexpiry=2015-07-02T08:49Z  
signedpermissions=p  
signature=+SzBm0wi8xECuGkKw97wnkSZ/62sxU+6Hq6a7qojIVE=  
signedidentifier=YWJjZGVmZw==   
signedversion=2015-02-21  
  
StringToSign = p + \n   
               2015-07-01T08:49Z + \n  
               2015-07-02T08:49Z + \n  
               queue/myaccount/myqueue + \n  
               YWJjZGVmZw== + \n  
               2015-02-21  
  
GET https://myaccount.queue.core.windows.net/myqueue/messages?visibilitytimeout=120&sv=2015-02-21&st=2015-07-01T08%3a49Z&se=2015-07-02T08%3a49Z&sp=p&si=YWJjZGVmZw%3d%3d&sig=jDrr6cna7JPwIaxWfdH0tT5v9dc%3d HTTP/1.1  
Host: myaccount.queue.core.windows.net  
  
```  
  
### Example: Add a Message using a Shared Access Signature  
 The following example shows how to construct a shared access signature for adding a message to a queue. This signature grants add permissions for the queue. Finally, this example uses the signature to add a message.  
  
 Examine the following signed signature fields, the construction of the StringToSign string, and the construction of the URL that calls the Put Message operation after the shared access signature authenticates:  
  
```  
signedstart=2015-07-01T08:49Z  
signedexpiry=2015-07-02T08:49Z  
signedpermissions=a  
signature= +SzBm0wi8xECuGkKw97wnkSZ/62sxU+6Hq6a7qojIVE=  
signedidentifier=YWJjZGVmZw==   
signedversion=2015-02-21  
  
StringToSign = a + \n   
               2015-07-01T08:49Z + \n  
               2015-07-02T08:49Z + \n  
               queue/myaccount/myqueue + \n  
               YWJjZGVmZw== + \n  
               2015-02-21  
  
POST https://myaccount.queue.core.windows.net/myqueue/messages?visibilitytimeout=120&sv=2015-02-21&st=2015-07-01T08%3a49Z&se=2015-07-02T08%3a49Z&sp=a&si=YWJjZGVmZw%3d%3d&sig=jDrr6cna7JPwIaxWfdH0tT5v9dc%3d HTTP/1.1  
Host: myaccount.queue.core.windows.net  
Content-Length: 100  
  
<QueueMessage>  
<MessageText>PHNhbXBsZT5zYW1wbGUgbWVzc2FnZTwvc2FtcGxlPg==</MessageText>  
</QueueMessage>  
  
```  
  
### Example: Peek at Messages and Get a Message using a Shared Access Signature  
 The following example shows how to construct a shared access signature for peeking at the next message in a queue and retrieving the message count of the queue. This signature grants read permissions for the queue. Finally, this example uses the shared access signature to peek at a message and then read the queues metadata, which includes the message count.  
  
 Examine the following signed signature fields, the construction of the string-to-sign, and the construction of the URL that calls the [Peek Messages](../StorageServicesREST/Peek-Messages.md) and [Get Queue Metadata](../StorageServicesREST/Get-Queue-Metadata.md) operations:  
  
```  
signedstart=2015-07-01T08:49Z  
signedexpiry=2015-07-02T08:49Z  
signedpermissions=r  
signature=+SzBm0wi8xECuGkKw97wnkSZ/62sxU+6Hq6a7qojIVE=  
signedidentifier=YWJjZGVmZw==   
signedversion=2015-02-21  
  
StringToSign = r + \n   
               2015-07-01T08:49Z + \n  
               2015-07-02T08:49Z + \n  
               queue/myacccount/myqueue + \n  
               YWJjZGVmZw== + \n  
               2015-02-21  
  
GET https://myaccount.queue.core.windows.net/myqueue/messages?peekonly=true&sv=2015-02-21&st=2015-07-01T08%3a49Z&se=2015-07-02T08%3a49Z&sp=r&si=YWJjZGVmZw%3d%3d&sig=jDrr6cna7JPwIaxWfdH0tT5v9dc%3d HTTP/1.1  
Host: myaccount.queue.core.windows.net  
  
GET https://myaccount.queue.core.windows.net/myqueue?comp=metadata&sv=2015-02-21&st=2015-07-01T08%3a49Z&se=2015-07-01T08%3a49Z&sp=r&si=YWJjZGVmZw%3d%3d&sig=jDrr6cna7JPwIaxWfdH0tT5v9dc%3d HTTP/1.1  
Host: myaccount.queue.core.windows.net  
  
```  
  
## Table Examples  
 This section contains examples that demonstrate shared access signatures for REST operations on tables. In these examples, the Table service operation only runs after the following criteria are met:  
  
-   The signature in the request successfully authenticates against the storage account.  
  
-   The request is made within the time frame specified by the shared access signature.  
  
-   The request does not violate any term of an associated stored access policy.  
  
-   The queue specified by the request is the same queue authorized by the shared access signature.  
  
### Example: Query a Table using a Shared Access Signature  
 The following example shows how to construct a shared access signature for querying entities in a table. The signature grants query permissions for a specific range in the table. Finally, this example uses the shared access signature to query entities within the range.  
  
 Examine the following signed signature fields, the construction of the StringToSign string, and the construction of the URL that calls the Query Entities operation. The results of this Query Entities operation will only include entities in the range defined by `startpk`, `startrk`, `endpk`, and `endrk`.  
  
```  
signedstart=2015-07-01T08:49Z  
signedexpiry=2015-07-02T08:49Z  
signedpermissions=r  
signature= +SzBm0wi8xECuGkKw97wnkSZ/62sxU+6Hq6a7qojIVE=  
signedidentifier=YWJjZGVmZw==   
signedversion=2015-02-21  
startpk="Coho Winery"  
startrk="Auburn"  
endpk="Coho Winery"  
endrk="Seattle"  
  
String-To-Sign = r + \n   
                 2015-07-01T08:49Z + \n  
                 2015-07-02T08:49Z + \n  
                 table/myaccount/mytable + \n  
                 YWJjZGVmZw==  + \n  
                 2015-02-21 + \n  
                 Coho Winery + \n  
                 Auburn + \n  
                 Coho Winery + \n  
                 Seattle  
  
GET https://myaccount.table.core.windows.net/MyTable?$filter=PartitionKey%20eq%20'Coho%20Winery'&sv=2015-02-21&tn=MyTable&st=2015-07-01T08%3a49Z&se=2015-07-02T08%3a49Z&sp=r&si=YWJjZGVmZw%3d%3d&sig=jDrr6cna7JPwIaxWfdH0tT5v9dc%3d&spk=Coho%20Winery&srk=Auburn&epk=Coho%20Winery&erk=Seattle HTTP/1.1  
Host: myaccount.table.core.windows.net  
DataServiceVersion: 1.0;NetFx  
MaxDataServiceVersion: 2.0;NetFx  
  
```  
  
### Example: Update a Table using a Shared Access Signature  
 The following example shows how to construct a shared access signature for updating entities in a table. The signature grants update permissions for a specific range of entities. Finally, this example uses the shared access signature to update an entity in the range.  
  
 Examine the following signed signature fields, the construction of the StringToSign string, and the construction of the URL that calls the Update Entity operation. The Update Entity operation can only update entities within the partition range defined by `startpk` and `endpk`.  
  
```  
signedstart=2015-07-01T08:49Z  
signedexpiry=2015-07-02T08:49Z  
signedpermissions=u  
signature= +SzBm0wi8xECuGkKw97wnkSZ/62sxU+6Hq6a7qojIVE=  
signedidentifier=YWJjZGVmZw==   
signedversion=2015-02-21  
startpk="Coho Winery"  
endpk="Coho Winery"  
  
String-To-Sign = u + \n   
                 2015-07-01T08:49Z + \n  
                 2015-07-02T08:49Z + \n  
                 table/myaccount/mytable + \n  
                 YWJjZGVmZw== + \n  
                 2015-02-21 + \n  
                 Coho Winery + \n  
                 + \n  
                 Coho Winery + \n  
  
MERGE https://myaccount.table.core.windows.net/MyTable(PartitionKey='Coho%20Winery',RowKey='Seattle')?sv=2015-02-21&tn=MyTable&st=2015-07-01T08%3a49Z&se=2015-07-02T08%3a49Z&sp=u&si=YWJjZGVmZw%3d%3d&sig=jDrr6cna7JPwIaxWfdH0tT5v9dc%3d&spk=Coho%20Winery&epk=Coho%20Winery HTTP/1.1  
Host: myaccount.table.core.windows.net  
DataServiceVersion: 1.0;NetFx  
MaxDataServiceVersion: 2.0;NetFx  
If-Match: *  
Content-Type: application/atom+xml  
Content-Length: 696  
  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<entry xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">  
  <title />  
  <author>  
    <name />  
  </author>  
  <id>https://myaccount.table.core.windows.net/MyTable(PartitionKey='Coho Winery',RowKey='Seattle')</id>  
  <content type="application/xml">  
    <m:properties>  
      <d:PartitionKey>P</d:PartitionKey>  
      <d:RowKey>R</d:RowKey>  
      <d:Timestamp m:type="Edm.DateTime">0001-01-01T00:00:00</d:Timestamp>  
    </m:properties>  
  </content>  
</entry>  
  
```  
  
## See Also  
 [Delegating Access with a Shared Access Signature](../StorageServicesREST/Delegating-Access-with-a-Shared-Access-Signature.md)   
 [Constructing a Service SAS](../StorageServicesREST/Constructing-a-Service-SAS.md)
---
title: "Specifying Conditional Headers for Blob Service Operations"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 36087161-9e7c-47e4-904c-3392cc35a8e9
caps.latest.revision: 46
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
# Specifying Conditional Headers for Blob Service Operations
Several Blob service operations support the use of conditional headers. You can specify conditional headers to carry out an operation only if a specified condition has been met.  
  
 The Blob service follows the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478) for conditional headers.  
  
##  <a name="Subheading1"></a> Supported Conditional Headers  
 The supported conditional headers are described in the following table.  
  
|Conditional header|Description|  
|------------------------|-----------------|  
|`If-Modified-Since`|A `DateTime` value. Specify this header to perform the operation only if the resource has been modified since the specified time.|  
|`If-Unmodified-Since`|A `DateTime` value. Specify this header to perform the operation only if the resource has not been modified since the specified date/time.|  
|`If-Match`|An ETag value. Specify this header to perform the operation only if the resource's ETag matches the value specified. For versions 2011-08-18 and newer, the ETag can be specified in quotes.|  
|`If-None-Match`|An ETag value, or the wildcard character (*). Specify this header to perform the operation only if the resource's ETag does not match the value specified. For versions 2011-08-18 and newer, the ETag can be specified in quotes.<br /><br /> Specify the wildcard character (\*) to perform the operation only if the resource does not exist, and fail the operation if it does exist.|  
  
## Specifying Conditional Headers for Blob Service Read Operations in Version 2013-08-15 or Later  
 Beginning with version 2013-08-15, the [Get Blob](../StorageServicesREST/Get-Blob.md) and [Get Blob Properties](../StorageServicesREST/Get-Blob-Properties.md) operations support multiple conditional headers. You can specify any combination of supported conditional headers. The Blob service will evaluate these conditions according to following expression:  
  
 `If-Match && If-Unmodified-Since && (If-None-Match || If-Modified-Since)`  
  
 You can also provide multiple comma-separated values for `If-Match` and `If-None-Match`. If you specify multiple values for `If-Match`, then the Blob service performs a logical `OR` operation on all of the provided values before evaluating the entire expression. If you specify multiple values for `if-None-Match`, then the service performs a logical `AND` operation before evaluating the entire expression. Specifying multiple values for `If-Modified-Since` and `If-Unmodified-Since` is not supported and results in error code 400 (`Bad Request`).  
  
 This feature is enabled in order to comply with [HTTP/1.1 specification](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html) and to cater to scenarios where a Content Delivery Network (CDN) or proxy server adds additional conditional headers to an inflight request. Below are some examples of different combinations of conditional headers.  
  
 **Example 1:**  
  
 Consider a [Get Blob](../StorageServicesREST/Get-Blob.md) request containing the `If-Match` and `If-Modified-Since` headers. The following table indicates the result if the headers are evaluated individually, and the result if they are evaluated in combination.  
  
|Conditional headers|Result if evaluated individually|Result if evaluated in combination|  
|-------------------------|--------------------------------------|----------------------------------------|  
|`If-Match`|412 (Precondition Failed)|412 (Precondition Failed)|  
|`If-Modified-Since`|200 (OK)|412 (Precondition Failed)|  
|`If-Match`|412 (Precondition Failed)|412 (Precondition Failed)|  
|`If-Modified-Since`|304 (Not Modified)|412 (Precondition Failed)|  
|`If-Match`|200 (OK)|200 (OK)|  
|`If-Modified-Since`|200 (OK)|200 (OK)|  
|`If-Match`|200 (OK)|304 (Not Modified)|  
|`If-Modified-Since`|304 (Not Modified)|304 (Not Modified)|  
  
 **Example 2:**  
  
 Consider a request containing `If-None-Match` and `If-Modified-Since` headers.  
  
|Conditional headers|Result if evaluated individually|Result if evaluated in combination|  
|-------------------------|--------------------------------------|----------------------------------------|  
|`If-None-Match`|304 (Not Modified)|200 (OK)|  
|`If-Modified-Since`|200 (OK)|200 (OK)|  
|`If-None-Match`|200 (OK)|200 (OK)|  
|`If-Modified-Since`|200 (OK)|200 (OK)|  
|`If-None-Match`|200 (OK)|200 (OK)|  
|`If-Modified-Since`|304 (Not Modified)|200 (OK)|  
|`If-None-Match`|304 (Not Modified)|304 (Not Modified)|  
|`If-Modified-Since`|304 (Not Modified)|304 (Not Modified)|  
  
 **Example 3:**  
  
 Consider a request containing `If-Modified-Since`, `If-Match` and `If-Unmodified-Since` headers.  
  
|Conditional headers|Result if evaluated individually|Result if evaluated in combination|  
|-------------------------|--------------------------------------|----------------------------------------|  
|`If-Modified-Since`|200 (OK)|412 (Precondition Failed)|  
|`If-Match`|412 (Precondition Failed)|412 (Precondition Failed)|  
|`If-Unmodified-Since`|200 (OK)|412 (Precondition Failed)|  
|`If-Modified-Since`|200 (OK)|412 (Precondition Failed)|  
|`If-Match`|200 (OK)|412 (Precondition Failed)|  
|`If-Unmodified-Since`|412 (Precondition Failed)|412 (Precondition Failed)|  
|`If-Modified-Since`|304 (Not Modified)|412 (Precondition Failed)|  
|`If-Match`|200 (OK)|412 (Precondition Failed)|  
|`If-Unmodified-Since`|412 (Precondition Failed)|412 (Precondition Failed)|  
|`If-Modified-Since`|304 (Not Modified)|304 (Not Modified)|  
|`If-Match`|200 (OK)|304 (Not Modified)|  
|`If-Unmodified-Since`|200 (OK)|304 (Not Modified)|  
  
 **Example 4:**  
  
 Consider a request containing `If-Modified-Since`, `If-None-Match`, `If-Unmodified-Since` and `If-Match` headers.  
  
|Combination|Individual http status code|Get Blob status result|  
|-----------------|---------------------------------|----------------------------|  
|`If-Modified-Since`|200 (OK)|200 (OK)|  
|`If-None-Match`|200 (OK)|200 (OK)|  
|`If-Unmodified-Since`|200 (OK)|200 (OK)|  
|`If-Match`|200 (OK)|200 (OK)|  
|`If-Modified-Since`|200 (OK)|412 (Precondition Failed)|  
|`If-None-Match`|304 (Not Modified)|412 (Precondition Failed)|  
|`If-Unmodified-Since`|412 (Precondition Failed)|412 (Precondition Failed)|  
|`If-Match`|200 (OK)|412 (Precondition Failed)|  
|`If-Modified-Since`|200 (OK)|200 (OK)|  
|`If-None-Match`|304 (Not Modified)|200 (OK)|  
|`If-Unmodified-Since`|200 (OK)|200 (OK)|  
|`If-Match`|200 (OK)|200 (OK)|  
|`If-Modified-Since`|304 (Not Modified)|412 (Precondition Failed)|  
|`If-None-Match`|200 (OK)|412 (Precondition Failed)|  
|`If-Unmodified-Since`|200 (OK)|412 (Precondition Failed)|  
|`If-Match`|412 (Precondition Failed)|412 (Precondition Failed)|  
|`If-Modified-Since`|304 (Not Modified)|412 (Precondition Failed)|  
|`If-None-Match`|200 (OK)|412 (Precondition Failed)|  
|`If-Unmodified-Since`|412 (Precondition Failed)|412 (Precondition Failed)|  
|`If-Match`|412 (Precondition Failed)|412 (Precondition Failed)|  
|`If-Modified-Since`|304 (Not Modified)|200 (OK)|  
|`If-None-Match`|200 (OK)|200 (OK)|  
|`If-Unmodified-Since`|200 (OK)|200 (OK)|  
|`If-Match`|200 (OK)|200 (OK)|  
|`If-Modified-Since`|304 (Not Modified)|412 (Precondition Failed)|  
|`If-None-Match`|304 (Not Modified)|412 (Precondition Failed)|  
|`If-Unmodified-Since`|412 (Precondition Failed)|412 (Precondition Failed)|  
|`If-Match`|200 (OK)|412 (Precondition Failed)|  
  
## Specifying Conditional Headers for Read Operations in Versions Prior to 2013-08-15, and for Write Operations (All Versions)  
 When calling Blob service read operations ([Get Blob](../StorageServicesREST/Get-Blob.md) and [Get Blob Properties](../StorageServicesREST/Get-Blob-Properties.md)) with versions prior to 2013-08-15, and when calling any write operation regardless of version, keep in mind the following:  
  
-   If a request specifies both the `If-None-Match` and `If-Modified-Since` headers, the request is evaluated based on the criteria specified in `If-None-Match`.  
  
-   If a request specifies both the `If-Match` and `If-Unmodified-Since` headers, the request is evaluated based on the criteria specified in `If-Match`.  
  
-   With the exception of the two combinations of conditional headers listed above, a request may specify only a single conditional header. Specifying more than one conditional header results in status code 400 (`Bad Request`).  
  
-   If a response includes an ETag, verify the version of the request and response before processing the ETag. For example, version 2011-08-18 and later return a quoted ETag, but older versions do not. Ensure that your application can process both ETag formats before they are evaluated.  
  
-   [RFC 2616](http://www.ietf.org/rfc/rfc2616.txt) allows multiple ETag values in a single header, but requests to the Blob service can only include one ETag value. Specifying more than one ETag value results in status code 400 (`Bad Request`).  
  
##  <a name="Subheading2"></a> Operations Supporting Conditional Headers  
 The operations that support conditional headers are described in the following table.  
  
||||  
|-|-|-|  
|**REST Operation**|**Operation type**|**Supported conditional headers**|  
|[Copy Blob](../StorageServicesREST/Copy-Blob.md)|Read and Write|For conditions on the destination blob:<br /><br /> -                     **If-Modified-Since**<br /><br /> -                     **If-Unmodified-Since**<br /><br /> -                     **If-Match**<br /><br /> -                     **If-None-Match**<br /><br /> For conditions on the source blob:<br /><br /> -                     **x-ms-source-if-modified-since**<br /><br /> -                     **x-ms-source-if-unmodified-since**<br /><br /> -                     **x-ms-source-if-match**<br /><br /> -                     **x-ms-source-if-none-match**|  
|[Delete Blob](../StorageServicesREST/Delete-Blob.md)|Write|**If-Modified-Since**<br /><br /> **If-Unmodified-Since**<br /><br /> **If-Match**<br /><br /> **If-None-Match**|  
|[Delete Container](../StorageServicesREST/Delete-Container.md)|Write|**If-Modified-Since**<br /><br /> **If-Unmodified-Since**|  
|[Get Blob](../StorageServicesREST/Get-Blob.md)|Read|**If-Modified-Since**<br /><br /> **If-Unmodified-Since**<br /><br /> **If-Match**<br /><br /> **If-None-Match**|  
|[Get Blob Metadata](../StorageServicesREST/Get-Blob-Metadata.md)|Read|**If-Modified-Since**<br /><br /> **If-Unmodified-Since**<br /><br /> **If-Match**<br /><br /> **If-None-Match**|  
|[Get Blob Properties](../StorageServicesREST/Get-Blob-Properties.md)|Read|**If-Modified-Since**<br /><br /> **If-Unmodified-Since**<br /><br /> **If-Match**<br /><br /> **If-None-Match**|  
|[Get Page Ranges](../StorageServicesREST/Get-Page-Ranges.md)|Write|**If-Modified-Since**<br /><br /> **If-Unmodified-Since**<br /><br /> **If-Match**<br /><br /> **If-None-Match**|  
|[Lease Blob](../StorageServicesREST/Lease-Blob.md)|Write|**If-Modified-Since**<br /><br /> **If-Unmodified-Since**<br /><br /> **If-Match**<br /><br /> **If-None-Match**|  
|[Lease Container](../StorageServicesREST/Lease-Container.md)|Write|**If-Modified-Since**<br /><br /> **If-Unmodified-Since**|  
|[Put Blob](../StorageServicesREST/Put-Blob.md)|Write|**If-Modified-Since**<br /><br /> **If-Unmodified-Since**<br /><br /> **If-Match**<br /><br /> **If-None-Match**|  
|[Put Block List](../StorageServicesREST/Put-Block-List.md)|Write|**If-Modified-Since**<br /><br /> **If-Unmodified-Since**<br /><br /> **If-Match**<br /><br /> **If-None-Match**|  
|[Append Block](../StorageServicesREST/Append-Block.md)<br /><br /> (version 2015-02-21 and later)|Write|**If-Modified-Since**<br /><br /> **If-Unmodified-Since**<br /><br /> **If-Match**<br /><br /> **If-None-Match**|  
|[Put Page](../StorageServicesREST/Put-Page.md)|Write|**If-Modified-Since**<br /><br /> **If-Unmodified-Since**<br /><br /> **If-Match**<br /><br /> **If-None-Match**|  
|[Set Blob Metadata](../StorageServicesREST/Set-Blob-Metadata.md)|Write|**If-Modified-Since**<br /><br /> **If-Unmodified-Since**<br /><br /> **If-Match**<br /><br /> **If-None-Match**|  
|[Set Blob Properties](../StorageServicesREST/Set-Blob-Properties.md)|Write|**If-Modified-Since**<br /><br /> **If-Unmodified-Since**<br /><br /> **If-Match**<br /><br /> **If-None-Match**|  
|[Set Container ACL](../StorageServicesREST/Set-Container-ACL.md)|Write|**If-Modified-Since**<br /><br /> **If-Unmodified-Since**|  
|[Set Container Metadata](../StorageServicesREST/Set-Container-Metadata.md)|Write|**If-Modified-Since**|  
|[Snapshot Blob](../StorageServicesREST/Snapshot-Blob.md)|Read|**If-Modified-Since**<br /><br /> **If-Unmodified-Since**<br /><br /> **If-Match**<br /><br /> **If-None-Match**|  
  
 The following Blob service data operations do not currently support conditional headers:  
  
-   [Abort Copy Blob](../StorageServicesREST/Abort-Copy-Blob.md)  
  
-   [Create Container](../StorageServicesREST/Create-Container.md)  
  
-   [Get Block List](../StorageServicesREST/Get-Block-List.md)  
  
-   [Get Container ACL](../StorageServicesREST/Get-Container-ACL.md)  
  
-   [Get Container Metadata](../StorageServicesREST/Get-Container-Metadata.md)  
  
-   [Get Container Properties](../StorageServicesREST/Get-Container-Properties.md)  
  
-   [List Blobs](../StorageServicesREST/List-Blobs.md)  
  
-   [List Containers](../StorageServicesREST/List-Containers2.md)  
  
-   [Put Block](../StorageServicesREST/Put-Block.md)  
  
##  <a name="Subheading3"></a> HTTP Response Codes for Operations Supporting Conditional Headers  
 If the request includes a conditional header and the specified condition is not met by the resource being requested, the Blob service returns an HTTP response code. The response codes returned are in accordance with the HTTP/1.1 protocol specification (RFC 2616).  
  
 Methods in the Azure .NET client library convert these error response codes into a <xref:Microsoft.WindowsAzure.Storage.StorageException?qualifyHint=False>.  
  
### Read Operations  
 The following table indicates the response codes returned for an unmet condition for each conditional header when the operation is a read operation. Read operations use the verbs GET or HEAD.  
  
|Conditional header|Response code if condition has not been met|  
|------------------------|-------------------------------------------------|  
|`If-Modified-Since`|Not Modified (304 (Not Modified))|  
|`If-Unmodified-Since`|Precondition Failed (412 (Precondition Failed))|  
|`If-Match`|Precondition Failed (412 (Precondition Failed))|  
|`If-None-Match`|Not Modified (304 (Not Modified))|  
  
 Refer to the examples above for results when using multiple headers with versions 2013-08-15 or later.  
  
### Write Operations  
 The following table indicates the response codes returned for an unmet condition for each conditional header when the operation is a write operation. Write operations use the verbs PUT or DELETE.  
  
|Conditional header|Response code if condition has not been met|  
|------------------------|-------------------------------------------------|  
|`If-Modified-Since`|Precondition Failed (412 (Precondition Failed))|  
|`If-Unmodified-Since`|Precondition Failed (412 (Precondition Failed))|  
|`If-Match`|Precondition Failed (412 (Precondition Failed))|  
|`If-None-Match`|Precondition Failed (412 (Precondition Failed))|  
  
## Copy Operations  
 The following table indicates the response codes returned for an unmet condition for each conditional header when the operation is a copy operation. The [Copy Blob](../StorageServicesREST/Copy-Blob.md) operation uses the verbs PUT.  
  
|Conditional header|Response code if condition has not been met|  
|------------------------|-------------------------------------------------|  
|`If-Modified-Since`|Precondition Failed (412 (Precondition Failed))|  
|`If-Unmodified-Since`|Precondition Failed (412 (Precondition Failed))|  
|`If-Match`|Precondition Failed (412 (Precondition Failed))|  
|`If-None-Match`|Precondition Failed (412 (Precondition Failed))|  
|`x-ms-source-if-modified-since`|Precondition Failed (412 (Precondition Failed))|  
|`x-ms-source-if-unmodified-since`|Precondition Failed (412 (Precondition Failed))|  
|`x-ms-source-if-match`|Precondition Failed (412 (Precondition Failed))|  
|`x-ms-source-if-none-match`|Precondition Failed (412 (Precondition Failed))|  
  
## See Also  
 [Blob Service Concepts](../StorageServicesREST/Blob-Service-Concepts.md)
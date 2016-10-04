---
title: "List Containers2"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
H1: List Containers
ms.assetid: 1a1d2a8e-de2b-4fa8-9d6d-582998a26a4f
caps.latest.revision: 90
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
# List Containers2
The `List Containers` operation returns a list of the containers under the specified account.  
  
##  <a name="Request"></a> Request  
 The `List Containers` request may be constructed as follows. HTTPS is recommended. Replace *myaccount* with the name of your storage account:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`GET`|`https://myaccount.blob.core.windows.net/?comp=list`|HTTP/1.1|  
  
 Note that the URI must always include the forward slash (/) to separate the host name from the path and query portions of the URI. In the case of the `List Containers` operation, the path portion of the URI is empty.  
  
### Emulated Storage Service Request  
 When making a request against the emulated storage service, specify the emulator hostname and Blob service port as `127.0.0.1:10000`, followed by the emulated storage account name:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|`GET`|`http://127.0.0.1:10000/devstoreaccount1?comp=list`|HTTP/1.1|  
  
 Note that emulated storage only supports blob sizes up to 2 GB.  
  
 For more information, see [Using the Azure Storage Emulator for Development and Testing](assetId:///f0e3acde-f019-4148-9544-34cf2ff27211) and [Differences Between the Storage Emulator and Azure Storage Services](assetId:///c60f2090-c0f4-4817-8559-e98786461dbe).  
  
### URI Parameters  
 The following additional parameters may be specified on the request URI.  
  
|Parameter|Description|  
|---------------|-----------------|  
|`prefix`|Optional. Filters the results to return only containers whose name begins with the specified prefix.|  
|`marker`|Optional. A string value that identifies the portion of the list of containers to be returned with the next listing operation. The operation returns the `NextMarker` value within the response body if the listing operation did not return all containers remaining to be listed with the current page. The `NextMarker` value can be used as the value for the `marker` parameter in a subsequent call to request the next page of list items.<br /><br /> The marker value is opaque to the client.|  
|`maxresults`|Optional. Specifies the maximum number of containers to return. If the request does not specify `maxresults`, or specifies a value greater than 5,000, the server will return up to 5,000 items. If the parameter is set to a value less than or equal to zero, the server will return status code 400 (Bad Request).|  
|`include=metadata`|Optional. Include this parameter to specify that the container's metadata be returned as part of the response body.<br /><br /> Note that metadata requested with this parameter must be stored in accordance with the naming restrictions imposed by the 2009-09-19 version of the Blob service. Beginning with this version, all metadata names must adhere to the naming conventions for [C# identifiers](http://msdn.microsoft.com/library/aa664670\(VS.71\).aspx).|  
|`timeout`|Optional. The `timeout` parameter is expressed in seconds. For more information, see [Setting Timeouts for Blob Service Operations](../StorageServicesREST/Setting-Timeouts-for-Blob-Service-Operations.md).|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Required for all authenticated requests. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
### Request Body  
 None.  
  
##  <a name="Response"></a> Response  
 The response includes an HTTP status code, a set of response headers, and a response body in XML format.  
  
### Status Code  
 A successful operation returns status code 200 (OK).  
  
 For information about status codes, see [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md).  
  
### Response Headers  
 The response for this operation includes the following headers. The response also includes additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response header|Description|  
|---------------------|-----------------|  
|`Content-Type`|Standard HTTP/1.1 header. Specifies the format in which the results are returned. Currently, this value is application/xml.|  
|`x-ms-request-id`|This header uniquely identifies the request that was made and can be used for troubleshooting the request. For more information, see [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md).|  
|`x-ms-version`|Indicates the version of the Blob service used to execute the request. This header is returned for requests made against version 2009-09-19 and above.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
  
### Response Body  
 The format of the response body is as follows.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<EnumerationResults ServiceEndpoint="https://myaccount.blob.core.windows.net">  
  <Prefix>string-value</Prefix>  
  <Marker>string-value</Marker>  
  <MaxResults>int-value</MaxResults>  
  <Containers>  
    <Container>  
      <Name>container-name</Name>  
      <Properties>  
        <Last-Modified>date/time-value</Last-Modified>  
        <Etag>etag</Etag>  
        <LeaseStatus>locked | unlocked</LeaseStatus>  
        <LeaseState>available | leased | expired | breaking | broken</LeaseState>  
        <LeaseDuration>infinite | fixed</LeaseDuration>        
      </Properties>  
      <Metadata>  
        <metadata-name>value</metadata-name>  
      </Metadata>  
    </Container>  
  </Containers>  
  <NextMarker>marker-value</NextMarker>  
</EnumerationResults>  
```  
  
 `LeaseStatus`, `LeaseState`, and `LeaseDuration` only appear in version 2012-02-12 and later.  
  
 Beginning with version 2013-08-15, the `AccountName` attribute for the `EnumerationResults` element has been renamed to `ServiceEndpoint`. The `URL` element has also been removed from the `Container` element. For versions prior to 2013-08-15, the container's URL, as specified by the `URL` field, does not include the `restype=container` parameter. If you use this value to make subsequent requests against the enumerated containers, be sure to append this parameter to indicate that the resource type is a container.  
  
 The `Prefix`, `Marker`, and `MaxResults` elements are only present if they were specified on the URI. The `NextMarker` element has a value only if the list results are not complete.  
  
 The `Metadata` element is present only if the `include=metadata` parameter was specified on the URI. Within the `Metadata` element, the value of each name-value pair is listed within an element corresponding to the pair's name.  
  
 If a metadata name-value pair violates the naming restrictions enforced by the 2009-09-19 version, the response body indicates the problematic name within an `x-ms-invalid-name` element, as shown in the following XML fragment:  
  
```  
  
<Metadata>  
  <MyMetadata1>first value</MyMetadata1>  
  <MyMetadata2>second value</MyMetadata2>  
  <x-ms-invalid-name>invalid-metadata-name</x-ms-invalid-name>  
</Metadata>  
  
```  
  
> [!NOTE]
>  Beginning with version 2009-09-19, the response body for `List Containers` returns the container's last modified time in an element named `Last-Modified`. In previous versions, this element was named `LastModified`.  
  
##  <a name="Authorization"></a> Authorization  
 Only the account owner may call this operation.  
  
## Remarks  
 If you specify a value for the `maxresults` parameter and the number of containers to return exceeds this value, or exceeds the default value for `maxresults`, the response body will contain the `NextMarker` element. `NextMarker` indicates the next container to return on a subsequent request. To return the next set of items, specify the value of `NextMarker` for the `marker` parameter on the URI for the subsequent request.  
  
 Note that the value of `NextMarker` should be treated as opaque.  
  
 Containers are listed in alphabetical order in the response body.  
  
 The `List Containers` operation times out after 30 seconds.  
  
##  <a name="Samplerequestandresponse"></a> Sample Request and Response  
 The following sample URI requests the list of containers for an account, setting the maximum results to return for the initial operation to 3.  
  
```  
GET https://myaccount.blob.core.windows.net/?comp=list&maxresults=3 HTTP/1.1  
```  
  
 The request is sent with these headers:  
  
```  
x-ms-version: 2013-08-15  
x-ms-date: Wed, 23 Oct 2013 22:08:44 GMT  
Authorization: SharedKey myaccount:CY1OP3O3jGFpYFbTCBimLn0Xov0vt0khH/D5Gy0fXvg=  
```  
  
 The status code and response headers are returned as follows:  
  
```  
HTTP/1.1 200 OK  
Transfer-Encoding: chunked  
Content-Type: application/xml  
Date: Wed, 23 Oct 2013 22:08:54 GMT  
x-ms-version: 2013-08-15  
Server: Windows-Azure-Blob/1.0 Microsoft-HTTPAPI/2.0  
  
```  
  
 The response XML for this request is as follows. Note that the `NextMarker` element follows the set of containers and includes the name of the next container to be returned.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<EnumerationResults ServiceEndpoint="https://myaccount.blob.core.windows.net/">  
  <MaxResults>3</MaxResults>  
  <Containers>  
    <Container>  
      <Name>audio</Name>  
      <Properties>  
        <Last-Modified>Wed, 23 Oct 2013 20:39:39 GMT</Last-Modified>  
        <Etag>0x8CACB9BD7C6B1B2</Etag>  
      </Properties>  
    </Container>  
    <Container>  
      <Name>images</Name>  
      <Properties>  
        <Last-Modified>Wed, 23 Oct 2013 20:39:39 GMT</Last-Modified>  
        <Etag>0x8CACB9BD7C1EEEC</Etag>  
      </Properties>  
    </Container>  
    <Container>  
      <Name>textfiles</Name>  
      <Properties>  
        <Last-Modified>Wed, 23 Oct 2013 20:39:39 GMT</Last-Modified>  
        <Etag>0x8CACB9BD7BACAC3</Etag>  
      </Properties>  
    </Container>  
  </Containers>  
  <NextMarker>video</NextMarker>  
</EnumerationResults>  
```  
  
 The subsequent list operation specifies the marker on the request URI, as follows. The next set of results is returned beginning with the container specified by the marker.  
  
```  
https://myaccount.blob.core.windows.net/?comp=list&maxresults=3&marker=video  
```  
  
## See Also  
 [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md)   
 [Status and Error Codes](../StorageServicesREST/Status-and-Error-Codes2.md)   
 [Blob Service Error Codes](../StorageServicesREST/Blob-Service-Error-Codes.md)   
 [Enumerating Blob Resources](../StorageServicesREST/Enumerating-Blob-Resources.md)   
 [Using the Azure Storage Emulator for Development and Testing](assetId:///f0e3acde-f019-4148-9544-34cf2ff27211)   
 [Setting Timeouts for Blob Service Operations](../StorageServicesREST/Setting-Timeouts-for-Blob-Service-Operations.md)
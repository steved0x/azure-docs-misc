---
title: "Enumerating Blob Resources"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 35f34a0b-ab15-42da-9249-70cc51093a4f
caps.latest.revision: 8
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
# Enumerating Blob Resources
The Blob service API includes operations for enumerating the containers within an account (the [List Containers](../StorageServicesREST/List-Containers2.md) operation) and the blobs within a container (the [List Blobs](../StorageServicesREST/List-Blobs.md) operation). These operations have some common features worth noting.  
  
 An enumeration operation returns an XML response that contains all or part of the requested list. The operation returns entities in alphabetical order.  
  
 This topic contains the following subtopics:  
  
 [Setting Maximum Results](#Subheading1)  
  
 [Retrieving Partial List Results with Markers](#Subheading2)  
  
 [Filtering List Results](#Subheading3)  
  
 [Traversing the Blob Namespace](#Subheading4)  
  
 [XML Response Format](#Subheading5)  
  
##  <a name="Subheading1"></a> Setting Maximum Results  
 To specify the maximum number of results to be returned in a single call to an enumeration operation, specify a value for the `maxresults` parameter on the request URI.  
  
 If the maximum number of results is not specified in the request or is greater than 5,000, the server will return up to the maximum of 5,000 items. If you specify a maximum number of results less than or equal to zero, the service returns status code 400 (Bad Request).  
  
##  <a name="Subheading2"></a> Retrieving Partial List Results with Markers  
 The first time that the enumeration operation is performed against a particular resource, the response may contain all results, or it may contain a subset of the results and a marker value. The marker value can be passed to the subsequent call to return the next set of results, and so on, until the list is complete and no marker is returned.  
  
 The marker value is included in the `NextMarker` element of the XML response. When the `NextMarker` element is empty, the listing is complete. The value of `NextMarker` is a string value that is opaque to the client.  
  
 To return the next set of results in a subsequent operation, pass the value returned in the `NextMarker` tag as the `marker` parameter on the request URI.  
  
##  <a name="Subheading3"></a> Filtering List Results  
  
-   The list of results can be filtered by specifying a prefix string on the request by using the `prefix` parameter. The list operation then returns the entities that have names that begin with that prefix. If the `prefix` parameter is specified on the request URI, the response XML includes a `Prefix` element containing the prefix character or characters. For example, specifying a prefix with a value of 'c' returns `<Prefix>``c``</Prefix>` within the response XML. For an example, see the [Container List](#ContainerList) section later in this topic.  
  
##  <a name="Subheading4"></a> Traversing the Blob Namespace  
 The [List Blobs](../StorageServicesREST/List-Blobs.md) operation has an additional `delimiter` parameter that enables the caller to traverse the blob namespace by using a user-configured delimiter. The delimiter may be a single character or a string. When the request includes this parameter, the operation returns a `BlobPrefix` element. The `BlobPrefix` element is returned in place of all blobs with names that begin with the same substring up to the appearance of the delimiter character. The value of the `BlobPrefix` element is *substring+delimiter*, where *substring* is the common substring that begins one or more blob names, and *delimiter* is the value of the *delimiter* parameter.  
  
 You can use the value of `BlobPrefix` to make a subsequent call to list the blobs that begin with this prefix, by specifying the value of `BlobPrefix` for the `prefix` parameter on the request URI. In this way, you can traverse a virtual hierarchy of blobs as though it were a file system. For an example, see the [Delimited Blob List](#DelimitedBlobList) example later in this topic.  
  
 Note that each `BlobPrefix` returned counts toward the maximum result.  
  
 Note that you cannot enumerate blob snapshots if you include a delimiter with the request. If you specify a value for the `delimiter` parameter and also set the `include=snapshots` parameter, the Blob service returns the InvalidQueryParameter error (HTTP status code 400 – Bad Request).  
  
##  <a name="Subheading5"></a> XML Response Format  
 The list output is an XML document whose format is similar to those shown in the code examples later in this topic.  
  
 Note that the response body includes the values of all parameters that were specified on the request URI as elements within the response body.  
  
 The `DateTime` value returned in the `Last-Modified` element is in RFC 1123 format. For more information about `DateTime` values, see [Representation of Date-Time Values in Headers](../StorageServicesREST/Representation-of-Date-Time-Values-in-Headers.md).  
  
###  <a name="ContainerList"></a> Container List  
 This example shows the result of an enumeration operation returning two containers. The request URI is as follows:  
  
```  
GET https://myaccount.blob.core.windows.net/?comp=list&prefix=c&maxresults=3&include=metadata  
```  
  
 The prefix 'c' was specified to filter the list. The maximum number of results to return was set to 3. The NextMarker tag shows the name of the container that will be returned on a subsequent list operation.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<EnumerationResults AccountName="https://myaccount.blob.core.windows.net/">  
  <Prefix>c</Prefix>  
  <MaxResults>3</MaxResults>  
  <Containers>  
    <Container>  
      <Name>container1</Name>  
      <Url>https://myaccount.blob.core.windows.net/container1</Url>  
      <Properties>  
        <Last-Modified>Sun, 27 Sep 2009 18:09:03 GMT</Last-Modified>  
        <Etag>0x8CAE7D0C4AF4487</Etag>  
      </Properties>  
      <Metadata>  
        <Color>orange</Color>  
        <ContainerNumber>01</ContainerNumber>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      </Metadata>  
    </Container>  
    <Container>  
      <Name>container2</Name>  
      <Url>https://myaccount.blob.core.windows.net/container2</Url>  
      <Properties>  
        <Last-Modified>Sun, 27 Sep 2009 17:26:40 GMT</Last-Modified>  
        <Etag>0x8CAE7CAD8C24928</Etag>  
      </Properties>  
      <Metadata>  
        <Color>pink</Color>  
        <ContainerNumber>02</ContainerNumber>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      </Metadata>  
    </Container>  
    <Container>  
      <Name>container3</Name>  
      <Url>https://myaccount.blob.core.windows.net/container3</Url>  
      <Properties>  
        <Last-Modified>Sun, 27 Sep 2009 17:26:40 GMT</Last-Modified>  
        <Etag>0x8CAE7CAD8EAC0BB</Etag>  
      </Properties>  
      <Metadata>  
        <Color>brown</Color>  
        <ContainerNumber>03</ContainerNumber>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      </Metadata>  
    </Container>  
  </Containers>  
  <NextMarker>container4</NextMarker>  
</EnumerationResults>  
```  
  
### Blob and Snapshot List  
 This example shows the result of an enumeration operation that returns blobs and snapshots in a container named *mycontainer*. The request URI is as follows:  
  
```  
GET https://myaccount.blob.core.windows.net/mycontainer?restype=container&comp=list&include=snapshots&include=metadata  
```  
  
 The response includes both the blobs and snapshots:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<EnumerationResults ContainerName="https://myaccount.blob.core.windows.net/mycontainer">  
  <Blobs>  
    <Blob>  
      <Name>blob1.txt</Name>  
      <Url>https://myaccount.blob.core.windows.net/mycontainer/blob1.txt</Url>  
      <Properties>  
        <Last-Modified>Wed, 09 Sep 2009 09:20:02 GMT</Last-Modified>  
        <Etag>0x8CBFF45D8A29A19</Etag>  
        <Content-Length>100</Content-Length>  
        <Content-Type>text/html</Content-Type>  
        <Content-Encoding />  
        <Content-Language>en-US</Content-Language>  
        <Content-MD5 />  
        <Cache-Control>no-cache</Cache-Control>  
        <BlobType>BlockBlob</BlobType>  
        <LeaseStatus>unlocked</LeaseStatus>  
      </Properties>  
      <Metadata>  
        <Color>blue</Color>  
        <BlobNumber>01</BlobNumber>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      </Metadata>  
    </Blob>  
    <Blob>  
      <Name>blob2.txt</Name>  
      <Snapshot>2009-09-09T09:20:03.0427659Z</Snapshot>  
      <Url>https://myaccount.blob.core.windows.net/mycontainer/blob2.txt?snapshot=2009-09-09T09%3a20%3a03.0427659Z</Url>  
      <Properties>  
        <Last-Modified>Wed, 09 Sep 2009 09:20:02 GMT</Last-Modified>  
        <Etag>0x8CBFF45D8B4C212</Etag>  
        <Content-Length>5000</Content-Length>  
        <Content-Type>application/octet-stream</Content-Type>  
        <Content-Encoding>gzip</Content-Encoding>  
        <Content-Language />  
        <Content-MD5 />  
        <Cache-Control />  
        <BlobType>BlockBlob</BlobType>  
      </Properties>  
      <Metadata>  
        <Color>green</Color>  
        <BlobNumber>02</BlobNumber>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
        <x-ms-invalid-name>nasdf$@#$$</x-ms-invalid-name>  
      </Metadata>  
    </Blob>  
    <Blob>  
      <Name>blob2.txt</Name>  
      <Snapshot>2009-09-09T09:20:03.1587543Z</Snapshot>  
      <Url>https://myaccount.blob.core.windows.net/mycontainer/blob2.txt?snapshot=2009-09-09T09%3a20%3a03.1587543Z</Url>  
      <Properties>  
        <Last-Modified>Wed, 09 Sep 2009 09:20:02 GMT</Last-Modified>  
        <Etag>0x8CBFF45D8B4C212</Etag>  
        <Content-Length>5000</Content-Length>  
        <Content-Type>application/octet-stream</Content-Type>  
        <Content-Encoding>gzip</Content-Encoding>  
        <Content-Language />  
        <Content-MD5 />  
        <Cache-Control />  
        <BlobType>BlockBlob</BlobType>  
      </Properties>  
      <Metadata>  
        <Color>green</Color>  
        <BlobNumber>02</BlobNumber>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      </Metadata>  
    </Blob>  
    <Blob>  
      <Name>blob2.txt</Name>  
      <Url>https://myaccount.blob.core.windows.net/mycontainer/blob2.txt</Url>  
      <Properties>  
        <Last-Modified>Wed, 09 Sep 2009 09:20:02 GMT</Last-Modified>  
        <Etag>0x8CBFF45D8B4C212</Etag>  
        <Content-Length>5000</Content-Length>  
        <Content-Type>application/octet-stream</Content-Type>  
        <Content-Encoding>gzip</Content-Encoding>  
        <Content-Language />  
        <Content-MD5 />  
        <Cache-Control />  
        <BlobType>BlockBlob</BlobType>  
        <LeaseStatus>unlocked</LeaseStatus>  
      </Properties>  
      <Metadata>  
        <Color>green</Color>  
        <BlobNumber>02</BlobNumber>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      </Metadata>  
    </Blob>  
    <Blob>  
      <Name>blob3.txt</Name>  
      <Url>https://myaccount.blob.core.windows.net/mycontainer/blob3.txt</Url>  
      <Properties>  
        <Last-Modified>Wed, 09 Sep 2009 09:20:03 GMT</Last-Modified>  
        <Etag>0x8CBFF45D911FADF</Etag>  
        <Content-Length>16384</Content-Length>  
        <Content-Type>image/jpeg</Content-Type>  
        <Content-Encoding />  
        <Content-Language />  
        <Content-MD5 />  
        <Cache-Control />  
        <x-ms-blob-sequence-number>3</x-ms-blob-sequence-number>  
        <BlobType>PageBlob</BlobType>  
        <LeaseStatus>locked</LeaseStatus>  
      </Properties>  
      <Metadata>  
        <Color>yellow</Color>  
        <BlobNumber>03</BlobNumber>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      </Metadata>  
    </Blob>  
  </Blobs>  
  <NextMarker />   
</EnumerationResults>  
```  
  
###  <a name="DelimitedBlobList"></a> Delimited Blob List  
 This example shows the result of an enumeration operation returning blobs beneath a container named *mycontainer*. The request URI is as follows:  
  
```  
GET https://myaccount.blob.core.windows.net/mycontainer?restype=container&comp=list&delimiter=/&maxresults=4  
```  
  
 In this case, the `delimiter` parameter has been specified as '/'. The response body includes the `BlobPrefix` tag, which represents the group of blobs beginning with the same substring, including the delimiter.  
  
 The sample blobs beneath the container are as follows. The first four are returned in the first enumeration operation, because `MaxResults` is set to 4. Note that *myfolder/blobA.txt* and *myfolder/blobB.txt* are grouped together in the response body in the `BlobPrefix` tag and count as a single blob in terms of the number of entities returned. To return the blobs beginning with this prefix, make a subsequent request in which the prefix parameter is set to *myfolder/*.  
  
-   blob1.txt  
  
-   blob2.txt  
  
-   myfolder/blobA.txt  
  
-   myfolder/blobB.txt  
  
-   newblob1.txt  
  
-   newblob2.txt  
  
 The next blob to be returned is newblob2.txt, returned in the `NextMarker` tag.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<EnumerationResults ContainerName="https://myaccount.blob.core.windows.net/mycontainer">  
  <MaxResults>4</MaxResults>  
  <Blobs>  
    <Blob>  
      <Name>blob1.txt</Name>  
      <Url>https://myaccount.blob.core.windows.net/mycontainer/blob1.txt</Url>  
      <Properties>  
        <Last-Modified>Sun, 27 Sep 2009 18:41:57 GMT</Last-Modified>  
        <Etag>0x8CAE7D55D050B8B</Etag>  
        <Content-Length>8</Content-Length>  
        <Content-Type>text/html</Content-Type>  
        <Content-Encoding />  
        <Content-Language>en-US</Content-Language>  
        <Content-MD5 />  
        <Cache-Control>no-cache</Cache-Control>  
        <BlobType>BlockBlob</BlobType>  
        <LeaseStatus>unlocked</LeaseStatus>  
      <Properties>  
    </Blob>  
    <Blob>  
      <Name>blob2.txt</Name>  
      <Url>https://myaccount.blob.core.windows.net/mycontainer/blob2.txt</Url>  
      <Properties>  
        <Last-Modified>Sun, 27 Sep 2009 12:18:50 GMT</Last-Modified>  
        <Etag>0x8CAE7D55CF6C339</Etag>  
        <Content-Length>100</Content-Length>  
        <Content-Type>text/html</Content-Type>  
        <Content-Encoding />  
        <Content-Language>en-US</Content-Language>  
        <Content-MD5 />  
        <Cache-Control>no-cache</Cache-Control>  
        <BlobType>BlockBlob</BlobType>  
        <LeaseStatus>unlocked</LeaseStatus>  
      </Properties>  
    </Blob>  
    <BlobPrefix>  
      <Name>myfolder/</Name>  
    </BlobPrefix>  
    <Blob>  
      <Name>newblob1.txt</Name>  
      <Url>https://myaccount.blob.core.windows.net/mycontainer/newblob1.txt</Url>  
      <Properties>  
        <Last-Modified>Sun, 27 Sep 2009 16:31:57 GMT</Last-Modified>  
        <Etag>0x8CAE7D55CF6C339</Etag>  
        <Content-Length>25</Content-Length>  
        <Content-Type>text/html</Content-Type>  
        <Content-Encoding />  
        <Content-Language>en-US</Content-Language>  
        <Content-MD5 />  
        <Cache-Control>no-cache</Cache-Control>  
        <BlobType>BlockBlob</BlobType>  
        <LeaseStatus>unlocked</LeaseStatus>  
      </Properties>  
    </Blob>  
  </Blobs>  
  <NextMarker>newblob2.txt</NextMarker>  
</EnumerationResults>  
```  
  
### Enumerating Blobs in the Root Container  
 To enumerate blobs in the root container, you can use the following URL:  
  
```  
https://myaccount.blob.core.windows.net/$root?restype=container&comp=list&maxresults=10  
```  
  
 Keep in mind that when you list the blobs in the root container, the XML response body does not include an explicit reference to the root container in the blob's `URL` field. Here's a sample response listing blobs in the root container:  
  
```xml  
  
<?xml version="1.0" encoding="utf-8"?>  
<EnumerationResults ContainerName="https://myaccount.blob.core.windows.net/%24root">  
  <MaxResults>10</MaxResults>  
  <Blobs>  
    <Blob>  
      <Name>rootblob1.txt</Name>  
      <Url>https://myaccount.blob.core.windows.net/rootblob1.txt</Url>  
      <Properties>  
        <Last-Modified>Sun, 27 Sep 2009 18:41:48 GMT</Last-Modified>  
        <Etag>0x8CAE7D55D050B8B</Etag>  
        <Content-Length>25</Content-Length>  
        <Content-Type>text/html</Content-Type>  
        <Content-Encoding />  
        <Content-Language>en-US</Content-Language>  
        <Content-MD5 />  
        <Cache-Control>no-cache</Cache-Control>  
        <BlobType>BlockBlob</BlobType>  
        <LeaseStatus>unlocked</LeaseStatus>  
      </Properties>  
   </Blob>  
    <Blob>  
      <Name>rootblob2.txt</Name>  
      <Url>https://myaccount.blob.core.windows.net/rootblob2.txt</Url>  
      <Properties>  
        <Last-Modified>Sun, 27 Sep 2009 18:45:57 GMT</Last-Modified>  
        <Etag>0x8CAE7D55CF6C339</Etag>  
        <Content-Length>14</Content-Length>  
        <Content-Type>text/plain; charset=UTF-8</Content-Type>  
        <Content-Encoding />  
        <Content-Language>en-US</Content-Language>  
        <Content-MD5 />  
        <Cache-Control>no-cache</Cache-Control>  
        <BlobType>BlockBlob</BlobType>  
        <LeaseStatus>unlocked</LeaseStatus>  
      </Properties>  
    </Blob>  
  </Blobs>  
</EnumerationResults>  
  
```  
  
## See Also  
 [List Containers](../StorageServicesREST/List-Containers2.md)   
 [List Blobs](../StorageServicesREST/List-Blobs.md)   
 [Blob Service Concepts](../StorageServicesREST/Blob-Service-Concepts.md)   
 [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md)
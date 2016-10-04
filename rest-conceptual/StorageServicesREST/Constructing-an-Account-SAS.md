---
title: "Constructing an Account SAS"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 3caef6a2-096c-4284-87bb-f88297a72032
caps.latest.revision: 19
author: tamram
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
# Constructing an Account SAS
Beginning with version 2015-04-05, Azure Storage supports creating a new type of shared access signature (SAS) at the level of the storage account. Creating an account SAS enables you to:  
  
-   Delegate access to service-level operations that are not currently available with a service-specific SAS, such as the `Get/Set Service Properties` and `Get Service Stats` operations.  
  
-   Delegate access to more than one service in a storage account at a time. For example, you can delegate access to resources in both the Blob and File services with an account SAS.  
  
-   Delegate access to write and delete operations for containers, queues, tables, and file shares, which are not available with an object-specific SAS.  
  
-   Specify an IP address or range of IP addresses from which to accept requests.  
  
-   Specify the HTTP protocol from which to accept requests (either HTTPS or HTTP/HTTPS).  
  
 A service-level SAS, by contrast, delegates access to a resource in just one of the storage services: the Blob, Queue, Table, or File service. For more information on service SAS, see [Constructing a Service SAS](../StorageServicesREST/Constructing-a-Service-SAS.md).  
  
> [!NOTE]
>  Stored access policies are currently not supported for account SAS.  
  
## Constructing the Account SAS URI  
 The account SAS URI consists of the URI to the resource for which the SAS will delegate access, followed by the SAS token. The SAS token is the query string that includes all of the information required to authenticate the SAS, as well as to specify the service, resource, and permissions available for access, and the time interval over which the signature is valid.  
  
### Specifying Account SAS Parameters  
 The following table describes the required and optional parameters for the SAS token.  
  
|SAS Query Parameter|Description|  
|-------------------------|-----------------|  
|`api-version`|Optional. Specifies the storage service version to use to execute the request made using the account SAS URI.|  
|`SignedVersion (sv)`|Required. Specifies the signed storage service version to use to authenticate requests made with this account SAS. Must be set to version 2015-04-05 or later.|  
|`SignedServices (ss)`|Required. Specifies the signed services accessible with the account SAS. Possible values include:<br /><br /> -   Blob (`b`)<br />-   Queue (`q`)<br />-   Table (`t`)<br />-   File (`f`)<br /><br /> You can combine values to provide access to more than one service. For example, `ss=bf` specifies access to the Blob and File endpoints.|  
|`SignedResourceTypes (srt)`|Required. Specifies the signed resource types that are accessible with the account SAS.<br /><br /> -   Service (`s`): Access to service-level APIs (*e.g.*, Get/Set Service Properties, Get Service Stats, List Containers/Queues/Tables/Shares)<br />-   Container (`c`): Access to container-level APIs (*e.g.*, Create/Delete Container, Create/Delete Queue, Create/Delete Table, Create/Delete Share, List Blobs/Files and Directories)<br />-   Object (`o`): Access to object-level APIs for  blobs, queue messages,  table entities, and files(*e.g.* Put Blob, Query Entity, Get Messages, Create File, etc.)<br /><br /> You can combine values to provide access to more than one resource type. For example, `srt=sc` specifies access to service and container resources.|  
|`SignedPermission (sp)`|Required. Specifies the signed permissions for the account SAS. Permissions are only valid if they match the specified signed resource type; otherwise they are ignored.<br /><br /> -   Read (`r`): Valid for all signed resources types (Service, Container, and Object). Permits read permissions to the specified resource type.<br />-   Write (`w`): Valid for all signed resources types (Service, Container, and Object). Permits write permissions to the specified resource type.<br />-   Delete (`d`): Valid for Container and Object resource types, except for queue messages.<br />-   List (`l`): Valid for Service and Container resource types only.<br />-   Add (`a`): Valid for the following Object resource types only: queue messages, table entities, and append blobs.<br />-   Create (`c`): Valid for the following Object resource types only: blobs and files. Users can create new blobs or files, but may not overwrite existing blobs or files.<br />-   Update (`u`): Valid for the following Object resource types only:   queue messages and table entities.<br />-   Process (`p`): Valid for the following Object resource type only: queue messages.|  
|`SignedStart (st)`|Optional. The time at which the SAS becomes valid, in an ISO 8601 format. If omitted, start time for this call is assumed to be the time when the storage service receives the request.|  
|`SignedExpiry (se)`|Required. The time at which the shared access signature becomes invalid, in an ISO 8601 format.|  
|`SignedIP (sip)`|Optional. Specifies an IP address or a range of IP addresses from which to accept requests. When specifying a range, note that the range is inclusive.<br /><br /> For example, `sip=168.1.5.65` or `sip=168.1.5.60-168.1.5.70`.|  
|`SignedProtocol (spr)`|Optional. Specifies the protocol permitted for a request made with the account SAS. Possible values are both HTTPS and HTTP (`https,http`) or HTTPS only (`https`).  The default value is `https,http`.<br /><br /> Note that HTTP only is not a permitted value.|  
|`Signature (sig)`|Required.  The signature part of the URI is used to authenticate the request made with the shared access signature.<br /><br /> The string-to-sign is a unique string constructed from the fields that must be verified in order to authenticate the request. The signature is an HMAC computed over the string-to-sign and key using the SHA256 algorithm, and then encoded using Base64 encoding.|  
  
### Specifying the Signature Validity Interval  
 The `SignedStart` and `SignedExpiry` fields must be expressed as UTC times and must adhere to a valid ISO 8601 format. Supported ISO 8601 formats include the following:  
  
-   YYYY-MM-DD  
  
-   YYYY-MM-DDThh:mmTZD  
  
-   YYYY-MM-DDThh:mm:ssTZD  
  
 For the date portion of these formats, YYYY is a four-digit year representation, MM is a two-digit month representation, and DD is a two-digit day representation. For the time portion, hh is the hour representation in 24-hour notation, mm is the two-digit minute representation, and ss is the two-digit second representation. A time designator T separates the date and time portions of the string, while a time zone designator TZD specifies the UTC time zone.  
  
### Constructing the Signature String  
 To construct the signature string for an account SAS, first construct the string-to-sign from the fields comprising the request, then encode the string as UTF-8 and compute the signature using the HMAC-SHA256 algorithm. Note that fields included in the string-to-sign must be URL-decoded.  
  
 To construct the string-to-sign for an account SAS, use the following format:  
  
```  
StringToSign = accountname + "\n" +  
    signedpermissions + "\n" +  
    signedservice + "\n" +  
    signedresourcetype + "\n" +  
    signedstart + "\n" +  
    signedexpiry + "\n" +  
    signedIP + "\n" +  
    signedProtocol + "\n" +  
    signedversion + "\n"  
  
```  
  
## Account SAS Example  
 Here is an example of an account SAS:  
  
```  
https://storagesample.blob.core.windows.net/sample-container?restype=container&comp=metadata&sv=2015-04-05ss=bfqt&srt=sco&sp=rl&se=2015-09-20T08:49Z&sip=168.1.5.60-168.1.5.70&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d  
```  
  
 The resource URI is `https://storagesample.blob.core.windows.net/sample-container?restype=container&comp=metadata`. Called with the GET/HEAD verbs, this URI returns container metadata.  
  
 The SAS token is `sv=2015-04-05&ss=bfqt&srt=sco&sp=rl&se=2015-09-20T08:49Z&sip=168.1.5.60-168.1.5.70&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d`. The table below describes each parameter value:  
  
|Parameter Value|Description|  
|---------------------|-----------------|  
|`sv=2015-04-05`|Specifies that version 2015-04-05 should be used for authenticating the SAS.|  
|`ss=bfqt`|Specifies that the SAS token provides access to the Blob, File, Queue, and Table services.|  
|`srt=sco`|Specifies that the resource types for which the SAS is valid are Service, Container, and Object. This means that the specified permissions are granted for all appropriate operations for the specified services.|  
|`sp=rl`|Specifies that the permissions for which the SAS is granted are Read (r) and List (l). This means that the SAS can be used only for operations that read data or list resources.|  
|`se=2015-09-20T08:49Z`|Specifies that the SAS expires on September 9, 2015 at 8:49 AM UTC time.|  
|`sip=168.1.5.60-168.1.5.70`|Specifies that the IP ranges from which a request that includes the SAS can be authenticated are 168.1.5.60 to 168.1.5.70.|  
|`sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d`|Specifies the signature created from the string-to-sign, as shown in the section above.|  
  
## Account SAS Permissions by Operation  
 The tables in the following sections list various APIs for each service and the signed resource types and signed permissions supported for each operation.  
  
### Blob Service  
 The following table lists Blob service operations and indicates which signed resource type and signed permissions to specify to delegate access to those operations.  
  
|Operation|Signed Service|Signed Resource Type|Signed Permission|  
|---------------|--------------------|--------------------------|-----------------------|  
|List Containers|Blob (b)|Service (s)|List (l)|  
|Get Blob Service Properties|Blob (b)|Service (s)|Read (r)|  
|Set Blob Service Properties|Blob (b)|Service (s)|Write (w)|  
|Get Blob Service Stats|Blob (b)|Service (s)|Read (r)|  
|Create Container|Blob (b)|Container (c)|Create(c) or Write (w)|  
|Get Container Properties|Blob (b)|Container (c)|Read (r)|  
|Get Container Metadata|Blob (b)|Container (c)|Read (r)|  
|Set Container Metadata|Blob (b)|Container (c)|Write (w)|  
|Lease Container|Blob (b)|Container (c)|Write (w)|  
|Delete Container|Blob (b)|Container (c)|Delete (d)|  
|List Blobs|Blob (b)|Container (c)|List (l)|  
|Put Blob (create new block blob)|Blob (b)|Object (o)|Create (c) or Write (w)|  
|Put Blob (overwrite existing block blob)|Blob (b)|Object (o)|Write (w)|  
|Put Blob (create new page blob)|Blob (b)|Object (o)|Create (c) or Write (w)|  
|Put Blob (overwrite existing page blob)|Blob (b)|Object (o)|Write (w)|  
|Get Blob|Blob (b)|Object (o)|Read (r)|  
|Get Blob Properties|Blob (b)|Object (o)|Read (r)|  
|Set Blob Properties|Blob (b)|Object (o)|Write (w)|  
|Get Blob Metadata|Blob (b)|Object (o)|Read (r)|  
|Set Blob Metadata|Blob (b)|Object (o)|Write (w)|  
|Delete Blob|Blob (b)|Object (o)|Delete (d)|  
|Lease Blob|Blob (b)|Object (o)|Write (w)|  
|Snapshot Blob|Blob (b)|Object (o)|Create (c)  or Write (w)|  
|Copy Blob (destination is new blob)|Blob (b)|Object (o)|Create (c)  or Write (w)|  
|Copy Blob (destination is an existing blob)|Blob (b)|Object (o)|Write (w)|  
|Abort Copy Blob|Blob (b)|Object (o)|Write (w)|  
|Put Block|Blob (b)|Object (o)|Write (w)|  
|Put Block List (create new blob)|Blob (b)|Object (o)|Write (w)|  
|Put Block List (update existing blob)|Blob (b)|Object (o)|Write (w)|  
|Get Block List|Blob (b)|Object (o)|Read (r)|  
|Put Page|Blob (b)|Object (o)|Write (w)|  
|Get Page Ranges|Blob (b)|Object (o)|Read (r)|  
|Append Block|Blob (b)|Object (o)|Add (a) or Write (w)|  
|Clear Page|Blob (b)|Object (o)|Write (w)|  
  
### Queue Service  
 The following table lists Queue service operations and indicates which signed resource type and signed permissions to specify to delegate access to those operations.  
  
|Operation|Signed Service|Signed Resource Type|Signed Permission|  
|---------------|--------------------|--------------------------|-----------------------|  
|Get Queue Service Properties|Queue (q)|Service (s)|Read (r)|  
|Set Queue Service Properties|Queue (q)|Service (s)|Write (w)|  
|List Queues|Queue (q)|Service (s)|List (l)|  
|Get Queue Service Stats|Queue (q)|Service (s)|Read (r)|  
|Create Queue|Queue (q)|Container (c)|Create(c) or Write (w)|  
|Delete Queue|Queue (q)|Container (c)|Delete (d)|  
|Get Queue Metadata|Queue (q)|Container (c)|Read (r)|  
|Set Queue Metadata|Queue (q)|Container (c)|Write (w)|  
|Put Message|Queue (q)|Object (o)|Add (a)|  
|Get Messages|Queue (q)|Object (o)|Process (p)|  
|Peek Messages|Queue (q)|Object (o)|Read (r)|  
|Delete Message|Queue (q)|Object (o)|Process (p)|  
|Clear Messages|Queue (q)|Object (o)|Delete (d)|  
|Update Message|Queue (q)|Object (o)|Update (u)|  
  
### Table Service  
 The following table lists Table service operations and indicates which signed resource type and signed permissions to specify to delegate access to those operations.  
  
|Operation|Signed Service|Signed Resource Type|Signed Permission|  
|---------------|--------------------|--------------------------|-----------------------|  
|Get Table Service Properties|Table (t)|Service (s)|Read (r)|  
|Set Table Service Properties|Table (t)|Service (s)|Write (w)|  
|Get Table Service Stats|Table (t)|Service (s)|Read (r)|  
|Query Tables|Table (t)|Container (c)|List (l)|  
|Create Table|Table (t)|Container (c)|Create (c) or Write (w)|  
|Delete  Table|Table (t)|Container (c)|Delete (d)|  
|Query Entities|Table (t)|Object (o)|Read (r)|  
|Insert Entity|Table (t)|Object (o)|Add (a)|  
|Insert Or Merge Entity|Table (t)|Object (o)|Add (a) or Update (u)|  
|Insert Or Replace Entity|Table (t)|Object (o)|Add (a) or Update (u)|  
|Update Entity|Table (t)|Object (o)|Update (u)|  
|Merge Entity|Table (t)|Object (o)|Update (u)|  
|Delete Entity|Table (t)|Object (o)|Delete (d)|  
  
### File Service  
 The following table lists File service operations and indicates which signed resource type and signed permissions to specify to delegate access to those operations.  
  
|Operation|Signed Service|Signed Resource Type|Signed Permission|  
|---------------|--------------------|--------------------------|-----------------------|  
|List Shares|File (f)|Service (s)|List (l)|  
|Get File Service Properties|File (f)|Service (s)|Read (r)|  
|Set File Service Properties|File (f)|Service (s)|Write (w)|  
|Get Share Stats|File (f)|Container (c)|Read (r)|  
|Create Share|File (f)|Container (c)|Create (c) or Write (w)|  
|Get Share Properties|File (f)|Container (c)|Read (r)|  
|Set Share Properties|File (f)|Container (c)|Write (w)|  
|Get Share Metadata|File (f)|Container (c)|Read (r)|  
|Set Share Metadata|File (f)|Container (c)|Write (w)|  
|Delete Share|File (f)|Container (c)|Delete (d)|  
|List Directories and Files|File (f)|Container (c)|List (l)|  
|Create Directory|File (f)|Object (o)|Create (c) or Write (w)|  
|Get Directory Properties|File (f)|Object (o)|Read (r)|  
|Get Directory Metadata|File (f)|Object (o)|Read (r)|  
|Set Directory Metadata|File (f)|Object (o)|Write (w)|  
|Delete Directory|File (f)|Object (o)|Delete (d)|  
|Create File (create new)|File (f)|Object (o)|Create (c) or Write (w)|  
|Create File (overwrite existing)|File (f)|Object (o)|Write (w)|  
|Get File|File (f)|Object (o)|Read (r)|  
|Get File Properties|File (f)|Object (o)|Read (r)|  
|Get File Metadata|File (f)|Object (o)|Read (r)|  
|Set File Metadata|File (f)|Object (o)|Write (w)|  
|Delete File|File (f)|Object (o)|Delete (d)|  
|Put Range|File (f)|Object (o)|Write (w)|  
|List Ranges|File (f)|Object (o)|Read (r)|  
|Abort Copy File|File (f)|Object (o)|Write (w)|  
|Copy File|File (f)|Object (o)|Write (w)|  
|Clear Range|File (f)|Object (o)|Write (w)|  
  
## See Also  
 [Delegating Access with a Shared Access Signature](../StorageServicesREST/Delegating-Access-with-a-Shared-Access-Signature.md)   
 [Constructing a Service SAS](../StorageServicesREST/Constructing-a-Service-SAS.md)   
 [SAS Error Codes](../StorageServicesREST/SAS-Error-Codes.md)
---
title: "Put Job"
ms.custom: na
ms.date: 05/25/2015
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 2f703ff1-d52b-43bd-81ec-90350a39e2af
caps.latest.revision: 12
author: tamram
manager: adinah
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
# Put Job
The `Put Job` operation creates a new job in the Windows Azure Import/Export service.  
  
## Request  
 The `Put Job` request may be constructed as follows. HTTPS is required. Replace `<subscription-id>` with your subscription ID, `<storage-account-name>` with the name of your storage account, and `<job-name>` with the name of your import job or export job:  
  
|Method|Request URI|  
|------------|-----------------|  
|PUT|`https://management.core.windows.net/subscription-id/services/importexport/storageaccounts/storage-account-name/jobs/jobname[?$format=format]`|  
  
### URI Parameters  
  
|Parameter|Description|  
|---------------|-----------------|  
|`format`|**Optional.** Can be used to override the `Accept` header. See the `Accept` request header for additional information.<br /><br /> The following is an example of the `$format` query parameter:<br /><br /> `$format=application/json;odata=minimalmetadata`|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Accept`|**Optional.** If specified, it must be `application/json` (which specifies the JSON Light format). Other values will result in response code 406 (`Not Acceptable`).<br /><br /> One of the following parameters can also be included:<br /><br /> `odata=minimalmetadata`<br /><br /> `odata=nometatadata`<br /><br /> `odata=fullmetadata`<br /><br /> The default parameter is `odata=minimalmetadata`.<br /><br /> The following is an example header:<br /><br /> `Accept: application/json;odata=minimalmetadata`|  
|`Accept-Language`|**Optional.** Currently only the values `en` and `en-us` are supported.|  
|`Content-Encoding`|**Optional.** If this header is specified, the value must be set to `identity`.|  
|`Content-Length`|**Required.** Specifies the length of the request body.|  
|`Content-Type`|**Optional.** If this header is specified, the value must be set to `application/json`. All other values will result in status code 406 (`Not Acceptable`).|  
|`x-ms-date`|**Optional.** If specified, the value should specify the date and time when the request is sent, in the RFC 1123 format.|  
|`x-ms-version`|**Required.** Specifies the service management version to use for this request. The value of this header must be set to `2014-05-01` or `2014-05-01`.|  
|`If-Modified-Since`|**Optional.** A DateTime value. Specify this header to perform the operation only if the resource has been modified since the specified time.|  
|`If-Unmodified-Since`|**Optional.** A DateTime value. Specify this header to perform the operation only if the resource has not been modified since the specified date/time.|  
|`If-Match`|**Optional.** An ETag value. Specify this header to perform the operation only if the resource's ETag matches the value specified.|  
|`If-None-Match`|**Optional.** An ETag value, or the wildcard character (*). Specify this header to perform the operation only if the resource's ETag does not match the value specified.<br /><br /> Specify the wildcard character (\*) to perform the operation only if the resource does not exist, and fail the operation if it does exist.|  
|`X-HTTP-Method`|**Optional.** If this header is specified, its value must be `PUT` and the HTTP verb for the request must be `GET`. The request will be processed as if it were a PUT request.|  
  
### Request Body  
 The format of the request body is as follows.  
  
```  
{  
  "odata.type":"Microsoft.Cis.Services.ImportExport.Public.Job",  
  "odata.id":"name",  
  "odata.editLink":"http://management.core.windows.net/<subscription-id>/services/importexport/jobs/name",  
  "Name":"name",  
  "Properties":{  
"StorageAccountKey": "storage-account-key",  
"ContainerSas": "container-sas",  
"Location": "location-name",  
    "Type":"job-type",  
    "FriendlyName":"human-readable-job-name",  
    "Description":"job-description",  
    "Metadata":"job-metadata",  
    "ReturnAddress":{  
      "Name":"return-name",  
      "Address":"return-address",  
      "Phone":"return-phone",  
      "Email":"return-email"  
    },  
    "ReturnShipping":{  
      "CarrierName":"carrier-name",  
      "CarrierAccountNumber":"carrier-account-number"  
    },  
    "ImportExportStatesPath":"importexport-states-path",  
    "EnableVerboseLog":enable-verbose-log,  
    "BackupDriveManifest":backup-drive-manifest  
  },  
  "DriveList":[  
    {  
      "DriveId":"drive-id",  
      "BitLockerKey":"bitlocker-key",  
      "ManifestFile":"manifest-file-path",  
      "ManifestHash":"manifest-hash-value"  
    },  
    {  
      . . .  
    },  
    . . .  
    ]  
  }  
  "Export":{  
    Blob-selection-fragment  
  }  
}  
  
Blob-selection-fragment ::=  
Blob-list-fragment | Blob-list-blob-fragment  
  
Blob-list-fragment ::=  
"BlobList":{  
  "BlobPath":[  
    "blob-path",  
    "blob-path",  
    . . .  
  ],  
  "BlobPathPrefix":[  
    "blob-prefix",  
    "blob-prefix",  
    . . .  
  ]  
}  
  
Blob-list-blob-fragment ::=  
    "BlobListBlobPath":"blob-list-blob-path"  
```  
  
 The format of the blob list blob is as follows.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
    <BlobPath>blob-path</BlobPath>  
    <BlobPath>blob-path</BlobPath>  
    . . .  
    <BlobPathPrefix>blob-prefix</BlobPathPrefix>  
    <BlobPathPrefix>blob-prefix</BlobPathPrefix>  
    . . .  
</BlobList>  
```  
  
 The following table describes the elements of the request body.  
  
|Element|Type|Description|  
|-------------|----------|-----------------|  
|`Name`|String|**Required.** The name of the import or export job. Uniquely identifies the job within the same subscription.|  
|`Properties`|property|**Required.** A list of properties for the job.|  
|`StorageAccountKey`|String|**Optional.** The storage account key. You must include either `StorageAccountKey` or `ContainerSas` in the request. `StorageAccountKey` is available with all REST versions, while `ContainerSas` is only available with REST version 2014-11-01.|  
|`ContainerSas`|String|**Optional.** The container SAS to use to import or export data to or from the storage account. You must include either `StorageAccountKey` or `ContainerSas` in the request. `StorageAccountKey` is available with all REST versions, while `ContainerSas` is only available with REST version 2014-11-01.<br /><br /> The value of `ContainerSas` must start with the container name, followed by a question mark (?) and the SAS token. For example:<br /><br /> `mycontainer?sv=2014-02-14&sr=c&si=abcde&sig=LiqEmV%2Fs1LF4loC%2FJs9ZM91%2FkqfqHKhnz0JM6bqIqN0%3D&se=2014-11-20T23%3A54%3A14Z&sp=rwdl`<br /><br /> The permissions, whether specified on the URL or in a stored access policy, must include Read, Write, and Delete for import jobs, and Read, Write and List for export jobs.<br /><br /> The `sv` (service version) parameter must be set to version 2014-02-14 or later.<br /><br /> When `ContainerSas` is specified, all blobs to be imported or exported must be within the container specified in the shared access signature. In addition, the `ImportExportStatesPath` must also include this container.|  
|`Location`|String|**Required.** The location where the job will be processed.<br /><br /> Note this may not be the same location where your storage account resides. See the [List Locations](../StorageImportExportREST/List-Locations2.md) operation to obtain the correct location.|  
|`Type`|String|**Required.** Indicates whether this is an import job or an export job.|  
|`FriendlyName`|String|**Optional.** A human-readable name for the job. May contain Unicode characters and spaces.|  
|`Description`|CDATA|**Optional.** A human-readable description of the job.|  
|`Metadata`|CDATA|**Optional.** Metadata associated with the job.|  
|`ImportExportStatesPath`|String|**Optional.** The container or virtual directory where the copy logs and backups of drive manifest files (if enabled) will be stored.<br /><br /> If a value is not specified for this element, the logs and manifest files will be written to a container or virtual directory named waimportexport. If a `StorageAccountKey` is specified on the request, then logs and manifest files will be written to a container with that name. If a `ContainerSas` is specified, then logs and manifest files will be written to a virtual directory named named `waimportexport` and located beneath the container named in the shared access signature. See [Import-Export Service Log File Format](../StorageImportExportREST/Import-Export-Service-Log-File-Format.md) for details.<br /><br /> Note that in REST version 2014-05-01, this element is called `ImportExportStatesContainer` and its value must be a container name.|  
|`EnableVerboseLog`|Boolean|`Optional.` Default value is false. Indicates whether verbose logging will be enabled. When enabled, the verbose log will contain detailed logs for each chunk copy, including status for both successful and non-successful copy operations. Regardless of whether verbose logging is enabled, warnings and errors will always be logged.<br /><br /> Log files are stored as block blobs in the container specified by the `ImportExportStatesPath` element, using the following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.<br /><br /> The addresses of the verbose logs (if enabled) and error logs are returned by the [Get Job](../StorageImportExportREST/Get-Job3.md) operation.|  
|`BackupDriveManifest`|Boolean|`Optional.` Default value is false. Indicates whether the manifest files on the drives should be copied to block blobs. If this value is true, the destination blobs will be stored in the container specified by the `ImportExportStatesPath` element.<br /><br /> Manifest files are stored as block blobs in the container specified by the `ImportExportStatesPath` element, using the following naming convention:<br /><br /> `waies/jobname_driveid_timestamp_manifest.xml`<br /><br /> The addresses of the manifest file backups are returned by the `Get Job` operation.|  
|`ReturnAddress`|property|**Optional.** Specifies the return address information for the job.|  
|`Name`|String|**Required.** The name of the recipient who will receive the hard drives when they are returned.|  
|`Address`|String|**Required.** Address of the recipient of the returned drives.|  
|`Phone`|String|**Required.** Phone number of the recipient of the returned drives.|  
|`Email`|String|**Required.** Email address of the recipient of the returned drives.|  
|`ReturnShipping`|Property|Optional. Specifies the return carrier and customer’s account with the carrier.|  
|`CarrierName`|String|Required. The carrier’s name.|  
|`CarrierAccountNumber`|String|Required. The customer’s account number with the carrier.|  
|`DriveList`|property|**Optional.** List of up to ten drives that comprise the job. The drive list is a required element for an import job; it is not specified for export jobs.|  
|`Drive`|property|**Required.** Contains information about a drive.|  
|`DriveId`|String|**Required.** The drive's hardware serial number, without spaces.|  
|`BitLockerKey`|String|**Required.** The BitLocker key used to encrypt the drive.|  
|`ManifestFile`|String|**Required.** The relative path of the manifest file on the drive.|  
|`ManifestHash`|String|**Required.** The Base16-encoded MD5 hash of the manifest file on the drive.|  
|`Export`|property|**Optional.** A property containing information about the blobs to be exported for an export job. This property is required for export jobs, but must not be specified for import jobs.|  
|`BlobList`|property|**Optional.** A list of the blobs to be exported.<br /><br /> The size of the data provided for this property must not exceed 32KB. If it is larger than 32KB, store the information as a blob in the storage account associated with the export job, and specify the `BlobListBlobPath` property to point to this blob.<br /><br /> Note that any snapshots of the specified blobs will also be exported. For block blobs, only committed blobs and blocks are exported.<br /><br /> See [Put Block List](../Topic/Put%20Block%20List.md) and [List Blobs](../Topic/List%20Blobs.md) for more information about committed and uncommitted blocks.|  
|`BlobPath`|Collection|**Optional.** A collection of `blob-path` strings.|  
|`blob-path`|String|**Required.** The relative URI to the blob, beginning with the container name. If the blob is in root container, you must explicitly specify `$root` in the path.|  
|`BlobPathPrefix`|Collection|**Optional.** A collection of `blob-prefix` strings.|  
|`blob-prefix`|String|**Required.** A blob path prefix that specifies all blobs whose relative path begins with that prefix. The prefix must begin with a forward slash "/" and must include the container name. If the container is the root container, you must explicitly specify `$root` in the path.<br /><br /> See the **Remarks** section for examples of valid blob prefix values.|  
|`BlobListBlobPath`|String|**Optional.** The relative URI to the block blob that contains the list of blob paths or blob path prefixes as defined above, beginning with the container name. If the blob is in root container, the URI must begin with `$root`.|  
  
 The following describes the general format for listing blobs in the `BlobList` blob:  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
    [<BlobPathPrefix>blob-prefix</BlobPathPrefix>]  
    . . .  
    [<BlobPath [IncludeSnapshots="true|false"]>blob-path</BlobPath>]  
    . . .  
    [<BlobPath SnapshotTime="snapshot-time">blob-path</BlobPath>]  
    . . .  
</BlobList>  
  
```  
  
 The elements and attributes of the XML format are defined as follows.  
  
|XML Element|Type|Description|  
|-----------------|----------|-----------------|  
|BlobList|Root element|Required. Contains a list of blob paths or prefixes for the blobs to be exported.|  
|BlobList/BlobPathPrefix|String|Optional. A blob path prefix that specifies all blobs whose relative path begins with that prefix. The prefix must begin with a forward slash "/" and must include the container name. If the container is the root container, you must explicitly specify $root in the path.|  
|BlobList/BlobPath|String|Optional. The relative URI to the blob, beginning with the container name. If the blob is in root container, you must explicitly specify $root in the path.|  
|BlobList/BlobPath/@IncludeSnapshots|Attribute, Boolean|Optional. Specifies whether to include all snapshots of the blob. The default value is true.|  
|BlobList/BlobPath/@SnapshotTime|Attribute, DateTime|Optional. Specifies the snapshot identifier for a blob snapshot.|  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 201 (Created).  
  
### Response Headers  
 The response for this operation includes the following headers.  
  
|Response Header|Description|  
|---------------------|-----------------|  
|`Content-Encoding`|The value of this header will always be `identity`.|  
|`Content-Length`|The length of the content returned in the response.|  
|`Content-Type`|Specifies the format in which the results are returned. The value of this header will always be `application/json`.|  
|`DataServiceId`|The address of the job being created.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
|`ETag`|Contains a value that the client can use to perform conditional operations by using the `If-Match` or `If-None-Match` request header.|  
|`Last-Modified`|The date/time that the job was last modified. The date format follows RFC 1123. For more information, see Representation of Date/Time Values in Headers.|  
|`x-ms-request-id`|A value that uniquely identifies a request made against the Import/Export service.|  
|`x-ms-version`|Indicates the version of the Import/Export service used to execute the request.|  
  
### Response Body  
 If the request fails, the response body will contain the following error message:  
  
```  
{  
  "odata.error": {  
    "code": "http-code",  
    "message": {  
        "lang": "en-US",  
        "value": "detailed-error-message"  
    },  
    "azure.values": [  
      { "ExtendedCode": "extended-error-code" },  
      { "ExtendedInformation": "extended-information" }  
    ]  
  }  
}  
```  
  
|Element|Type|Description|  
|-------------|----------|-----------------|  
|`http-code`|String|The standard HTTP status code returned when the request fails.|  
|`detailed-error-message`|String|A human-readable description of the error.|  
|`Extended-code`|String|A predefined error code, if applicable.|  
|`Extended-information`|String|Additional information provided to diagnose the error.|  
  
## Sample Request and Response  
 The following shows a sample request and response for the `Put Job` operation.  
  
### Request  
  
```  
PUT https://management.core.windows.net/afb1a4eb-bc88-4ce1-b1af-dfec80067464/services/importexport/storageaccounts/xttest/jobs/MySampleJob?timeout=3600 HTTP/1.1  
x-ms-version: 2014-05-01  
x-ms-date: Wed, 30 Apr 2014 00:23:50 GMT  
DataServiceVersion: 3.0;  
Content-Type: application/json  
Accept: application/json  
Host: management.core.windows.net  
Content-Length: 1232  
Expect: 100-continue  
Connection: Keep-Alive  
  
{  
  "odata.type":"Microsoft.Cis.Services.ImportExport.Public.Job","odata.id":"MySampleJob","odata.editLink":"https://management.core.windows.net/afb1a4eb-bc88-4ce1-b1af-dfec80067464/services/importexport/jobs/MySampleJob","Name":"MySampleJob","Properties":{  
    "StorageAccountName":"xttest","StorageAccountKey":"SaXzhgVbqJ32nhPSibJAO5pe8z6G2rPhrsFGZW52kAnJxegjw9U9Lucw9AljfFRlWCpIo4gsB6Ecl+eRoGvd/A==","Location":"South Central US","Type":"Import","FriendlyName":"A sample job using Windows Azure Import/Export service.","Description":"Optional more detailed description about this job.","ReturnAddress":{  
      "Name":"John Doe","Address":"One Microsoft Way, Redmond, WA 98052","Phone":"1-800-000-0000","Email":"johndoe@outlook.com"  
    },"EnableVerboseLog":true,"BackupDriveManifest":true  
  },"DriveList":[  
    {  
      "DriveId":"1W0F9LV1","BitLockerKey":"259358-100188-581471-154165-090552-296406-410091-426844","ManifestFile":"\\DriveManifest.xml","ManifestHash":"B306C4B34DAA0E99957A4B9C779D2FA2"  
    },{  
      "DriveId":"9WM3NZFS","BitLockerKey":"360294-634645-210485-401192-415272-513568-389334-516043","ManifestFile":"\\DriveManifest.xml","ManifestHash":"DDBEDA902DABD438D2C40B2744C64B1D"  
    }  
  ]  
}  
```  
  
### Response  
  
```  
HTTP/1.1 201 Created  
Cache-Control: no-cache  
Transfer-Encoding: chunked  
Content-Encoding: identity  
Content-Language: en-us  
Last-Modified: Wed, 30 Apr 2014 00:23:52 GMT  
ETag: W/"datetime'2014-04-30T00%3A23%3A52.6173161Z'"  
Server: 1.0.6198.70 (rd_rdfe_stable.140426-2318) Microsoft-HTTPAPI/2.0  
x-ms-servedbyregion: ussouth2  
x-ms-version: 2014-05-01  
x-ms-request-id: d84d1c93200e94e5a599debd536f7b06  
Date: Wed, 30 Apr 2014 00:23:52 GMT  
  
0  
```  
  
## Remarks  
 A subscription may have up to twenty jobs active at any given time, not counting jobs that are in the `Completed` state. Each job may be in one of several different job states; in each state, operations are expected to complete within a certain period of time, or the job will be internally marked as faulted and an investigation will be conducted.  
  
 Each job may be comprised of up to ten drives for import or export. To import data that spans more than ten drives, you'll need to create additional jobs.  
  
 Note that if you specify a job name that is already associated with a job in the same subscription that is in any state other than `Creating`, the new `Put Job` request will be rejected, regardless of any conditional headers specified. If you wish to reuse the same job name, you must first complete the existing job and then delete it.  
  
 To update properties of an existing job, you can call the [Update Job Properties](../StorageImportExportREST/Update-Job-Properties.md) operation.  
  
 After you create a job, you must ship your disks within two weeks. If the disks are not shipped within that interval, the job will automatically be deleted by the Windows Azure Import/Export service.  
  
 The service will automatically delete a completed job after 90 days. You can explicitly delete the job prior to that time by calling the [Delete Job](../StorageImportExportREST/Delete-Job1.md) operation.  
  
 When you create an export job, you can specify the blobs to be exported in any of these ways:  
  
-   You can specify a full blob path to export a single blob.  
  
-   You can specify a blob path prefix to export all blobs that begin with the prefix. The prefix must begin with a forward slash and all or part of the container name.  
  
-   You can specify a relative URI to a blob in the storage account that contains a list of blobs to export.  
  
-   The following table shows some examples of valid blob paths and prefixes:  
  
|Prefix|Matches These Blobs|  
|------------|-------------------------|  
|`/picturecontainer`|All blobs in container `picturecontainer`|  
|`/bob`|All blobs in containers `bob` and `bobkids`|  
|`/bob/`|All blobs in container `bob`, but not `bobkids`, `picturecontainer` or `videocontainer`|  
|`/picturecontainer/image`|Blobs `picturecontainer/image`, `picturecontainer/image.png`, `picturecontainer/ image2.png`, `picturecontainer/image/photo.png`, and `picturecontainer/imagefiles/photo.png`|  
|`/$root/`|All blobs in the root container|  
|`/`|All blobs in all containers, including the root container.|  
  
 If a blob to be exported is currently leased, the service attempts to create a snapshot of the blob and export the snapshot instead of the original blob. If a snapshot cannot be created, the blob will be skipped for the current export job but will be included in the incomplete blob list (see [Get Job](../StorageImportExportREST/Get-Job3.md)).  
  
### Conditional Headers  
 You can call `Put Job` with conditional headers specified to create the job only when certain conditions are met. When specifying conditional headers, keep in mind the following:  
  
-   If a request specifies both the `If-None-Match` and `If-Modified-Since` headers, the request is evaluated based on the criteria specified in `If-None-Match`.  
  
-   If a request specifies both the `If-Match` and `If-Unmodified-Since` headers, the request is evaluated based on the criteria specified in `If-Match`.  
  
-   With the exception of the two combinations of conditional headers listed above, a request may specify only a single conditional header. Specifying more than one conditional header results in status code 400 (`Bad Request`).  
  
 The following table indicates the response codes returned for an unmet condition for each conditional header:  
  
|Conditional header|Response code if condition has not been met|  
|------------------------|-------------------------------------------------|  
|`If-Modified-Since`|Precondition Failed (412)|  
|`If-Unmodified-Since`|Precondition Failed (412)|  
|`If-Match`|Precondition Failed (412)|  
|`If-None-Match`|Precondition Failed (412)|  
  
## See Also  
 [Import/Export Service Operations](../StorageImportExportREST/Azure-Import-Export-Service-Operations.md)
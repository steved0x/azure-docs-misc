---
title: "Update Job Properties"
ms.custom: na
ms.date: 05/25/2015
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 6f83d480-c09e-4e3b-b096-46e140e8c93d
caps.latest.revision: 13
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
# Update Job Properties
The `Update Job Properties` operation updates specific properties of a job. You can call this operation to notify the Import/Export service that the hard drives comprising the import or export job have been shipped to the Microsoft data center. An `Update Job Properties` request can also be used to cancel an existing job.  
  
## Request  
 The `Update Job Properties` request may be constructed as follows. HTTPS is required. Replace `<subscription-id>` with your subscription ID, `<storage-account-name>` with the name of your storage account, and `<jobname>` with the name of your job:  
  
|Method|Request URI|  
|------------|-----------------|  
|PATCH|`https://management.core.windows.net/subscription-id/services/importexport/storageacounts/storage-acount-name/jobs/jobname[?$format=format]`|  
  
## URI Parameters  
  
|Parameter|Description|  
|---------------|-----------------|  
|`format`|**Optional.** Can be used to override the `Accept` header. See the `Accept` header for additional information.<br /><br /> The following is an example of the `$format` query parameter:<br /><br /> `$format=application/json;odata=minimalmetadata`|  
  
## Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Accept`|**Optional.** If specified, it must be `application/json` (which specifies the JSON Light format). Other values will result in response code 406 (`Not Acceptable`).<br /><br /> One of the following parameters can also be included:<br /><br /> `odata=minimalmetadata`<br /><br /> `odata=nometatadata`<br /><br /> `odata=fullmetadata`<br /><br /> The default parameter is `odata=minimalmetadata`.<br /><br /> The following is an example header:<br /><br /> `Accept: application/json;odata=minimalmetadata`|  
|`Accept-Language`|**Optional.** Currently only the values `en` and `en-us` are supported.|  
|`Content-Encoding`|**Optional.** If this header is specified, the value must be set to `identity`.|  
|`Content-Length`|**Optional.** Specifies the length of the request body.|  
|`Content-Type`|**Optional.** If this header is specified, the value must be set to `application/json`. All other values will result in status code 406 (`Not Acceptable`).|  
|`x-ms-date`|**Optional.** If specified, the value should specify the date and time when the request is sent, in the RFC 1123 format.|  
|`x-ms-version`|**Required.** Specifies the service management version to use for this request. The value of this header must be set to `2014-05-01` or `2014-11-01`.|  
|`If-Modified-Since`|**Optional.** A DateTime value. Specify this header to perform the operation only if the resource has been modified since the specified time.|  
|`If-Unmodified-Since`|**Optional.** A DateTime value. Specify this header to perform the operation only if the resource has not been modified since the specified date/time.|  
|`If-Match`|**Optional.** An ETag value. Specify this header to perform the operation only if the resource's ETag matches the value specified.|  
|`If-None-Match`|**Optional.** An ETag value, or the wildcard character (*). Specify this header to perform the operation only if the resource's ETag does not match the value specified.<br /><br /> Specify the wildcard character (\*) to perform the operation only if the resource does not exist, and fail the operation if it does exist.|  
|`X-HTTP-Method`|Optional. If this header is specified, its value must be PATCH and the request HTTP verb must be GET. The request will be processed as if it were a PATCH request.|  
  
## Request Body  
 The format of the XML request body is as follows.  
  
```  
{  
  "odata.type":"Microsoft.Cis.Services.ImportExport.Public.Job",  
  "odata.id":"name",  
  "odata.editLink":"http://management.core.windows.net/<subscription-id>/services/importexport/jobs/name",  
  "Name":"name",  
  "Properties":{  
    "FriendlyName":"human-readable-job-name",  
    "Description":"job-description",  
"Metadata":"job-metadata",  
"State":"Shipping",  
"CancelRequested":true,  
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
"DeliveryPackage":{  
  "CarrierName":"carrier-name"  
  "TrackingNumber":"tracking-number",  
  "DriveCount":drive-count,  
  "ShipDate":"ship-date"  
},  
    "EnableVerboseLog":enable-verbose-log,  
    "BackupDriveManifest":backup-drive-manifest  
  }  
}  
```  
  
 The following table describes the elements of the request body.  
  
|Element|Type|Description|  
|-------------|----------|-----------------|  
|`Properties`|property|Required. The list of properties for the job.|  
|`FriendlyName`|String|Optional. A human-readable name for the job. May contain Unicode characters and spaces.|  
|`Description`|CDATA|Optional. A human-readable description of the job.|  
|`Metadata`|CDATA|Optional. Metadata associated with the job.|  
|`CancelRequested`|Boolean|Optional. If specified, the value must be `true`. The service will attempt to cancel the job.|  
|`State`|String|Optional. If specified, the value must be `Shipping`, which tells the Import/Export service that the package for the job has been shipped. The `ReturnAddress` and `DeliveryPackage` properties must have been set either in this request or in a previous request, otherwise the request will fail.|  
|`ReturnAddress`|property|Optional. Specifies the return address information for the job.|  
|`Name`|String|Required. The name of the recipient who will receive the hard drives when they are returned.|  
|`Address`|String|Required. Address of the recipient of the returned drives.|  
|`Phone`|String|Required. Phone number of the recipient of the returned drives.|  
|`Email`|String|Required. Email address of the recipient of the returned drives.|  
|`ReturnShipping`|Property|Optional. Specifies the return carrier and customer’s account with the carrier.|  
|`CarrierName`|String|Required. The carrier’s name.|  
|`CarrierAccountNumber`|String|Required. The customer’s account number with the carrier.|  
|`DeliveryPackage`|property|Optional. Contains information about the package being shipped by the customer to the Microsoft data center.|  
|`CarrierName`|String|Required. The name of the carrier.|  
|`TrackingNumber`|String|Required. The tracking number of the package.|  
|`DriveCount`|Integer|Optional. The number of drives included in the shipment.|  
|`ShipDate`|Date|Optional. The date when the package is shipped.|  
|`EnableVerboseLog`|Boolean|Optional. Indicates whether verbose logging is enabled; see [Put Job](../StorageImportExportREST/Put-Job.md) for details.|  
|`BackupDriveManifest`|Boolean|Optional. Indicates whether drive manifest files are backed up to block blobs; see [Put Job](../StorageImportExportREST/Put-Job.md) for details.|  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 204 (`No Content`).  
  
### Response Headers  
  
|Response Header|Description|  
|---------------------|-----------------|  
|`Content-Encoding`|Only applicable for error responses. The value of this header will always be `identity`.|  
|`Content-Length`|Only applicable for error responses. When the response body is chunked, this header is not included.|  
|`Content-Type`|Only applicable for error responses. The value of this header will always be `application/json`.|  
|`DataServiceId`|The address of the job being updated.|  
|`Date`|A UTC date/time value generated by the service that indicates the time at which the response was initiated.|  
|`ETag`|Contains a value that the client can use to perform conditional operations by using the `If-Match` or `If-None-Match` request header.|  
|`Last-Modified`|The date/time that the job was last modified. The date format follows RFC 1123. For more information, see [Representation of Date-Time Values in Headers](../Topic/Representation%20of%20Date-Time%20Values%20in%20Headers.md).|  
|`x-ms-request-id`|A value that uniquely identifies a request made against the Import/Export service.|  
|`x-ms-version`|Indicates the version of the Import/Export service used to execute the request.|  
  
### Response Body  
 If the request succeeds, there is no response body.  
  
 If the request fails, the response body will contain the following error message format:  
  
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
 The following shows a sample request and response for the `Update Job Properties` operation.  
  
### Request  
  
```  
PATCH https://management.core.windows.net/afb1a4eb-bc88-4ce1-b1af-dfec80067464/services/importexport/storageaccounts/xttest/jobs/MySampleJob?timeout=3600 HTTP/1.1  
x-ms-version: 2014-05-01  
x-ms-date: Wed, 30 Apr 2014 00:25:41 GMT  
DataServiceVersion: 3.0;  
Content-Type: application/json  
Accept: application/json  
Host: management.core.windows.net  
Content-Length: 388  
Expect: 100-continue  
Connection: Keep-Alive  
  
{  
  "odata.type":"Microsoft.Cis.Services.ImportExport.Public.Job","odata.id":"MySampleJob","odata.editLink":"https://management.core.windows.net/afb1a4eb-bc88-4ce1-b1af-dfec80067464/services/importexport/jobs/MySampleJob","Properties":{  
    "DeliveryPackage":{  
      "CarrierName":"FedEx","TrackingNumber":"999999999999","DriveCount":2,"ShipDate":"4/30/2014 12:25:40 AM"  
    }  
  }  
}  
```  
  
### Response  
  
```  
HTTP/1.1 200 OK  
Cache-Control: no-cache  
Transfer-Encoding: chunked  
Content-Encoding: identity  
Content-Language: en-us  
Last-Modified: Wed, 30 Apr 2014 00:23:52 GMT  
ETag: W/"datetime'2014-04-30T00%3A23%3A52.6173161Z'"  
Server: 1.0.6198.70 (rd_rdfe_stable.140426-2318) Microsoft-HTTPAPI/2.0  
x-ms-servedbyregion: ussouth2  
DataServiceId: https://management.core.windows.net/afb1a4eb-bc88-4ce1-b1af-dfec80067464/services/importexport/jobs/MySampleJob  
x-ms-version: 2014-05-01  
x-ms-request-id: 8d21cb4a7ea496a1b4b71b6dfcc8e287  
Date: Wed, 30 Apr 2014 00:25:43 GMT  
  
0  
```  
  
## Remarks  
 The `Update Job Properties` operation enables you to update properties of a job after the job has been created. After you ship your drives to a Windows Azure data center, you are required to update certain fields before your job can be processed.  
  
 Some properties, like the `Metadata` property, may be updated at any time during the lifetime of a job, whereas the `DeliveryPackage` property can only be updated prior to the package's arrival at the Windows Azure data center.  
  
 The table below describes when various properties can be changed.  
  
|Property|Comments|  
|--------------|--------------|  
|`FriendlyName`|May be updated at any time.|  
|`Description`|May be updated at any time.|  
|`Metadata`|May be updated at any time.|  
|`State`|May only be updated when the status of the job is `Creating`.|  
|`CancelRequested`|May be updated when the status of the job is `Creating`, `Shipping`, or `Transferring`.|  
|`ReturnAddress`|May be updated until the status of the job is `Packaging`.|  
|`ReturnShipping`|May be updated until the status of the job is `Packaging`.|  
|`DeliveryPackage`|May be updated until all drives arrive at the datacenter.|  
|`EnableVerboseLog`|May be updated until the status of the job is `Packaging`.|  
|`BackupDriveManifest`|May be updated until the status of the job is `Packaging`.|  
|`ManagementCertificate`|May be updated until the status of the job is `Transferring`.|  
  
 You can call `Update Job Properties` to update your shipping information, or to cancel a job. These two functions are described in detail below.  
  
### Shipping  
 After you ship your drives, you must call `Update Job Properties` with the `State` property set to `Shipping`, and with the `ReturnAddress` and `DeliveryPackage` properties set to valid values. In this way you notify the Import/Export service that your drives have been shipped.  
  
> [!IMPORTANT]
>  Failure to set these properties or to notify the Import/Export service that the drives have shipped may result in delays in processing your import or export job.  
  
### Cancellation  
 To cancel a job, you must call `Update Job Properties` and set the `CancelRequested` property to `true`. You can cancel a job if its state is `Creating`, `Shipping`, or `Transferring,` but not if the state is `Packaging`.  
  
 When you cancel a job, any drives that have not entered the data transfer process will be skipped. The job will be completed for any drives that are already in the data transfer process.  
  
> [!NOTE]
>  The Import/Export service cancels a job on a best effort basis, but there are no guarantees about the success of a cancellation request.  
  
### Conditional Headers  
 You can call `Update Job Properties` with conditional headers specified to update the job only when certain conditions are met. When specifying conditional headers, keep in mind the following:  
  
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
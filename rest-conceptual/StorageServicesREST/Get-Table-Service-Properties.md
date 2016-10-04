---
title: "Get Table Service Properties"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 99806684-7d33-4a59-acc2-23aaf460eb31
caps.latest.revision: 19
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
# Get Table Service Properties
The `Get Table Service Properties` operation gets the properties of a storage account’s Table service, including properties for [Storage Analytics](../StorageServicesREST/Storage-Analytics.md) and CORS (Cross-Origin Resource Sharing) rules.  
  
 For detailed information about CORS rules and evaluation logic, see [CORS Support for the Storage Services](../StorageServicesREST/Cross-Origin-Resource-Sharing--CORS--Support-for-the-Azure-Storage-Services.md).  
  
## Request  
 The `Get Table Service Properties` request may be specified as follows. HTTPS is recommended. Replace `<account-name>` with the name of your storage account:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|GET|`https://<account-name>.table.core.windows.net/?restype=service&comp=properties`|HTTP/1.1|  
  
 Note that the URI must always include the forward slash (/) to separate the host name from the path and query portions of the URI. In the case of this operation, the path portion of the URI is empty.  
  
### URI Parameters  
  
|URI Parameter|Description|  
|-------------------|-----------------|  
|`restype=service&comp=properties`|Required. The combination of both query strings is required to get the Table service properties.|  
|`timeout`|Optional. The `timeout` parameter is expressed in seconds.|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, storage account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Required for all authenticated requests. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
### Request Body  
 None.  
  
## Response  
 The response includes an HTTP status code, a set of response headers, and a response body.  
  
### Status Code  
 A successful operation returns status code 200 (OK).  
  
 For information about status codes, see [Service Management Status and Error Codes](assetId:///10f8d244-4649-4063-b6c9-7a20765513fa).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response Header|Description|  
|---------------------|-----------------|  
|`x-ms-request-id`|A value that uniquely identifies a request made against the service.|  
|`x-ms-version`|Specifies the version of the operation used for the response. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
  
### Response Body  
 For version 2012-02-12 and earlier, the format of the response body is as follows:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<StorageServiceProperties>  
    <Logging>  
        <Version>version-number</Version>  
        <Delete>true|false</Delete>  
        <Read>true|false</Read>  
        <Write>true|false</Write>  
        <RetentionPolicy>  
            <Enabled>true|false</Enabled>  
            <Days>number-of-days</Days>  
        </RetentionPolicy>  
    </Logging>  
    <Metrics>  
        <Version>version-number</Version>  
        <Enabled>true|false</Enabled>  
        <IncludeAPIs>true|false</IncludeAPIs>  
        <RetentionPolicy>  
            <Enabled>true|false</Enabled>  
            <Days>number-of-days</Days>  
        </RetentionPolicy>  
    </Metrics>  
</StorageServiceProperties>  
```  
  
 Beginning with version 2013-08-15, the format of the response body is as follows:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<StorageServiceProperties>  
    <Logging>  
        <Version>version-number</Version>  
        <Delete>true|false</Delete>  
        <Read>true|false</Read>  
        <Write>true|false</Write>  
        <RetentionPolicy>  
            <Enabled>true|false</Enabled>  
            <Days>number-of-days</Days>  
        </RetentionPolicy>  
    </Logging>  
    <HourMetrics>  
        <Version>version-number</Version>  
        <Enabled>true|false</Enabled>  
        <IncludeAPIs>true|false</IncludeAPIs>  
        <RetentionPolicy>  
            <Enabled>true|false</Enabled>  
            <Days>number-of-days</Days>  
        </RetentionPolicy>  
    </HourMetrics>  
    <MinuteMetrics>  
        <Version>version-number</Version>  
        <Enabled>true|false</Enabled>  
        <IncludeAPIs>true|false</IncludeAPIs>  
        <RetentionPolicy>  
            <Enabled>true|false</Enabled>  
            <Days>number-of-days</Days>  
        </RetentionPolicy>  
    </MinuteMetrics>  
    <Cors>  
        <CorsRule>  
            <AllowedOrigins>comma-separated-list-of-allowed-origins</AllowedOrigins>  
            <AllowedMethods>comma-separated-list-of-HTTP-verb</AllowedMethods>  
            <MaxAgeInSeconds>max-caching-age-in-seconds</MaxAgeInSeconds>  
            <ExposedHeaders>comma-seperated-list-of-response-headers</ExposedHeaders>  
            <AllowedHeaders> comma-seperated-list-of-request-headers </AllowedHeaders>  
        </CorsRule>  
    </Cors>  
</StorageServiceProperties>  
  
```  
  
 The following table describes the elements of the response body:  
  
|Element Name|Description|  
|------------------|-----------------|  
|**Logging**|Groups the Azure Analytics **Logging** settings.|  
|**Metrics**|Groups the Azure Analytics **Metrics** settings. The **Metrics** settings provide a summary of request statistics grouped by API in hourly aggregates for tables.|  
|**HourMetrics**|Groups the Azure Analytics **HourMetrics** settings. The **HourMetrics** settings provide a summary of request statistics grouped by API in hourly aggregates for tables.|  
|**MinuteMetrics**|Groups the Azure Analytics **MinuteMetrics** settings. The **MinuteMetrics** settings provide request statistics for each minute for tables.|  
|**Version**|The version of Storage Analytics currently in use.|  
|**Delete**|Applies only to logging configuration. Indicates whether delete requests are being logged.|  
|**Read**|Applies only to logging configuration. Indicates whether read requests are being logged.|  
|**Write**|Applies only to logging configuration. Indicates whether write requests are being logged.|  
|**Enabled**|Indicates whether metrics is enabled for the Table service.<br /><br /> If read-access geo-redundant replication is enabled, both primary and secondary metrics are collected. If read-access geo-redundant replication is not enabled, only primary metrics are collected.|  
|**IncludeAPIs**|Applies only to metrics configuration. Indicates whether metrics generates summary statistics for called API operations.|  
|**RetentionPolicy/Enabled**|Indicates whether a retention policy is enabled for the storage service.|  
|**RetentionPolicy/Days**|Indicates the number of days that metrics or logging data is retained. All data older than this value will be deleted.|  
|**Cors**|Groups all CORS rules.|  
|**CorsRule**|Groups settings for a CORS rule.|  
|**AllowedOrigins**|A comma-separated list of origin domains that are allowed via CORS, or "*" if all domains are allowed.|  
|**ExposedHeaders**|A comma-separated list of response headers to expose to CORS clients.|  
|**MaxAgeInSeconds**|The number of seconds that the client/browser should cache a preflight response.|  
|**AllowedHeaders**|A comma-separated list of headers allowed to be part of the cross-origin request.|  
|**AllowedMethods**|A comma-separated list of HTTP methods that are allowed to be executed by the origin. For Azure Storage, permitted methods are DELETE, GET, HEAD, MERGE, POST, OPTIONS or PUT.|  
  
## Authorization  
 Only the storage account owner may call this operation.  
  
## Sample Request and Response  
 The following sample URI makes a request to get the Table service properties for the fictional storage account named *myaccount*:  
  
```  
GET https://myaccount.table.core.windows.net/?restype=service&comp=properties HTTP/1.1  
```  
  
 The request is sent with the following headers:  
  
```  
x-ms-version: 2013-08-15  
x-ms-date: Wed, 23 Oct 2013 04:49:03 GMT  
Authorization: SharedKey  
myaccount:Z1lTLDwtq5o1UYQluucdsXk6/iB7YxEu0m6VofAEkUE=  
Host: myaccount.table.core.windows.net  
```  
  
 After the request has been sent, the following response is returned:  
  
```  
HTTP/1.1 200 OK  
Content-Length: 1020  
Content-Type: application/xml  
Date: Wed, 23 Oct 2013 04:49:04 GMT  
Server: Windows-Azure-Table/1.0 Microsoft-HTTPAPI/2.0  
x-ms-request-id: cb939a31-0cc6-49bb-9fe5-3327691f2a30  
x-ms-version: 2013-08-15  
  
```  
  
 The response body is similar to the following:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<StorageServiceProperties>  
    <Logging>  
        <Version>1.0</Version>  
        <Delete>true</Delete>  
        <Read>false</Read>  
        <Write>true</Write>  
        <RetentionPolicy>  
            <Enabled>true</Enabled>  
            <Days>7</Days>  
        </RetentionPolicy>  
    </Logging>  
    <HourMetrics>  
        <Version>1.0</Version>  
        <Enabled>true</Enabled>  
        <IncludeAPIs>false</IncludeAPIs>  
        <RetentionPolicy>  
            <Enabled>true</Enabled>  
            <Days>7</Days>  
        </RetentionPolicy>  
    </HourMetrics>  
        <MinuteMetrics>  
        <Version>1.0</Version>  
        <Enabled>true</Enabled>  
        <IncludeAPIs>true</IncludeAPIs>  
        <RetentionPolicy>  
            <Enabled>true</Enabled>  
            <Days>7</Days>  
        </RetentionPolicy>  
    </MinuteMetrics>  
    <Cors>  
        <CorsRule>  
            <AllowedOrigins> http://www.fabrikam.com,http://www.contoso.com</AllowedOrigins>  
            <AllowedMethods>GET,PUT</AllowedMethods>  
            <MaxAgeInSeconds>500</MaxAgeInSeconds>  
            <ExposedHeaders>x-ms-meta-data*,x-ms-meta-customheader</ExposedHeaders>  
            <AllowedHeaders>x-ms-meta-target*,x-ms-meta-customheader</AllowedHeaders>  
        </CorsRule>  
    </Cors>  
</StorageServiceProperties>  
```  
  
## See Also  
 [Storage Analytics](../StorageServicesREST/Storage-Analytics.md)   
 [CORS Support for the Storage Services](../StorageServicesREST/Cross-Origin-Resource-Sharing--CORS--Support-for-the-Azure-Storage-Services.md)   
 [CORS HTTP specification](http://www.w3.org/TR/cors/)
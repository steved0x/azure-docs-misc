---
title: "Set Blob Service Properties"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 65424a3c-ab49-4994-865c-827409598092
caps.latest.revision: 21
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
# Set Blob Service Properties
The `Set Blob Service Properties` operation sets properties for a storage account’s Blob service endpoint, including properties for [Storage Analytics](../StorageServicesREST/Storage-Analytics.md) and CORS (Cross-Origin Resource Sharing) rules. See [CORS Support for the Storage Services](../StorageServicesREST/Cross-Origin-Resource-Sharing--CORS--Support-for-the-Azure-Storage-Services.md) for more information on CORS rules.  
  
 You can also use this operation to set the default request version for all incoming requests to the Blob service that do not have a version specified.  
  
## Request  
 The `Set Blob Service Properties` request may be specified as follows. HTTPS is recommended. Replace `<account-name>` with the name of your storage account:  
  
|Method|Request URI|HTTP Version|  
|------------|-----------------|------------------|  
|PUT|`https://<account-name>.blob.core.windows.net/?restype=service&comp=properties`|HTTP/1.1|  
  
 Note that the URI must always include the forward slash (/) to separate the host name from the path and query portions of the URI. In the case of this operation, the path portion of the URI is empty.  
  
### URI Parameters  
  
|URI Parameter|Description|  
|-------------------|-----------------|  
|`restype=service&comp=properties`|Required. The combination of both query strings is required to set the storage service properties.|  
|`timeout`|Optional. The `timeout` parameter is expressed in seconds. For more information, see [Setting Timeouts for Blob Service Operations](../StorageServicesREST/Setting-Timeouts-for-Blob-Service-Operations.md).|  
  
### Request Headers  
 The following table describes required and optional request headers.  
  
|Request Header|Description|  
|--------------------|-----------------|  
|`Authorization`|Required. Specifies the authentication scheme, storage account name, and signature. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`Date` or `x-ms-date`|Required. Specifies the Coordinated Universal Time (UTC) for the request. For more information, see [Authentication for the Azure Storage Services](../StorageServicesREST/Authentication-for-the-Azure-Storage-Services.md).|  
|`x-ms-version`|Required for all authenticated requests. Specifies the version of the operation to use for this request. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
|`x-ms-client-request-id`|Optional. Provides a client-generated, opaque value with a 1 KB character limit that is recorded in the analytics logs when storage analytics logging is enabled. Using this header is highly recommended for correlating client-side activities with requests received by the server. For more information, see [About Storage Analytics Logging](../StorageServicesREST/About-Storage-Analytics-Logging.md) and [Azure Logging: Using Logs to Track Storage Requests](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).|  
  
### Request Body  
 For version 2012-02-12 and earlier, the format of the request body is as follows:  
  
```  
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
    <!-- The DefaultServiceVersion element can only be set for the Blob service and the request must be made using version 2011-08-18 or later -->  
    <DefaultServiceVersion>default-service-version-string</DefaultServiceVersion>  
</StorageServiceProperties>  
```  
  
 For version 2013-08-15 and later, the format of the request body is as follows:  
  
```  
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
    <!-- The DefaultServiceVersion element can only be set for the Blob service and the request must be made using version 2011-08-18 or later -->  
    <DefaultServiceVersion>default-service-version-string</DefaultServiceVersion>  
</StorageServiceProperties>  
```  
  
 Beginning with version 2013-08-15, you can call `Set Blob Service Properties` with one or more root elements specified in the request body. The root elements include:  
  
-   **Logging**  
  
-   **HourMetrics**  
  
-   **MinuteMetrics**  
  
-   **Cors**  
  
-   **DefaultServiceVersion**  
  
 It is no longer necessary to specify every root element on the request. If you omit a root element, the existing settings for the service for that functionality are preserved. However, if you do specify a given root element, you must specify every child element for that element.  
  
 The following table describes the elements of the request body:  
  
|Element Name|Description|  
|------------------|-----------------|  
|**Logging**|Optional beginning with version 2013-08-15. Required for earlier versions. Groups the Azure Analytics **Logging** settings.|  
|**Metrics**|Required for version 2012-02-12 and earlier. Not applicable for version 2013-08-15 or later. Groups the Azure Analytics **Metrics** settings. The **Metrics** settings provide a summary of request statistics grouped by API in hourly aggregates for blobs.|  
|**HourMetrics**|Optional for version 2013-08-15 or later; not applicable for earlier versions. Groups the Azure Analytics **HourMetrics** settings. The **HourMetrics** settings provide a summary of request statistics grouped by API in hourly aggregates for blobs.|  
|**MinuteMetrics**|Optional for version 2013-08-15 or later; not applicable for earlier versions. Groups the Azure Analytics **MinuteMetrics** settings. The **MinuteMetrics** settings provide request statistics for each minute for blobs. For versions earlier than 2013-08-15, **MinuteMetrics** is not included in the response body.|  
|**Version**|Required if **Logging**, **Metrics**, **HourMetrics**, or **MinuteMetrics** settings are specified. The version of Storage Analytics to configure.|  
|**Delete**|Required if **Logging**, **Metrics**, **HourMetrics**, or **MinuteMetrics** settings are specified. Applies only to logging configuration. Indicates whether all delete requests should be logged.|  
|**Read**|Required if **Logging**, **Metrics**, **HourMetrics**, or **MinuteMetrics** settings are specified. Applies only to logging configuration. Indicates whether all read requests should be logged.|  
|**Write**|Required if **Logging**, **Metrics**, **HourMetrics**, or **MinuteMetrics** settings are specified. Applies only to logging configuration. Indicates whether all write requests should be logged.|  
|**Enabled**|Required. Indicates whether metrics are enabled for the Blob service.<br /><br /> If read-access geo-redundant replication is enabled, both primary and secondary metrics are collected. If read-access geo-redundant replication is not enabled, only primary metrics are collected.|  
|**IncludeAPIs**|Required only if metrics are enabled. Applies only to metrics configuration. Indicates whether metrics should generate summary statistics for called API operations.|  
|**RetentionPolicy/Enabled**|Required. Indicates whether a retention policy is enabled for the storage service.|  
|**RetentionPolicy/Days**|Required only if a retention policy is enabled. Indicates the number of days that metrics or logging data should be retained. All data older than this value will be deleted. The minimum value you can specify is `1`; the largest value is `365` (one year).|  
|**DefaultServiceVersion**|Optional. To set **DefaultServiceVersion**, you must call `Set Blob Service Properties` using version 2011-08-18 or later. **DefaultServiceVersion** indicates the default version to use for requests to the Blob service if an incoming request’s version is not specified. Possible values include version 2008-10-27 and all more recent versions. For more information on applicable versions, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).<br /><br /> Applies only to the Blob service.|  
|**Cors**|Optional. The **Cors** element is supported for version 2013-08-15 or later. Groups all CORS rules.<br /><br /> Omitting this element group will not overwrite existing CORS settings.|  
|**CorsRule**|Optional. Specifies a CORS rule for the Blob service. You can include up to five **CorsRule** elements in the request. If no **CorsRule** elements are included in the request body, all CORS rules will be deleted, and CORS will be disabled for the Blob service.|  
|**AllowedOrigins**|Required if **CorsRule** element is present. A comma-separated list of origin domains that will be allowed via CORS, or "*" to allow all domains. Limited to 64 origin domains. Each allowed origin can have up to 256 characters.|  
|**ExposedHeaders**|Required if **CorsRule** element is present. A comma-separated list of response headers to expose to CORS clients. Limited to 64 defined headers and two prefixed headers. Each header can be up to 256 characters.|  
|**MaxAgeInSeconds**|Required if **CorsRule** element is present. The number of seconds that the client/browser should cache a preflight response.|  
|**AllowedHeaders**|Required if **CorsRule** element exists. A comma-separated list of headers allowed to be part of the cross-origin request. Limited to 64 defined headers and 2 prefixed headers. Each header can be up to 256 characters.|  
|**AllowedMethods**|Required if **CorsRule** element exists. A comma-separated list of HTTP methods that are allowed to be executed by the origin. For Azure Storage, permitted methods are DELETE, GET, HEAD, MERGE, POST, OPTIONS or PUT.|  
  
## Response  
 The response includes an HTTP status code and a set of response headers.  
  
### Status Code  
 A successful operation returns status code 202 (Accepted).  
  
 For information about status codes, see [Service Management Status and Error Codes](assetId:///10f8d244-4649-4063-b6c9-7a20765513fa).  
  
### Response Headers  
 The response for this operation includes the following headers. The response may also include additional standard HTTP headers. All standard headers conform to the [HTTP/1.1 protocol specification](http://go.microsoft.com/fwlink/?linkid=150478).  
  
|Response Header|Description|  
|---------------------|-----------------|  
|`x-ms-request-id`|A value that uniquely identifies a request made against the service.|  
|`x-ms-version`|Specifies the version of the operation used for the response. For more information, see [Versioning for the Azure Storage Services](../StorageServicesREST/Versioning-for-the-Azure-Storage-Services.md).|  
  
### Response Body  
 None.  
  
## Authorization  
 Only the account owner may call this operation.  
  
## Remarks  
 The following restrictions and limitations apply to CORS rules in Azure Storage:  
  
-   A maximum of five rules can be stored.  
  
-   The maximum size of all CORS rules settings on the request, excluding XML tags, should not exceed 2 KB.  
  
-   The length of an allowed header, exposed header, or allowed origin should not exceed 256 characters.  
  
-   Allowed headers and exposed headers may be either:  
  
    -   Literal headers, where the exact header name is provided, such as **x-ms-meta-processed**. A maximum of 64 literal headers may be specified on the request.  
  
    -   Prefixed headers, where a prefix of the header is provided, such as **x-ms-meta-data\***. Specifying a prefix in this manner allows or exposes any header that begins with the given prefix. A maximum of two prefixed headers may be specified on the request.  
  
-   The methods (or HTTP verbs) specified in the **AllowedMethods** element must conform to the methods supported by Azure storage service APIs. Supported methods are DELETE, GET, HEAD, MERGE, POST, OPTIONS and PUT.  
  
 Specifying CORS rules on the request is optional. If you call `Set Blob Service Properties` without specifying the **Cors** element in the request body, any existing CORS rules are maintained.  
  
 To disable CORS, call `Set Blob Service Properties` with an empty CORS rules settings (*i.e.,*`</Cors>`) and no inner CORS rules. This call deletes any existing rules, disabling CORS for the Blob service.  
  
 All CORS rule elements are required if the **CorsRule** element is specified. The request will fail with error code 400 (`Bad Request`) if any element is missing.  
  
 Beginning with version 2013-08-15, XML settings elements will be optional so updating a specific element can be done by sending an XML that only contains the updated element and other settings will not be affected.  
  
 For detailed information about CORS rules and evaluation logic, see [CORS Support for the Storage Services](../StorageServicesREST/Cross-Origin-Resource-Sharing--CORS--Support-for-the-Azure-Storage-Services.md).  
  
## Sample Request and Response  
 The following sample URI makes a request to change the Blob service properties for the fictional storage account named *myaccount*:  
  
```  
PUT https://myaccount.blob.core.windows.net/?restype=service&comp=properties HTTP/1.1  
```  
  
 The request is sent with the following headers:  
  
```  
x-ms-version: 2013-08-15  
x-ms-date: Mon, 21 Oct 2013 04:28:19 GMT  
Authorization: SharedKey  
myaccount:Z1lTLDwtq5o1UYQluucdsXk6/iB7YxEu0m6VofAEkUE=  
Host: myaccount.blob.core.windows.net  
```  
  
 The request is sent with the following XML body:  
  
```  
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
            <AllowedOrigins>http://www.fabrikam.com,http://www.contoso.com</AllowedOrigins>  
            <AllowedMethods>GET,PUT</AllowedMethods>  
            <MaxAgeInSeconds>500</MaxAgeInSeconds>  
            <ExposedHeaders>x-ms-meta-data*,x-ms-meta-customheader</ExposedHeaders>  
            <AllowedHeaders>x-ms-meta-target*,x-ms-meta-customheader</AllowedHeaders>  
        </CorsRule>  
    </Cors>  
    <DefaultServiceVersion>2013-08-15</DefaultServiceVersion>  
</StorageServiceProperties>  
```  
  
 After the request has been sent, the following response is returned:  
  
```  
HTTP/1.1 202 Accepted  
Connection: Keep-Alive  
Transfer-Encoding: chunked  
Date: Mon, 21 Oct 2013 04:28:21 GMT  
Server: Windows-Azure-Blob/1.0 Microsoft-HTTPAPI/2.0  
x-ms-request-id: cb939a31-0cc6-49bb-9fe5-3327691f2a30  
x-ms-version: 2013-08-15  
  
```  
  
## See Also  
 [Improved HTTP Headers for Resume on Download and a Change in If-Match Conditions](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-blobs-improved-http-headers-for-resume-on-download-and-a-change-in-if-match-conditions.aspx)   
 [Storage Analytics](../StorageServicesREST/Storage-Analytics.md)   
 [CORS Support for the Storage Services](../StorageServicesREST/Cross-Origin-Resource-Sharing--CORS--Support-for-the-Azure-Storage-Services.md)   
 [CORS HTTP specification](http://www.w3.org/TR/cors/)
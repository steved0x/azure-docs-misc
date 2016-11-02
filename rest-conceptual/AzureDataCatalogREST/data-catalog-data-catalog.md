# Data Catalog

## Create or Update
Creates or updates a catalog.  
  
**Required**  
  
Azure Resource Manager requests must be **Authorized**, see [Authenticating Azure Resource Manager requests](https://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
  
### Request  
    PUT https://management.azure.com/subscriptions/<subscriptionId>/resourceGroups/<resouceGroup>/providers/Microsoft.DataCatalog/catalogs/<catalogName>  
  
#### Uri parameters  
|Name|Description|Data Type  
|---|---|---  
| subscriptionId | Subscription to provision the catalog into.|String  
| resouceGroup | All resources need to be put into a group. See [Resource groups].(https://azure.microsoft.com/documentation/articles/resource-group-overview)|String  
|catalogName|Name of the catalog.|String  
  
  
#### Header  
  
|Name|Value  
|---|---  
|Content-Type|application/json  
  
  
  
### Body Example  
  
    {  
        "location" : "North US",  
        "tags": {  
           "mykey": "myvalue",  
           "mykey2": "myvalue2",  
        }  
      
        "properties" : {  
            "sku" : "Standard",  
            "units" : 1,  
            "enableAutomaticUnitAdjustment" : false,  
            "admins" : [{"upn" : "myupn@microsoft.com", "objectId" : "99999999-…-999999999999"}],  
            "users" :  [{"upn" : "myupn@microsoft.com", "objectId" : "99999999-…-999999999999"}]  
        }  
    }  
  
### Response  
  
#### Status codes  
  
|**Code**|**Description**  
|---|---  
|200|OK. An existing annotation was updated. If the **ProvisioningState** is not "Succeeded", "Failed", or "Canceled", then the call is **asynchronous**, and is not complete. The caller needs to either poll by doing a GET on the same URL until ProvisioningState turns into one of those values or check the value returned in Azure-AsyncOperation header, and poll that location.  
|400 | Bad request.  
  
  
#### Example Response Header  
  
|Name|Value  
|---|---  
|Access-Control-Allow-Origin|*,*  
|Cache-Control|no-cache,no-cache,no-store  
|Content-Length|548  
|Content-Type|application/json; charset=utf-8  
|Date|Wed,02 Mar 2016 01:42:46 GMT  
|ETag|W/"AAAAAAABQIE="  
|Expires|-1  
  
#### Response body properties  
  
|Name| Description  
|---|---  
Sku | Either "Free" or "Standard" (case matters). Link to our pricing page that describes what this means.  
Units|  Billing granularity for Standard SKU. One unit represents 100 allowed users. Must be set to value greater than 0 if enableAutomaticUnitAdjustment is false. Must be set to 0 if enableAutomaticUnitAdjustment is true.  
enableAutomaticUnitAdjustment| Noolean setting which determines if units should be automatically calculated. This setting must be set to true in order to use security groups in the admin or allow list.  
Admins| List of catalog administrators: <br/> - upn: Universal Principal Name of the account <br/> - objectId: Azure Active Directory Object ID of the account <br/>  
Users| list of catalog users: <br/> - upn/objectId same as above  
  
  
#### Example Response Body  
  
    {  
      "id": "/subscriptions/99999999-9999-…-999999999999/resourceGroups/myRG/providers/Microsoft.DataCatalog/catalogs/ExtractorStore1",  
      "name": "...",  
      "type": "Microsoft.DataCatalog/catalogs",  
      "location": "North US",  
      "tags": {  
          "mykey": "myvalue",  
          "mykey2": "myvalue2",  
      }  
      "properties": {  
        "sku": "Standard",  
        "units": 1,  
        "admins": [  
          {  
            "upn": "myupn@microsoft.com",  
            "objectId": "99999999-…-999999999999"  
          }  
        ],  
        "successfullyProvisioned": true,  
        "enableAutomaticUnitAdjustment": false,  
        "users": [  
          {  
            "upn": "myupn@microsoft.com",  
            "objectId": "99999999-…-999999999999"  
          }  
        ]  
      }  
    }  


## Delete
Deletes a catalog.  
  
**Required**  
  
Azure Resource Manager requests must be **Authorized**, see [Authenticating Azure Resource Manager requests](https://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
    DELETE https://management.azure.com/subscriptions/<subscriptionId>/resourceGroups/<rgName>/providers/Microsoft.DataCatalog/catalogs/<catalogName>  
  
### Request  
  
#### Headers  
None  
  
#### Body Example  
None  
  
#### Example Response Headers  
|Name|Value  
|---|---  
|Access-Control-Allow-Origin|*,*  
|Cache-Control|no-cache,no-cache,no-store  
|Content-Length|0  
|Content-Type|application/json; charset=utf-8  
|Date|Wed,02 Mar 2016 01:42:46 GMT  
|Expires|-1  
  
### Response  
  
#### Status codes  
|**Code**|**Description**  
|---|---  
|200|OK. An existing annotation was updated.  
|204 | No Content (didn't exist).  
|202 | Accepted. Delete is asynchronous. In this case, the caller needs to read the Location header for an URL to poll. That URL will continue to return 202 until the operation is complete. When it stops returning 202, the response it gives back is the result of the DELETE operation.  
|400 | Bad request.  


## Get
Gets a catalog.  
  
**Required**  
  
Azure Resource Manager requests must be **Authorized**, see [Authenticating Azure Resource Manager requests](https://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
    GET https://management.azure.com/subscriptions/<subscriptionId>/resourceGroups/<resouceGroup>/providers/Microsoft.DataCatalog/catalogs/<catalogName>  
  
#### Uri parameters  
|Name|Description|Data Type  
|---|---|---  
| subscriptionId | Subscription to provision the catalog into.|String  
| resouceGroup | All resources need to be put into a group. See [Resource groups].(https://azure.microsoft.com/documentation/articles/resource-group-overview)|String  
|catalogName|Name of the catalog.|String  
  
### Request  
  
#### Header  
  
|Name|Value  
|---|---  
|Content-Type|application/json  
  
#### Body Example  
None  
  
  
#### Example Response Headers  
  
|Name|Value  
|---|---  
|Access-Control-Allow-Origin|*,*  
|Cache-Control|no-cache,no-cache,no-store  
|Content-Length|548  
|Content-Type|application/json; charset=utf-8  
|Date|Wed,02 Mar 2016 01:42:46 GMT  
|ETag|W/"AAAAAAABQIE="  
|Expires|-1  
  
#### Response body properties  
  
|Name| Description  
|---|---  
Sku | Either "Free" or "Standard" (case matters). Link to our pricing page that describes what this means.  
Units|  Billing granularity for Standard SKU. One unit represents 100 allowed users. Must be set to value greater than 0 if enableAutomaticUnitAdjustment is false. Must be set to 0 if enableAutomaticUnitAdjustment is true.  
enableAutomaticUnitAdjustment| Noolean setting which determines if units should be automatically calculated. This setting must be set to true in order to use security groups in the admin or allow list.  
Admins| List of catalog administrators: <br/> - upn: Universal Principal Name of the account <br/> - objectId: Azure Active Directory Object ID of the account <br/>  
Users| list of catalog users: <br/> - upn/objectId same as above  
  
#### Example Response Body  
  
    {  
      "id": "/subscriptions/99999999-…-999999999999/resourceGroups/myRG/providers/Microsoft.DataCatalog/catalogs/ExtractorStore1",  
      "name": "ExtractorStore1",  
      "type": "Microsoft.DataCatalog/catalogs",  
      "location": "North US",  
      "tags": {},  
      "properties": {  
        "sku": "Standard",  
        "units": 1,  
        "admins": [  
          {  
            "upn": "myupn@microsoft.com",  
            "objectId": "99999999-…-999999999999"  
          }  
        ],  
        "enableAutomaticUnitAdjustment": false,  
        "users": [  
          {  
            "upn": "myupn@microsoft.com",  
            "objectId": "99999999-…-999999999999"  
          }  
        ]  
      }  
    }  


## List
lists all catalogs.  
  
**Required**  
  
Azure Resource Manager requests must be **Authorized**, see [Authenticating Azure Resource Manager requests](https://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
    GET https://management.azure.com/subscriptions/<subscriptionId>/resourceGroups/<resouceGroup>/providers/Microsoft.DataCatalog/catalogs  
  
#### Uri parameters  
|Name|Description|Data Type  
|---|---|---  
| subscriptionId | Subscription to provision the catalog into.|String  
| resouceGroup | All resources need to be put into a group. See [Resource groups].(https://azure.microsoft.com/documentation/articles/resource-group-overview)|String  
  
### Request  
#### Header  
  
|Name|Value  
|---|---  
|Content-Type|application/json  
  
#### Body Example  
None  
  
#### Example Response Headers  
  
|Name|Value  
|---|---  
|Access-Control-Allow-Origin|*,*  
|Cache-Control|no-cache,no-cache,no-store  
|Content-Length|570  
|Content-Type|application/json; charset=utf-8  
|Date|Wed,02 Mar 2016 01:42:46 GMT  
|Expires|-1  
  
#### Response body properties  
  
|Name| Description  
|---|---  
Sku | Either "Free" or "Standard" (case matters). Link to our pricing page that describes what this means.  
Units|  Billing granularity for Standard SKU. One unit represents 100 allowed users. Must be set to value greater than 0 if enableAutomaticUnitAdjustment is false. Must be set to 0 if enableAutomaticUnitAdjustment is true.  
enableAutomaticUnitAdjustment| Noolean setting which determines if units should be automatically calculated. This setting must be set to true in order to use security groups in the admin or allow list.  
Admins| List of catalog administrators: <br/> - upn: Universal Principal Name of the account <br/> - objectId: Azure Active Directory Object ID of the account <br/>  
Users| list of catalog users: <br/> - upn/objectId same as above  
  
#### Example Response Body  
  
    {  
      "value": [  
        {  
          "id": "/subscriptions/99999999-…-999999999999/resourceGroups/myRG/providers/Microsoft.DataCatalog/catalogs/ExtractorStore1",  
          "name": "ExtractorStore1",  
          "type": "Microsoft.DataCatalog/catalogs",  
          "location": "North US",  
          "tags": {},  
          "properties": {  
            "sku": "Standard",  
            "units": 1,  
            "admins": [  
              {  
                "upn": "myupn@microsoft.com",  
                "objectId": "99999999-…-999999999999"  
              }  
            ],  
            "successfullyProvisioned": true,  
            "enableAutomaticUnitAdjustment": false,  
            "users": [  
              {  
                "upn": "myupn@microsoft.com",  
                "objectId": "99999999-…-999999999999"  
              }  
            ]  
          }  
        }  
      ]  
    }  


## Update
Updates a Catalog.  
  
**Required**  
  
Azure Resource Manager requests must be **Authorized**, see [Authenticating Azure Resource Manager requests](https://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
    PATCH https://management.azure.com/subscriptions/<subscriptionId>/resourceGroups/<resouceGroup>/providers/Microsoft.DataCatalog/catalogs/<catalogName>  
  
#### Uri parameters  
|Name|Description|Data Type  
|---|---|---  
| subscriptionId | Subscription to provision the catalog into.|String  
| resouceGroup | All resources need to be put into a group. See [Resource groups].(https://azure.microsoft.com/documentation/articles/resource-group-overview)|String  
|catalogName|Name of the catalog.|String  
  
  
### Request  
  
|Name|Value  
|---|---  
|Content-Type|application/json  
  
  
### Body Example  
    {  
        "properties" : {  
           "admins" : [{"upn" : "myupn@google.com", "objectId" : "99999999-…-999999999999"}],  
        }  
    }  
  
### Response  
  
|**Code**|**Description**  
|---|---  
|200|OK. An existing annotation was updated. If the **ProvisioningState** is not "Succeeded", "Failed", or "Canceled", then the call is **asynchronous**, and is not complete. The caller needs to either poll by doing a GET on the same URL until ProvisioningState turns into one of those values or check the value returned in Azure-AsyncOperation header, and poll that location.  
|400 | Bad request.  
  
  
#### Example Response Header  
  
|Name|Value  
|---|---  
|Access-Control-Allow-Origin|*,*  
|Cache-Control|no-cache,no-cache,no-store  
|Content-Length|548  
|Content-Type|application/json; charset=utf-8  
|Date|Wed,02 Mar 2016 01:42:46 GMT  
|ETag|W/"AAAAAAABQIE="  
|Expires|-1  
  
  
#### Response body properties  
  
|Name| Description  
|---|---  
Sku | Either "Free" or "Standard" (case matters). Link to our pricing page that describes what this means.  
Units|  Billing granularity for Standard SKU. One unit represents 100 allowed users. Must be set to value greater than 0 if enableAutomaticUnitAdjustment is false. Must be set to 0 if enableAutomaticUnitAdjustment is true.  
enableAutomaticUnitAdjustment| Noolean setting which determines if units should be automatically calculated. This setting must be set to true in order to use security groups in the admin or allow list.  
Admins| List of catalog administrators: <br/> - upn: Universal Principal Name of the account <br/> - objectId: Azure Active Directory Object ID of the account <br/>  
Users| list of catalog users: <br/> - upn/objectId same as above  
  
#### Example Response Body  
  
    {  
      "id": "/subscriptions/99999999-…-999999999999/resourceGroups/myRG/providers/Microsoft.DataCatalog/catalogs/ExtractorStore1",  
      "name": "ExtractorStore1",  
      "type": "Microsoft.DataCatalog/catalogs",  
      "location": "North US",  
      "tags": {},  
      "properties": {  
        "sku": "Standard",  
        "units": 1,  
        "admins": [  
          {  
            "upn": "myupn@google.com",  
            "objectId": "99999999-…-999999999999"  
          }  
        ],  
        "successfullyProvisioned": true,  
        "enableAutomaticUnitAdjustment": false,  
        "users": [  
          {  
            "upn": "myupn@microsoft.com",  
            "objectId": "99999999-…-999999999999"  
          }  
        ]  
      }  
    }  

---
title: "Update Catalog"
ms.custom: na
ms.date: 2016-07-21
ms.prod: azure
ms.reviewer: na
ms.service: data-catalog
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 57f987f6-b9ba-4633-8af6-e3bdd88e6573
caps.latest.revision: 6
author: spelluru
manager: jhubbard
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
# Update Catalog
Updates a Catalog.  
  
**Required**  
  
Azure Resource Manager requests must be **Authorized**, see [Authenticating Azure Resource Manager requests](https://msdn.microsoft.com/library/azure/dn790557.aspx).  
  
    PATCH https://management.azure.com/subscriptions/<subscriptionId>/resourceGroups/<resouceGroup>/providers/Microsoft.DataCatalog/catalogs/<catalogName>  
  
### Uri parameters  
|Name|Description|Data Type  
|---|---|---  
| subscriptionId | Subscription to provision the catalog into.|String  
| resouceGroup | All resources need to be put into a group. See [Resource groups].(https://azure.microsoft.com/documentation/articles/resource-group-overview)|String  
|catalogName|Name of the catalog.|String  
  
  
## Request  
  
|Name|Value  
|---|---  
|Content-Type|application/json  
  
  
## Body Example  
    {  
        "properties" : {  
           "admins" : [{"upn" : "myupn@google.com", "objectId" : "99999999-…-999999999999"}],  
        }  
    }  
  
## Response  
  
|**Code**|**Description**  
|---|---  
|200|OK. An existing annotation was updated. If the **ProvisioningState** is not "Succeeded", "Failed", or "Canceled", then the call is **asynchronous**, and is not complete. The caller needs to either poll by doing a GET on the same URL until ProvisioningState turns into one of those values or check the value returned in Azure-AsyncOperation header, and poll that location.  
|400 | Bad request.  
  
  
### Example Response Header  
  
|Name|Value  
|---|---  
|Access-Control-Allow-Origin|*,*  
|Cache-Control|no-cache,no-cache,no-store  
|Content-Length|548  
|Content-Type|application/json; charset=utf-8  
|Date|Wed,02 Mar 2016 01:42:46 GMT  
|ETag|W/"AAAAAAABQIE="  
|Expires|-1  
  
  
### Response body properties  
  
|Name| Description  
|---|---  
Sku | Either "Free" or "Standard" (case matters). Link to our pricing page that describes what this means.  
Units|  Billing granularity for Standard SKU. One unit represents 100 allowed users. Must be set to value greater than 0 if enableAutomaticUnitAdjustment is false. Must be set to 0 if enableAutomaticUnitAdjustment is true.  
enableAutomaticUnitAdjustment| Noolean setting which determines if units should be automatically calculated. This setting must be set to true in order to use security groups in the admin or allow list.  
Admins| List of catalog administrators: <br/> - upn: Universal Principal Name of the account <br/> - objectId: Azure Active Directory Object ID of the account <br/>  
Users| list of catalog users: <br/> - upn/objectId same as above  
  
### Example Response Body  
  
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

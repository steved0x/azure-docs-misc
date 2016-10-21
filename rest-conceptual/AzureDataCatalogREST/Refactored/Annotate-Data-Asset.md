---
title: "Annotate Data Asset"
ms.custom: na
ms.date: 2016-07-21
ms.prod: azure
ms.reviewer: na
ms.service: data-catalog
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: bb123f7b-7c8f-42bc-bf3f-11a4852700d7
caps.latest.revision: 20
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
# Annotate Data Asset
---
[Request](#request) | [Response](#response)
<a name="top"/>

The **Annotate Data Asset** operation annotates an asset.
etag property is optional and is used for concurrency control.
<a name="request"/>
## Request
POST https://api.azuredatacatalog.com/catalogs/{catalog_name}/views/{view_name}/{view_item_id}/{nested_view_name}?api-version={api-version}

> [AZURE.NOTE] Some HTTP client implementations may automatically re-issue requests in response to a 302 from the server, but typically strip **Authorization headers** from the request. Since the Authorization header is required to make requests to ADC, you must ensure the Authorization header is still provided when re-issuing a request to a redirect location specified by ADC. Below is sample code demonstrating this using the .NET HttpWebRequest object.

### Uri parameters

|Name|Description|Data Type
|-|-|-
|catalog_name|Name of the catalog, or "DefaultCatalog" to use the default catalog.|String
|view_name|Name of Data Asset View.|String
|view_item_id|Id of a View item.|String
|nested_view_name|Name of a nested View item.|String
|api-version|The API version.|String

### Example: Add Experts
POST https://api.azuredatacatalog.com/catalogs/DefaultCatalog/views/tables/042297b0...1be45ecd462a/experts?api-version=2016-03-30
#### Header
Content-Type: application/json
x-ms-client-request-id:   13d9f885…a92d-8a9f8cf9f707
Authorization: Bearer eyJ0eX ... FWSXfwtQ
#### Body

    {
        "etag": "59085E253E2244A59F664A2F447E675E",
        "properties":
        {
            "fromSourceSystem": false,
            "key": "22c3fa019b3945dc97143ebc3ad74cbf--1111fa019b3945dc97143ebc3ad74cbf",
            "expert":
            {
                "upn": "expert1@contoso.com",
                "objectId": "1111fa019b3945dc97143ebc3ad74cbf"
            },
        }
    }

### Example: Add Glossary Term Tags
POST https://api.azuredatacatalog.com/catalogs/DefaultCatalog/views/tables/042297b0...1be45ecd462a/termTags?api-version=2016-03-30
#### Header
Content-Type: application/json
x-ms-client-request-id:   13d9f885…a92d-8a9f8cf9f707
Authorization: Bearer eyJ0eX ... FWSXfwtQ
#### Body

    {
        "etag": "59085E253E2244A59F664A2F447E675E",
        "properties":
        {
            "fromSourceSystem": false,
            "key": "22c3fa019b3945dc97143ebc3ad74cbf--1111fa019b3945dc97143ebc3ad74cbf",
            "termId": "https://test.catalog.com/catalogs/DefaultCatalog/glossaries/DefaultGlossary/terms/ed975c9d-2fb2-49a3-b6f2-222389cefd7e",
        }
    }

### Example: Add Glossary Column Term Tags
POST https://api.azuredatacatalog.com/catalogs/DefaultCatalog/views/tables/042297b0...1be45ecd462a/columnTermTags?api-version=2016-03-30
#### Header
Content-Type: application/json
x-ms-client-request-id:   13d9f885…a92d-8a9f8cf9f707
Authorization: Bearer eyJ0eX ... FWSXfwtQ
#### Body

    {
        "etag": "59085E253E2244A59F664A2F447E675E",
        "properties":
        {
            "fromSourceSystem": false,
            "key": "22c3fa019b3945dc97143ebc3ad74cbf--1111fa019b3945dc97143ebc3ad74cbf",
            "columnName": "Col1",
            "termId": "https://test.catalog.com/catalogs/DefaultCatalog/glossaries/DefaultGlossary/terms/ed975c9d-2fb2-49a3-b6f2-222389cefd7e",
        }
    }

<a name="response"/>
## Response
### Status codes
|Code|Description
|-|-
|201|Created. The request was fulfilled and a new annotation was created.
|200|OK. An existing annotation was updated.
|412|Precondition Failed. The request was cancelled because of the ETag mismatch in at least one item.

### Content-Type
application/json
### Header
HTTP/1.1 201 Created
x-ms-request-id: 72cf83c0…058f2b2a0c68
Location: https://api.azuredatacatalog.com/catalogs/DefaultCatalog/views/tables/042297b0...1be45ecd462a/experts/22c3fa019b3945dc97143ebc3ad74cbf-1111fa019b3945dc97143ebc3ad74cbf

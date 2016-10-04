---
title: "Data Catalog REST API reference"
ms.custom: na
ms.date: 2016-07-21
ms.prod: azure
ms.reviewer: na
ms.service: data-catalog
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 61e320b1-4891-4cc6-af3a-001eac836662
caps.latest.revision: 17
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
# Data Catalog REST API reference
  
  
The Data Catalog Assets REST API is a REST-based API that provides programmatic access to **Data Catalog** resources to register, annotate and search data assets programmatically. Azure Data Catalog is a cloud-based service that you can use to register and discover enterprise data assets. The service gives you capabilities that enable any user, from analysts to data scientists to developers, to register, discover, understand, and consume data assets.  
  
The API has the concepts of a **Catalog Entry** that has a **type** and **identity**.  
  
To perform operations on Data Catalog resources, you send HTTP requests with a supported method: GET, POST, PUT, or DELETE to an endpoint that targets a resource collection or a specific resource. A Data Catalog operation requires an Azure Active Directory (AAD) access token.  
  
The Data Catalog REST API has the following operations:  
  
-   Register data asset operations: [Register Data Asset](../AzureDataCatalogREST/Register-Data-Asset.md), [Delete Data Asset](https://msdn.microsoft.com/library/mt267568.aspx), and [Search Data Asset](https://msdn.microsoft.com/library/mt267569.aspx).  
-   Annotate data asset operations: [Annotate Data Asset](../AzureDataCatalogREST/Annotate-Data-Asset.md), [Update Annotation](../AzureDataCatalogREST/Update-Annotation.md), [Get Data Asset with Annotations](https://msdn.microsoft.com/library/mt267562.aspx), and [Delete Annotation](../AzureDataCatalogREST/Delete-Annotation.md).  
  
The Data Catalog has a Search query syntax:  
  
-   [Search data assets](../AzureDataCatalogREST/Data-Catalog-Search-syntax-reference.md)  
  
To learn the types of assets and annotations supported in **Data Catalog**, see [Azure Data Catalog developer concepts](https://azure.microsoft.com/documentation/articles/data-catalog-developer-concepts/).  

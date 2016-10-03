---
title: "Data Catalog limitations"
ms.custom: na
ms.date: 2016-07-21
ms.prod: azure
ms.reviewer: na
ms.service: data-catalog
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 84c628b8-c98e-4d2e-a447-04fbff75256b
caps.latest.revision: 9
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
# Data Catalog limitations
The Data Catalog Assets REST API has the following limitations:  
  
-   Maximum annotation or asset root size in bytes: 256K.  
-   Maximum number of annotations on an asset: 1000.  
-   Maximum overall size of asset and it's annotations: 8 MB.  
-   Transactions are scoped to a single asset and its annotations. Transcations cannot span assets.  
-   Delete of an assset deletes all anntoations associated with that asset. A delete of annoation deletes all annotations beneath that annotation.  
-   Maximum length of the value for the "key" property (applicable only to non-singleton annotations): 256.
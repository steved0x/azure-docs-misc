---
title: "Data Catalog Search syntax reference"
ms.custom: na
ms.date: 2016-07-21
ms.prod: azure
ms.reviewer: na
ms.service: data-catalog
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 606d6e0f-78ce-4b0a-a60d-96f6fa3e7f4a
caps.latest.revision: 12
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
# Data Catalog Search syntax reference
**Azure Data Catalog** is a fully managed service hosted in Microsoft Azure that serves as a system of registration and system of discovery for enterprise data sources. **Azure Data Catalog** has capabilities that enable technical and non-technical users to discover, understand, and consume data sources.  
  
  
A key aspect of data discovery is the ability to search for data sources that have been registered in **Azure Data Catalog**. **Azure Data Catalog** has a  powerful search syntax that enables users to easily build queries that return the data the users need.  
  
## Search Syntax Overview  
**Azure Data Catalog** searches is similar to that used by Microsoft Windows and Microsoft Outlook, and which should be familiar to users of these tools.  
  
## Query Techniques  
  
|Technique|Use|Example  
|---|---|---  
|Basic Search|Basic search using one or more search terms.  Results are any assets that match on any property with one or more of the terms specified.|sales data  
|Property Scoping|Only return data sources where the search term is matched with the specified property|name:finance  
|Boolean Operators|Broaden or narrow a search using Boolean operations|finance NOT corporate  
|Grouping with Parenthesis|Use parentheses to group parts of the query to achieve logical isolation, especially in conjunction with Boolean operators|name:finance AND (tags:tag1 OR tags:tag2)  
|Comparison Operators|Use comparisons other than equality for properties that have numeric and date data types|creationTime>"11/05/2014"  
  
  
## Matching, Comparison, and Boolean Operators  
  
|Keyword/Symbol|Examples|Function  
|---|---|---  
|:|experts:user@domain.com tags:tag1|Use property scoping and return only those assets where a given property contains the text being searched. The semantics for the query are "prefix match".  
|=|name=Sales name="Soft Drink Sales"|Allows the user to specify an exact match. Only those assets that contain the property with exactly the value of the search term will be returned.  
|<>|experts<>user1 tags<>tag2|"Not equal to" operator. Will return only those assets that don't have the value indicated in the search query.  
|""|"social security"|Finds items that contain the exact phrase social security. There is one special case to using quotes. If quotes are used with property scoping the semantics are grouping but not exact phrasing. In this case the behavior is the same as specifying the named property twice. Example: name:"social security" will find any assets that have a name property with the word social in it or a name property with the word security in it.  
|()|(tags:tag1 AND tags:tag2) OR (name:sales AND database:salesfy15)|Finds items that contain tag1 and tag2 or have the name sales in database salesfy15. Typically used in conjunction with boolean operators  
|>,>=|timestamp>"11/05/2014"|Finds items with a modified date after 11/05/2014.  
|<,<=|timestamp<"11/05/2014" |Finds items with a date before 11/05/2014.  
|NOT|social NOT security|Finds items that contain social, but not security.  
|AND|social AND security|Finds items that contain social and security.  
|OR|social OR security|Finds items that contain social or security.  
|has:|has:tags has:description|Allow filtering and return only those assets where a given property is set (or if the property represents a collection - it holds at least one element).  
  
## Notes  
  
### Prefix semantics  
By default, all of the searches in **Azure Data Catalog** are done using a technique called **Prefix Match Semantics**. This means that any search term will start a match at the beginning of the asset's properties.  
  
  
As an example, consider two fictional assets registered in **Azure Data Catalog**  with the following names:  
  
-   SalesData  
-   Salesman Quotes  
  
A search for "sales" will return both of these assets, since their names both start with the word "sales". Future releases of **Azure Data Catalog** will include support for exact match operators.  
  
## Property Scoped Searches  
**Azure Data Catalog** query grammar supports property scoping. In the current preview, **the property scopes are case-sensitive**. That means that in order for the query to work, the actual casing of the property in the search query must match what is in the index.  
  
Searches on invalid properties (properties that don't exist) will result in an error.  
  
Quotes behave in a special way when using property scoping. Quotes in any other context indicate exact phrasing.  However, when quotes are used in property scoping the semantics are grouping.  For example name:”Sales Products” does a free text search looking on the content of the name property looking for “Sales” or “Products”.  So the semantics of:  
  
    name:”Sales Products”  
    is exactly the same as  
    name:Sales name:Products  
  
The general principle for property names in **Searchable Properties** is camel-case, which means that first letter is lower-case, and then each of the word first letters are uppercase.  
  
The most useful properties are listed below.  For the full list of properties see the Developer concepts section.  
  
|Property|Use|Example  
|---|---|---  
|name|Finds items were the search term appears in the data source name|name:finance  
|description|Finds items were the search term appears in the data source description|description:finance  
|objectType|Finds items of a specific object type, such as table, view, or KPI|objectType:table  
|sourceType|Finds items of a specific data source type, such as SQL Server or SQL Server Analysis Services Multidimensional|sourceType:"tabular"  
|tags|Finds items were the search term appears in the data source tags|tags:finance  
|timestamp|Finds items based on the date and time their metadata was most recently modified|timestamp:>"11/05/2014"  
|lastRegisteredTime|Finds items based on the date and time their metadata was registered|lastRegisteredTime:>"11/05/2014"  
|friendlyName|Finds items were the search term appears in the data source friendly name|friendlyName:finance  
|experts|Finds items were the data source expert matches the search term|experts:user@example.com experts:user  
  
You can also use the following property names along with "has:" filter to check where assets have specific properties set.  
  
|Property|Use|Example  
|---|---|---  
|previews|Finds items that contain preview|has:preview  
|documentation|Finds items that contain documentation|has:documentation  
|tableDataProfiles|Finds items that have a table profile (size, number of rows, etc.)|has:tableDataProfiles  
|columnsDataProfiles|Finds items that have a column data profile (amount of distinct values, min, max, etc.)|has:columnsDataProfiles  
  
## Search Examples  
The following shows a few Search examples.  
###Return all assets with "sales" in the name  
name:sales  
  
  
### Return all assets registered after 4/20/2015 that include "sales" in any property  
sales AND lastRegisteredTime&gt;"4/20/2015"  
  
  
### Return all assets that include sales in any property, and which do not have the Q1FY2013 tag  
sales AND tags&lt;&gt;"Q1FY2013"  
  
  
### Return all assets that don't have experts nor documentation assigned  
not has:experts and not has:documentation  

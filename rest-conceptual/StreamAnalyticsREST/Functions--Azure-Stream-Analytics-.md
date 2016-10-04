---
title: "Functions (Azure Stream Analytics)"
ms.custom: na
ms.date: 2016-03-07
ms.prod: azure
ms.reviewer: na
ms.service: stream-analytics
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 403656df-05fb-45fb-8d4d-48ebc6185d82
caps.latest.revision: 8
author: jeffstokes72
manager: jhubbard
robots: noindex,nofollow
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
# Functions (Azure Stream Analytics)
  A (User-Defined) Function provides an extensible way for a Streaming Job to transform input data to output data using a facility that is not completely described by the Transformation query. Currently Azure Machine Learning Request-Response Service (RRS) is the supported UDF framework.  
  
## Request  
 The **Function** property is a properties bag needed to completely specify the information needed to make use of an Azure Machine Learning function.  
  
```  
{  
  "type": <function type>,  
  "properties": {  
    .  
    .  
    .  
  }  
}  
  
```  
  
 **Type**: Scalar  
  
 Properties  
  
 Azure Machine Learning Request-Response Service (RRS) Endpoint  
  
 A transformation query can call out to an operationalized Azure ML Request-Response Service (RRS) endpoint to perform scoring against a trained model. The properties in the property bag are just those needed to call the operationalized RRS endpoint.  
  
 Example payload to create an Azure Machine Learning scalar function  
  
```  
{  
  "name": "scoreTweet",  
  "properties": {  
    "type": "Scalar",  
    "properties": {  
      "inputs": [  
        {  
          "dataType": "nvarchar(max)",  
          "isConfigurationParameter": false  
        }  
      ],  
      "output": {  
        "dataType": "nvarchar(max)"  
      },  
      "binding": {  
        "type": "Microsoft.MachineLearning/WebService",  
        "properties": {  
          "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77fa4a46bf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",  
          "apiKey": "apiKey",  
          "inputs": {  
            "name": "input1",  
            "columnNames": [  
              {  
                "name": "tweet",  
                "dataType": "String",  
                "mapTo": 0  
              }  
            ]  
          },  
          "outputs": [  
            {  
              "name": "Sentiment",  
              "dataType": "String"  
            }  
          ],  
          "batchSize": 100  
        }  
      }  
    }  
  }  
}  
  
```  
  
|Property|Description|  
|--------------|-----------------|  
|name|Name of the UDF|  
|Type|Scalar|  
|inputs|An array of inputs, describing the parameters of the UDF.|  
|Inputs.dataType|Data type of the UDF parameter. List of valid Azure Stream Analytics data types are  described at [Azure Stream Analytics data types](https://msdn.microsoft.com/en-us/library/azure/dn835065.aspx).|  
|Input.isConfigurationParameter|Optional. True if this parameter is expected to be a constant. Default is false.|  
|output|Described output of the UDF.|  
|Output.dataType|Data type of UDF output. List of valid Azure Stream Analytics data types are  described at [Azure Stream Analytics data types](https://msdn.microsoft.com/en-us/library/azure/dn835065.aspx).|  
|Binding|Described the physical binding for the UDF. For example, in Azure Machine Learning RRS's this described the endpoint.|  
|Binding.Type|Type of the binding. Currently **Microsoft.MachineLearning/WebService** is the only valid binding at this time.|  
|Binding.Properties|Properties for the binding. Values are dependent on the type of binding.|  
  
 Binding properties for Microsoft.MachineLearning/WebService.  
  
|Property|Description|  
|--------------|-----------------|  
|Endpoint|Request-Response execute endpoint of Azure Machine Learning Webservice. This endpoint is available from the Request-Response Endpoint documentation page in the Azure Management portal.|  
|apiKey|API key used to authenticate with Request-Response endpoint. This is available from the Azure Management portal.|  
|batchSize|Optional. Value between 10 and 1000 describing maximum number of rows for every Azure Machine Learning RRS execute request. Default is 10.|  
|Inputs|Describes the set of inputs for RRS enpoint.|  
|Inputs.name|Name of the input. This is the name provided while authoring the endpoint. The name is available from Azure Machine Learning Studio or from the RRS endpoint documentation page.|  
|Input.ColumnNames|Array describing inputs to Azure Machine Learning  endpoint|  
  
 Element properties of Input.ColumnNames  
  
|Property|Description|  
|--------------|-----------------|  
|Name|Name of the input column.|  
|dataType|Azure Machine Learning data type. List of valid types are available at [Azure Machine Learning data types](https://msdn.microsoft.com/library/azure/dn905923.aspx). These are also described in RRS endpoint documentation.|  
|MapTo|Zero based index of the UDF parameter this input maps to.|  
|Outputs|Array describing outputs from an Azure Machine Learning RRS endpoint execution.|  
  
 Element properties of Outputs  
  
|Property|Description|  
|--------------|-----------------|  
|Name|Name of the output column.|  
|dataType|Azure Machine Learning data type. List of valid types are available at [Azure Machine Learning data types](https://msdn.microsoft.com/library/azure/dn905923.aspx). These are also described in RRS endpoint documentation.|  
  
  
---
title: "DimensionBinding 資料類型 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DimensionBinding Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DimensionBinding
helpviewer_keywords: DimensionBinding data type
ms.assetid: 6163d86b-0f6c-4237-b07b-47bc7e2962c4
caps.latest.revision: "41"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ce64884dedd1e1f01e58d4f072ce712e70138e98
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="dimensionbinding-data-type-assl"></a>DimensionBinding 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定義代表資料來源之間的繫結的衍生的資料類型和[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionBinding>  
   <!-- The following elements extend Binding -->  
      <DataSourceID>...</DataSourceID>  
   <DimensionID>...</DimensionID>  
      <Persistence>...</Persistence>  
      <RefreshPolicy>...</RefreshPolicy>  
   <RefreshInterval>...</RefreshInterval>  
</DimensionBinding>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[繫結](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[DataSourceID](../../../analysis-services/scripting/properties/datasourceid-element-assl.md)， [DimensionID](../../../analysis-services/scripting/properties/dimensionid-element-assl.md)，[持續性](../../../analysis-services/scripting/properties/persistence-element-assl.md)， [RefreshInterval](../../../analysis-services/scripting/properties/refreshinterval-element-assl.md)， [RefreshPolicy](../../../analysis-services/scripting/properties/refreshpolicy-element-assl.md)|  
|衍生的元素|請參閱[繫結](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 如需有關**繫結**型別，包括之 Analysis Services 指令碼語言 (ASSL) 物件的資料表**繫結**型別和繼承階層架構的**繫結**類型，請參閱[繫結資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)項目。  
  
 如需 ASSL 中資料繫結的概觀，請參閱[資料來源和繫結 &#40;SSAS 多維度 &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.DimensionBinding>。  
  
## <a name="see-also"></a>請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

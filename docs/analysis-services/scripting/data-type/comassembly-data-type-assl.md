---
title: "ComAssembly 資料類型 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ComAssembly Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ComAssembly
helpviewer_keywords: ComAssembly data type
ms.assetid: 23c0f4b3-b6ac-4ec8-9254-74d2f84f5244
caps.latest.revision: "48"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ba15ade9aaad8586806da3cd4b19cf8998dfca62
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="comassembly-data-type-assl"></a>ComAssembly 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定義代表與相關聯之 COM 程式庫的衍生的資料類型[伺服器](../../../analysis-services/scripting/objects/server-element-assl.md)或[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。  
  
> [!IMPORTANT]  
>  COM 組件可能會造成安全性風險。 由於這項風險和其他考量，COM 組件在 [!INCLUDE[ssASversion10](../../../includes/ssasversion10-md.md)]中已經被取代。 在未來的版本中，可能不再支援 COM 組件。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ComAssembly>  
      <!-- The following elements extend Assembly -->  
   <Source>...</Source>  
</ComAssembly>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[組件](../../../analysis-services/scripting/objects/assembly-element-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[Source](../../../analysis-services/scripting/properties/source-element-comassembly-assl.md)|  
|衍生的元素|請參閱[組件](../../../analysis-services/scripting/objects/assembly-element-assl.md)([組件](../../../analysis-services/scripting/collections/assemblies-element-assl.md)集合[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)或[伺服器](../../../analysis-services/scripting/objects/server-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 **ComAssembly**項目相關聯的執行個體是 COM 程式庫包含的參考 （完整的檔案名稱或程式設計識別碼） [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]或具有特定執行個體上的資料庫[!INCLUDE[ssAS](../../../includes/ssas-md.md)]。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.ComAssembly>。  
  
## <a name="see-also"></a>請參閱  
 [ClrAssembly 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)   
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

---
title: "Hierarchy 資料類型 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Hierarchy Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Hierarchy data type
ms.assetid: 2e05917e-7e5d-4dd1-817b-4ff5647747ff
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f2f13329023783a91d94fe63c04e4e65c65fef4a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="hierarchy-data-type-assl"></a>Hierarchy 資料類型 (ASSL)
  定義代表維度中某個階層的基本資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Hierarchy>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Description>...</Description>  
   <DisplayFolder>...</DisplayFolder>  
   <Translations>...</Translations>  
   <AllMemberName>...</AllMemberName>  
   <AllMemberTranslations>...</AllMemberTranslation>  
   <MemberNamesUnique>...</MemberNamesUnique>  
   <AllowDuplicateNames>...</AllowDuplicateNames>  
   <Levels>...</Levels>  
   <Annotations>...</Annotation>  
</Hierarchy>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[AllMemberName](../../../analysis-services/scripting/properties/allmembername-element-assl.md)、 [AllMemberTranslations](../../../analysis-services/scripting/collections/allmembertranslations-element-assl.md)、 [AllowDuplicateNames](../../../analysis-services/scripting/properties/allowduplicatenames-element-assl.md)、 [Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md)、 [Description](../../../analysis-services/scripting/properties/description-element-assl.md)、 [DisplayFolder](../../../analysis-services/scripting/properties/displayfolder-element-assl.md)、 [ID](../../../analysis-services/scripting/properties/id-element-assl.md)、 [Levels](../../../analysis-services/scripting/collections/levels-element-assl.md)、 [MemberNamesUnique](../../../analysis-services/scripting/properties/membernamesunique-element-assl.md)、 [Name](../../../analysis-services/scripting/properties/name-element-assl.md)、 [Translations](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
|衍生的元素|[Hierarchy](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 SharePoint 或表格式伺服器模式的 DevelopmentMode 1 或 2 下各不支援 *MemberNamesUnique* 元素。  
  
 SharePoint 或表格式伺服器模式的 DevelopmentMode 1 或 2 下各不支援 *MemberKeysUnique* 元素。  
  
 SharePoint 或表格式伺服器模式的 DevelopmentMode 1 或 2 下各不支援 *AllowDuplicateNames* 元素。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.Hierarchy>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
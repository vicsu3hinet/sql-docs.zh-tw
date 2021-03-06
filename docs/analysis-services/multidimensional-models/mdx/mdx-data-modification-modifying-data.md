---
title: "修改資料 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying data [MDX]
- Multidimensional Expressions [Analysis Services], data modifications
- MDX [Analysis Services], data modifications
- data modifications [MDX]
ms.assetid: 363b662c-b839-4971-bbd7-1842f73ce141
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fcf75945b77c8ced0321089805f7e23fc7223821
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="mdx-data-modification---modifying-data"></a>MDX 資料修改-修改資料
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
除了使用多維度運算式 (MDX) 擷取及處理維度與 Cube 的資料之外，您還可以使用 MDX來更新或「回寫」維度與 Cube 資料。 這些更新可能是暫時性 (如同推測性或 "what if" 分析 ) 或永久性 (例如，必須根據資料分析來變更時)。  
  
 資料的更新可發生在維度或 Cube 層級：  
  
 **維度回寫**  
 您可以使用 [ALTER CUBE 陳述式 (MDX)](../../../mdx/mdx-data-definition-alter-cube.md) 陳述式來變更可寫入維度的資料，並且使用 [REFRESH CUBE 陳述式 (MDX)](../../../mdx/mdx-data-definition-refresh-cube.md) 來反映屬性值的刪除、建立及更新。 您也可以使用 ALTER CUBE 陳述式來執行複雜的作業，例如刪除階層中的整個子樹，以及將已刪除成員的子系升級。  
  
 **Cube 回寫**  
 您可以使用 [UPDATE CUBE](../../../mdx/mdx-data-manipulation-update-cube.md) 陳述式，對可寫入 Cube 進行更新。 您可以使用 UPDATE CUBE 陳述式，來更新具有指定值的 Tuple。 您可以使用 [REFRESH CUBE 陳述式 (MDX)](../../../mdx/mdx-data-definition-refresh-cube.md)，以伺服器上的更新資料來重新整理用戶端工作階段中的資料。  
  
 如需詳細資訊，請參閱[使用 Cube 回寫 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-modification-using-cube-writebacks.md)。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 查詢基礎觀念 &#40;Analysis Services &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  

---
title: "重新命名多維度資料庫 (Analysis Services) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: renaming databases
ms.assetid: 15fdaec7-f3e4-44d9-9b78-1a1d78c484e0
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2e71eba3112c7d7795c7bff342a27e081c5619d9
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="rename-a-multidimensional-database-analysis-services"></a>重新命名多維度資料庫 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]您可以在其中變更名稱的方式[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫取決於您如何連接到[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫。 若要變更現有資料庫的名稱，您必須以線上模式連接。 若要將資料庫名稱變更為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中要具現化的物件，您必須以專案模式連接。  
  
### <a name="to-change-the-database-name-in-online-mode"></a>以線上模式變更資料庫名稱  
  
1.  使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]直接連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。  
  
2.  在方案總管中，以滑鼠右鍵按一下資料庫，然後按一下 [編輯資料庫]。  
  
3.  在 **[資料庫名稱]** 文字方塊中，變更資料庫名稱。  
  
4.  按一下工具列上的 **[儲存]** 或 **[全部儲存]** 、按一下 **[檔案]** 功能表上的 **[儲存選取項目]** 或 **[全部儲存]** ，或是關閉 **[資料庫設計工具]** ，並在出現提示時按一下 **[儲存]** 。  
  
     即會在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體中更新此資料庫名稱，而且會重新整理 [方案總管] 中的資料庫物件。  
  
### <a name="to-change-the-database-name-in-project-mode"></a>在專案模式中變更資料庫名稱  
  
1.  開啟 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案。  
  
2.  在方案總管中，以滑鼠右鍵按一下 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案，然後按一下 [屬性]。  
  
3.  在 **[屬性頁]** 對話方塊中，按一下 **[組態屬性]** 區段中的 **[部署]** 。  
  
4.  將 **[資料庫]** 屬性變更為新的資料庫名稱。  
  
     下次部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案時，它將會部署成這個新的資料庫名稱； 如果此資料庫已經存在，將會覆寫它。  
  
### <a name="to-change-the-database-name-using-sql-server-management-studio"></a>若要使用 SQL Server Management Studio 變更資料庫名稱  
  
-   以滑鼠右鍵按一下 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫並編輯 Name 屬性。  
  
## <a name="see-also"></a>請參閱  
 [Analysis Services 的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [設定多維度資料庫屬性 &#40;Analysis Services &#41;](../../analysis-services/multidimensional-models/set-multidimensional-database-properties-analysis-services.md)   
 [設定 Analysis Services 專案屬性 &#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md)   
 [部署 Analysis Services 專案 &#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
  

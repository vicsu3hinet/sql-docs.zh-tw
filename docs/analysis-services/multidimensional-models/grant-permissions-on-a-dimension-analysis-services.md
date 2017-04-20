---
title: "授與維度的權限 (Analysis Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.roledesignerdialog.dimensions.f1"
helpviewer_keywords: 
  - "維度 [Analysis Services], 安全性"
  - "讀取/寫入權限"
  - "使用者存取權限 [Analysis Services], 維度"
  - "權限 [Analysis Services], 維度"
ms.assetid: be5b2746-0336-4b12-827e-131462bdf605
caps.latest.revision: 39
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 39
---
# 授與維度的權限 (Analysis Services)
  維度安全性是用來設定維度物件的權限，而不是設定它的資料。 通常，允許或拒絕存取處理作業是在設定維度權限時的主要目標。  
  
 不過，或許您的目標不是控制處理作業，而是維度的資料存取，或其所包含的屬性和階層。 例如，設有地區業務部門的公司可能想要讓該部門以外的其他部門無法看見銷售績效資訊。 若要針對不同構成份子允許或拒絕存取部分維度資料，您可以設定維度屬性和維度成員的權限。 請注意，您無法拒絕存取個別維度物件本身，僅能拒絕存取其資料。 如果您的立即目標是允許或拒絕存取維度中的成員 (包含個別屬性階層的存取權限)，請參閱[授與維度資料的自訂存取權 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)，以取得更多資訊。  
  
 這個主題的其餘部分涵蓋您可以在維度物件本身上設定的屬性，包含：  
  
-   讀取或讀取/寫入權限 (您只能從 [讀取] 或 [讀取/寫入] 中選擇；無法選擇指定「無」)。 如前所述，如果您的目標是限制存取維度資料，請參閱[授與維度資料的自訂存取權 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)，以取得詳細資料。  
  
-   處理權限 (當案例需要要求個別物件之自訂權限處理策略時，請執行這個作業)  
  
-   讀取定義權限 (通常您會執行這個動作來支援工具中的互動式處理，或為模型提供可見性。 讀取定義可在不需擁有其資料權限或修改其定義之能力的情況下，讓您看見維度的結構)。  
  
 定義維度的角色時，可用權限會視物件是否為獨立資料庫維度 (在資料庫內部但在 Cube 外部) 或 Cube 維度而改變。  
  
> [!NOTE]  
>  根據預設，Cube 維度會繼承資料庫維度的權限。 例如，如果您啟用 Customer 資料庫維度的 [讀取/寫入]，Customer Cube 維度就會繼承目前角色內容中的 [讀取/寫入]。 如果您想要覆寫權限設定，可以清除繼承的權限。  
  
## 設定資料庫維度的權限  
 資料庫維度是資料庫內的獨立物件，允許在相同模型內重複使用維度。 請考量一個可在模型中多次使用的 DATE 資料庫維度，如同 Order Date、Ship Date 及 Due Date Cube 維度。 由於 Cube 和資料庫維度是資料庫中的對等物件，因此您可以個別設定每個物件的處理權限。  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體，在物件總管中展開適當資料庫的 [角色]，然後按一下資料庫角色 (或建立新的資料庫角色)。  
  
2.  在 [維度] 窗格中，應該將維度集設為 [所有資料庫維度]。  
  
     根據預設，會將權限設為 [讀取]。  
  
     儘管可以使用 [讀取/寫入]，但還是建議您不要使用這個權限。 [讀取/寫入] 是用於維度回寫狀況 (已不再使用)。 請參閱[SQL Server 2016 中已被取代的 Analysis Services 功能](../../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md)。  
  
     只要您尚未在資料庫層級設定 [讀取定義] 和 [處理] 權限，就可以選擇性地設定個別維度物件的這些權限。 如需詳細資訊，請參閱[授與處理權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md) 和[授與物件中繼資料的讀取定義權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md)。  
  
## 設定 Cube 維度的權限  
 Cube 維度是已新增到 Cube 的資料庫維度。 嚴格來說，它們在相關聯的量值群組上具有結構相依性。 儘管您能以不可部分完成的方式來處理這些物件，但就授權而言，將 Cube 和 Cube 維度視為單一實體是合理的。  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體，在物件總管中展開適當資料庫的 [角色]，然後按一下資料庫角色 (或建立新的資料庫角色)。  
  
2.  在 [維度] 窗格中，將維度集變更為 \<Cube 名稱> **Cube 維度**。  
  
     根據預設，權限是繼承自相對應的資料庫維度。 清除 [繼承] 核取方塊，即可將權限從 [讀取] 更改為 [讀取/寫入]。 使用 [讀取/寫入] 之前，請務必閱讀上一節的注意事項。  
  
> [!IMPORTANT]  
>  如果您使用分析管理物件 (AMO) 來設定資料庫角色權限，則任何參考 Cube 之 DimensionPermission 屬性的 Cube 維度，就會切斷資料庫的 DimensionPermission 屬性的權限繼承。 如需 AMO 的詳細資訊，請參閱[使用分析管理物件 &#40;AMO&#41; 來開發](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)。  
  
## 請參閱＜  
 [角色與權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md)   
 [授與 Cube 或模型權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)   
 [授與資料採礦結構和模型的權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [授與維度資料的自訂存取權 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)   
 [授與資料格資料的自訂存取權 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
  
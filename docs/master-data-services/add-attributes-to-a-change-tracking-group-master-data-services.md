---
title: "將屬性加入至變更追蹤群組 (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "變更追蹤群組 [Master Data Services]"
  - "屬性 [Master Data Services], 變更追蹤群組"
  - "變更追蹤群組, [Master Data Services], 新增屬性"
ms.assetid: e153eb5f-70ca-4c6f-89d8-1f937ed3917d
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# 將屬性加入至變更追蹤群組 (Master Data Services)
  當您想要追蹤屬性值變更時，可以在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中將屬性新增至變更追蹤群組。  
  
> [!NOTE]  
>  將屬性加入至變更追蹤群組之後，當屬性值變更時，[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫中的屬性會標示為已變更。 建立商務規則，以根據變更來執行動作。  
  
## 必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
-   屬性必須存在，才能加入至變更追蹤群組。 如需詳細資訊，請參閱[建立文字屬性 &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)。  
  
### 若要將屬性加入至變更追蹤群組  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 [管理模型]  頁面上，從方格中選取模型，然後按一下 [實體] 。  
  
3.  在 [管理實體]  頁面上，選取您要為其建立屬性之實體的資料列。  
  
4.  按一下 **[屬性]**。  
  
5.  在 [管理屬性] 頁面上，執行下列其中一項動作。  
  
    -   如果是分葉成員的屬性，請選取 [成員類型]  清單方塊的 [分葉]  。  
  
    -   如果是合併成員的屬性，請選取 [成員類型]  清單方塊的 [合併]  。  
  
    -   如果是集合的屬性，請選取 [成員類型]  清單方塊的 [集合]  。  
  
6.  選取要編輯的屬性資料列，然後按一下 [編輯]。  
  
7.  選取 [啟用變更追蹤] 核取方塊。  
  
8.  在 [變更追蹤群組] 方塊中，輸入群組的編號。  
  
9. 按一下 **[儲存屬性]**。  
  
     對於已編輯的屬性，方格中的 [Enable Change Tracking Group (啟用變更追蹤群組)] 資料行會變更為 [Yes (Group: entered group number) (是 (群組: 已輸入群組編號))]。  
  
10. 重複此程序，加入要包含在群組中的所有屬性。 對群組中的每個屬性，使用相同的變更追蹤群組編號。  
  
## 後續步驟  
  
-   [根據屬性值變更來起始動作 &#40;Master Data Services&#41;](../master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)  
  
## 另請參閱  
 [建立文字屬性 &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)   
 [建立網域屬性 &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
  
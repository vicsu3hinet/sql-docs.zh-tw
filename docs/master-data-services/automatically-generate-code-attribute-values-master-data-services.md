---
title: "自動產生 Code 屬性值 (Master Data Services) | Microsoft Docs"
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
ms.assetid: 19b354ee-2906-4cc7-ba2f-32b4543bddcf
caps.latest.revision: 5
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 5
---
# 自動產生 Code 屬性值 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，當您希望每次建立新成員時，自動將整數指派給字碼值，請自動為實體的 Code 屬性自動產生值。  
  
## 必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
-   實體必須存在。 如需詳細資訊，請參閱[建立實體 &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)。  
  
### 若要自動產生值字碼  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 [管理模型]  頁面上，選取含有您想要編輯之實體的模型資料列，然後按一下 [實體] 。  
  
3.  在 [管理實體]  頁面上，選取您要為其產生程式碼之實體的資料列，然後按一下 [編輯] 。  
  
4.  選取 **[自動建立字碼值]** 核取方塊。  
  
5.  在 **[開始]** 方塊中，輸入開始遞增的數字。 如果成員已存在，則將根據最大的現有值設定 Code。 例如，如果最大的現有 Code 值為 299，則下一個成員的 Code 值將設為 300。  
  
6.  按一下 **[儲存]**。  
  
## 另請參閱  
 [自動建立代碼 &#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md)   
 [自動產生 Code 以外的屬性值 &#40;Master Data Services&#41;](../master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)  
  
  
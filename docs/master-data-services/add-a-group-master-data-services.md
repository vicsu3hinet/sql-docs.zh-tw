---
title: "加入群組 (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "群組 [Master Data Services], 加入"
  - "加入群組 [Master Data Services]"
ms.assetid: c7a88381-3b2c-4af7-9cf7-3a930c1abdee
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# 加入群組 (Master Data Services)
  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 的 [群組] 清單中加入群組，開始指派 Web 應用程式權限的程序。 在群組中的使用者存取 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 之前，您必須提供群組一個或多個功能區域和模型物件的權限。  
  
## 必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[使用者及群組的權限]** 功能區域的權限。  
  
### 若要加入群組  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[使用者及群組的權限]**。  
  
2.  在 [使用者] 頁面上，按一下功能表列中的 [管理群組]。  
  
3.  按一下 [加入群組]。  
  
4.  輸入群組名稱，並在名稱前面加入 Active Directory 網域名稱或伺服器電腦名稱，如下：*domain\group_name* 或 *computer\group_name*。  
  
5.  (選擇性) 按一下 **[檢查名稱]**。  
  
6.  按一下 **[確定]**。  
  
    > [!NOTE]  
    >  在使用者第一次存取 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 時，使用者的名稱就會加入至 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 使用者清單。  
  
## 後續步驟  
  
-   [指派功能區域權限 &#40;Master Data Services&#41;](../master-data-services/assign-functional-area-permissions-master-data-services.md)  
  
## 另請參閱  
 [安全性 &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)  
  
  
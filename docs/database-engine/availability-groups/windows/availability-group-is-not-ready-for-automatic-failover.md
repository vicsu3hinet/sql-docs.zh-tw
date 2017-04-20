---
title: "可用性群組尚未就緒，無法自動容錯 | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.agdashboard.agp3autofailover.issues.f1"
helpviewer_keywords: 
  - "可用性群組 [SQL Server], 原則"
ms.assetid: 28261014-342c-442a-bd89-6d04b8d4e8b7
caps.latest.revision: 12
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 12
---
# 可用性群組尚未就緒，無法自動容錯
    
## 簡介  
  
|||  
|-|-|  
|**原則名稱**|可用性群組自動容錯移轉整備|  
|**問題**|可用性群組尚未準備進行自動容錯移轉。|  
|**類別目錄**|**嚴重**|  
|**Facet**|可用性群組|  
  
## 描述  
 這項原則檢查可用性群組是否至少有一個已做好容錯移轉準備的次要複本。 當主要複本的容錯移轉模式為自動，但是可用性群組中的次要複本都未準備進行容錯移轉時，原則為狀況不良並會引發警示。  
  
 至少一個次要複本已做好自動容錯移轉的準備時，原則為狀況良好。  
  
> [!NOTE]  
>  在此 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 版本中，可能原因和解決方案的資訊位於 TechNet Wiki 上的 [Availability group is not ready for automatic failover](http://go.microsoft.com/fwlink/p/?LinkId=220851) (可用性群組尚未準備進行自動容錯移轉)。  
  
## 可能的原因  
 可用性群組尚未準備進行自動容錯移轉。 主要複本已設定為自動容錯移轉，不過次要複本尚未準備進行自動容錯移轉。 設定為自動容錯移轉的次要複本可能無法使用，或者其資料同步處理狀態目前不是 SYNCHRONIZED。  
  
## 可能的解決方案  
 此問題的可能解決方案如下：  
  
-   請確認至少一個次要複本已設定為自動容錯移轉。 如果沒有設定為自動容錯移轉的次要複本，請以同步認可將次要複本的組態更新為自動容錯移轉目標。  
  
-   使用此原則確認資料處於同步處理狀態而且自動容錯移轉目標為 SYNCHRONIZED，然後解決可用性複本上的問題。  
  
## 另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 儀表板 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
---
title: "檢視交易式發行集的資料衝突 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "衝突解決 [SQL Server 複寫], 佇列更新訂閱"
  - "佇列更新訂閱 [SQL Server 複寫]"
  - "檢視衝突資訊"
ms.assetid: 9977dd75-b0de-4376-9c13-86d80567d8aa
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# 檢視交易式發行集的資料衝突 (SQL Server Management Studio)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 複寫衝突檢視器可讓您檢視點對點異動複寫和具有佇列更新訂閱之異動複寫的衝突。 如何偵測和解決衝突的相關資訊，請參閱 [中端對端複寫的衝突偵測](../../relational-databases/replication/transactional/conflict-detection-in-peer-to-peer-replication.md) 和 [設定佇列更新衝突解決選項 & #40。SQL Server Management Studio & #41;](../../relational-databases/replication/publish/set-queued-updating-conflict-resolution-options-sql-server-management-studio.md)。  
  
 衝突資料的可用性會取決於複寫的類型和衝突保留期限而定：  
  
-   如果是點對點複寫，則在預設情況下，當散發代理程式偵測到衝突時，就會發生失敗。 衝突錯誤會記錄到錯誤記錄檔中，但是不會將任何衝突資料記錄到衝突資料表中；因此，此資料表無法供人檢視。 如果允許散發代理程式繼續進行，會將衝突記錄在本機中偵測到衝突的每一個節點上。 如需詳細資訊，請參閱 「 處理衝突 」 在 [中端對端複寫的衝突偵測](../../relational-databases/replication/transactional/conflict-detection-in-peer-to-peer-replication.md)。  
  
-   如果是佇列更新訂閱，則會針對每一個衝突提供資料。 複寫衝突檢視器可以在衝突保留期限指定的時間內使用衝突資料 (預設為 14 天)。 若要設定衝突保留期限，您可以執行以下其中一項作業：  
  
    -   指定保留值的 @conflict_retention 參數 [sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)。  
  
    -   指定的值為 **'conflict_retention'** @property 參數和 @value 參數的保留值 [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)。  
  
### 若要檢視衝突  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的適當伺服器，然後展開伺服器節點：  
  
    -   如果是點對點複寫，這會是發生衝突的節點。  
  
    -   如果是佇列更新訂閱，這會是發行者。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下您要檢視衝突，然後再按一下發行的集 **檢視衝突**。  
  
4.  在 **選取衝突資料表** 對話方塊中，選取 [發行集資料庫和資料表用來檢視衝突。  
  
5.  在複寫衝突檢視器中，您可以：  
  
    -   使用上方格右側按鈕篩選資料列。  
  
    -   在上方格內選取資料列，以便於下方格的該資料列顯示資訊。  
  
    -   在上方方格中，選取一或多個資料列，然後按一下 **移除**, ，以移除衝突中繼資料資料表中的資料列。  
  
    -   按一下屬性按鈕 (**...**) 的資料行上檢視詳細資訊有關於衝突。  
  
    -   選取 **記錄這個衝突的詳細資料** 衝突資料記錄到檔案。 若要指定檔案的位置，請指向 **檢視** 功能表，然後再按一下 **選項**。 輸入值，或按一下 [瀏覽按鈕 (**...**)，然後瀏覽至適當的檔案。 按一下 [ **確定** 關閉 **選項** 對話方塊。  
  
6.  關閉複寫衝突檢視器。  
  
## 另請參閱  
 [點對點異動複寫](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [佇列更新衝突偵測和解決](../../relational-databases/replication/transactional/queued-updating-conflict-detection-and-resolution.md)  
  
  
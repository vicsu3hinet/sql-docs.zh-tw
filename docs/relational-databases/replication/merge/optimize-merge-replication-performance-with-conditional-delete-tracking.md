---
title: "使用條件式刪除追蹤最佳化合併式複寫效能 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "條件式刪除追蹤 [SQL Server 複寫]"
  - "合併式複寫 [SQL Server 複寫], 條件式刪除追蹤"
  - "發行項 [SQL Server 複寫], 條件式刪除追蹤"
ms.assetid: 58f120a3-ea3a-4e97-93f0-0eb4e580ecf2
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# 使用條件式刪除追蹤最佳化合併式複寫效能
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 您可以使用合併式複寫，來指定一或多個發行項的刪除不由複寫觸發程序與系統資料表來追蹤。 如果您為發行項指定了此選項，則不會從「發行者」或任何「訂閱者」追蹤或複寫這些刪除。 此選項可支援一些應用程式實例，並在不需要或不想要對刪除的複寫時提供效能最佳化。 有三種方法可以提升效能：不儲存刪除的中繼資料；同步處理期間不列舉刪除；不在「訂閱者」端複寫及套用刪除。  
  
> [!NOTE]  
>  若要使用僅限下載發行項，發行集的相容性層級必須至少為 90RTM。  
  
 如果應用程式要求複寫某些刪除，而其餘的則不複寫 (例如批次刪除)，則可以在發行集建立或在 ON 與 OFF 之間切換時指定選項。 以下範例說明此選項在應用程式中可能的用法：  
  
-   行動銷售部門的應用程式通常會有資料表這類 **SalesOrderHeader**, ，**SalesOrderDetail** 和 **產品**。 在「訂閱者」端輸入訂單 (通常將資料提供給訂單實行系統)，然後再將其複寫至「發行者」。 許多行動工作者使用含有限儲存的手持式裝置：訂單在「發行者」端接收後，可以在「訂閱者」端刪除。 刪除不會傳播到「發行者」，因為此訂單在系統中仍為使用中訂單。  
  
     在此案例中，刪除不會追蹤的 **SalesOrderHeader** 和 **SalesOrderDetail** 資料表。 會為追蹤刪除 **產品** 資料表，因為在發行者端刪除產品後，如果刪除應被傳送到 「 訂閱者 」 來保持最新的產品清單。  
  
-   應用程式可以歷程記錄資料儲存在資料表這類 **TransactionHistory**, ，它會定期清除的記錄超過一年。 資料表可以使用篩選，以便「訂閱者」僅接收當月的交易資料。 儘管「發行者」端每月進行的批次刪除 (即清除舊資料) 與「訂閱者」無關，但依預設它們仍會被追蹤及列舉。  
  
     在此狀況下，可以在批次處理前停止系統中的作業，並讓應用程式停用對刪除的追蹤。 處理完成後，追蹤可再次啟用。  
  
> [!IMPORTANT]  
>  如果其他作業在「發行者」端繼續，您必須確定在停用刪除追蹤時，不會發生應傳播給「訂閱者」的刪除。  
  
 **若要指定刪除不被追蹤**  
  
-   複寫 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 程式設計︰ [指定，會刪除應該不會追蹤針對合併發行項 & #40。複寫 TRANSACT-SQL 程式設計 & #41;](../../../relational-databases/replication/publish/specify that deletes should not be tracked for merge articles.md)  
  
## 另請參閱  
 [合併式複寫的發行項選項](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [使用僅限下載的發行項最佳化合併式複寫效能](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)  
  
  
---
title: "加入或編輯聯結 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.addeditjoin.f1"
ms.assetid: 3b546560-720f-48b8-9d63-cf159290e9d4
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# 加入或編輯聯結
  **[加入聯結]** 和 **[編輯聯結]** 對話方塊可讓您為合併發行集加入和編輯聯結篩選。  
  
> [!NOTE]  
>  編輯現有發行集內的篩選需要該發行集的新快照集。 如果發行集有訂閱，就必須重新初始化訂閱。 如需屬性變更的詳細資訊，請參閱 [變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
 聯結篩選可讓您根據發行集內相關資料表的篩選方式來篩選資料表。 通常，父資料表會使用參數化資料列篩選器進行篩選，然後一個或多個聯結篩選會以您在資料表之間定義聯結的相同方式進行定義。 聯結篩選會擴充資料列篩選，以便只有當資料與聯結篩選子句相符時，才複寫相關資料表中的資料。  
  
 聯結篩選通常會遵循為套用到之資料表所定義的主索引鍵/外部索引鍵關聯性，但並非嚴格受限於主索引鍵/外部索引鍵關聯性。 聯結篩選可以根據任何比較兩個發行項資料表中之相關資料的邏輯。  
  
> [!IMPORTANT]  
>  聯結篩選可以包含無限數量的資料表，但如果篩選的資料表數量過多，會影響合併處理過程中的效能。 若您正在產生五個以上資料表的聯結篩選，請考慮其他方案：不要篩選小型、無法變更或主要為查詢資料表的資料表。 聯結篩選只能用於必須在訂閱者中分割的資料表之間。  
  
## 選項  
 這個對話方塊包括三個步驟的處理程序，以在兩個資料表之間建立一個聯結篩選。 若要建立一個以上的聯結篩選，就必須執行此對話方塊一次以上。  
  
1.  **確認已篩選的資料表並選取聯結的資料表**  
  
    -   如果您要加入新聯結，請確認資料表中的 **篩選表格** 文字方塊是否正確 (如果不正確，請按一下 [ **取消**, ，選取正確的資料表上 **篩選資料表資料列** 頁面，然後按一下 **加入聯結** 回到此對話方塊)。 然後選取 [從資料表 **聯結的資料表** 下拉式清單方塊。  
  
    -   如果是編輯現有的聯結，則資料表名稱已經指定且無法變更。 若要變更涉及聯結的資料表，必須在 **[篩選資料表的資料列]** 頁面上刪除現有的聯結篩選，然後在不同的資料表之間建立新聯結。  
  
2.  **建立聯結陳述式**  
  
    -   如果是加入新聯結，請選取 **[使用產生器建立陳述式]** 或 **[手動寫入聯結陳述式]**。 如果您一開始是以手動寫入聯結，就無法使用產生器。  
  
         如果您選取使用產生器，使用的資料行在方格中 (**搭配**, ，**篩選資料表資料行**, ，**運算子**, ，和 **聯結資料表資料行**) 來建立聯結陳述式。 在方格中的每個資料行包含一個下拉式清單方塊，可讓您選取兩個資料行和一個運算子 (**=**, ，**<>**, ，**<=**, ，**\<**, ，**>=**, ，**>**, ，**像**)。 結果會在 **[預覽]** 文字區域中顯示。 如果聯結涉及一對以上的資料行，選取一個結合 (**AND** 或 **OR**) 從 **搭配** 資料行，然後輸入兩個多個資料行和另一個運算子。  
  
         如果選取手動寫入陳述式，請在 **[聯結陳述式]** 文字區域寫入聯結陳述式。 使用 **[已篩選的資料表資料行]** 清單方塊和 **[聯結的資料表資料行]** 清單方塊，將資料行拖放到 **[聯結陳述式]** 文字區域。  
  
    -   如果是編輯現有的聯結，您必須以手動進行編輯。  
  
3.  **指定聯結選項**  
  
    -   如果在已篩選的資料表中聯結的資料行是唯一的，請選取 **[唯一索引鍵]**。 如果資料行是唯一的，合併處理可以使用特殊效能最佳化。  
  
        > [!CAUTION]  
        >  選取此選項表示聯結篩選中的子資料表與父資料表之間的關聯性是一對一或一對多。 如果在父資料表中的聯結資料行有保證唯一性的條件約束，請僅選取此選項。 如果選項設定不正確，則資料可能發生非聚合的情況。  
  
    -   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 依預設，合併式複寫在同步處理過程中會按逐個資料列的方式處理變更。 若要將相關的變更作為一個單位來處理，請選取 **[邏輯記錄]**。 只有當發行項與發行集之使用邏輯記錄的需求均符合時，才可以使用此選項。 如需詳細資訊，請參閱 「 使用邏輯記錄的考量 」 一節中 [使用邏輯記錄的相關資料列群組變更](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
 您加入或編輯篩選之後，請按一下 **[確定]** 以儲存變更並關閉對話方塊。 您指定的篩選會被剖析，並會針對 SELECT 子句中的資料表執行。 如果篩選陳述式包含語法錯誤或其他問題，則系統會通知您，然後您可以編輯該篩選陳述式。  
  
## 另請參閱  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [檢視及修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [篩選發行的資料](../../relational-databases/replication/publish/filter-published-data.md)   
 [聯結篩選](../../relational-databases/replication/merge/join-filters.md)   
 [參數化資料列篩選器](../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
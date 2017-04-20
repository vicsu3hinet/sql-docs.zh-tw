---
title: "進階合併式複寫衝突偵測與解決 | Microsoft Docs"
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
  - "合併式複寫衝突解決 [SQL Server 複寫], 關於衝突解決"
  - "預設 Conflict Resolver"
  - "資料行層級衝突追蹤"
  - "資料列層級衝突追蹤"
  - "檢視合併式複寫衝突"
  - "解決合併式複寫衝突"
  - "邏輯記錄層級衝突追蹤 [SQL Server 複寫]"
  - "衝突解決 [SQL Server 複寫], 合併式複寫"
ms.assetid: 063d3d9c-ccb5-4fab-9d0c-c675997428b4
caps.latest.revision: 46
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 46
---
# 進階合併式複寫衝突偵測與解決
  發行者與訂閱者連接並進行同步處理時，合併代理程式會偵測是否有任何衝突。 如果偵測到衝突，「合併代理程式」會使用衝突解析程式 (在發行項加入發行集時指定)，決定要接受及傳播至其他站台的資料。  
  
> [!NOTE]  
>  雖然「訂閱者」會與「發行者」同步，但是衝突通常是在不同「訂閱者」端進行更新之間發生，而不是在「訂閱者」端和「發行者」端進行更新時發生。  
  
 衝突偵測與解決的行為取決於下列選項，這些選項會在本主題中說明：  
  
-   您是否指定資料行層級追蹤、資料列層級追蹤或邏輯記錄層級追蹤。  
  
-   您是否指定預設的優先權式解決機制或指定發行項解析程式。 發行項解析程式可以是：  
  
    -   以 Managed 程式碼撰寫的 *商務邏輯處理常式* 。  
  
    -   以 COM 為基礎 *自訂解析程式*。  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 提供之以 COM 為基礎的解析程式。  
  
     如果使用預設解析機制，則會依據所用的訂閱類型進一步決定行為：用戶端或伺服器。  
  
## 衝突偵測  
 資料變更是否算是衝突取決於您為發行項所設定的衝突追蹤類型：  
  
-   當您選取資料行層級衝突追蹤時，如果在一個以上的複寫節點對相同資料列中的相同資料行進行變更，則該變更會被視為衝突。  
  
-   當您選取資料列層級追蹤時，如果在一個以上的複寫節點對相同資料列中的任何資料行進行變更，則該變更會被視為衝突 (對應資料列中受影響的資料行不需要相同)。  
  
-   當您選取邏輯記錄層級追蹤時，如果在一個以上的複寫節點對相同邏輯記錄中的任何資料列進行變更，則該變更會被視為衝突 (對應資料列中受影響的資料行不需要相同)。  
  
 如需詳細資訊，請參閱 [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/detecting-and-resolving-conflicts-in-logical-records.md)。  
  
 若要指定發行項的衝突追蹤與解決層級，請參閱＜ [Specify the Conflict Tracking and Resolution Level for Merge Articles](../../../relational-databases/replication/publish/specify-the-conflict-tracking-and-resolution-level-for-merge-articles.md)＞。  
  
## 衝突解決  
 在偵測到衝突後，「合併代理程式」會啟動選取的衝突解析程式，並使用該解析程式決定衝突成功者。 成功的資料列已套用至「發行者」與「訂閱者」，而失敗的資料列則已寫入衝突資料表。 衝突會在解析程式執行後立即解決，除非您選擇以互動方式解決衝突。  
  
### 解析程式類型  
 在合併式複寫中，衝突解決會在發行項層級發生。 對於由許多發行項所組成的發行集來說，您可以使用各種不同的衝突解析程式來處理不同的發行項，也可以使用相同的解析程式來解決一個發行項、數個發行項，或者組成發行集的所有發行項。  
  
 如果您計劃使用預設的優先權式衝突解析程式，就無需設定發行項的解析程式屬性。 如果您要使用發行項解析程式而非預設的解析程式，則必須在「發行者」上選取可用的解析程式，以設定要使用此解析程式的發行項之解析程式屬性。 需要傳遞至解析程式的任何特定資訊，也可以在解析程式資訊屬性中指定。  
  
 合併式複寫提供四種類型的衝突解析程式：  
  
-   預設的優先權式衝突解析程式  
  
     根據訂閱是客訂閱或主訂閱而定，預設解決機制的行為會有所差異。 您可指派優先權值給使用主訂閱的個別「訂閱者」；對具有最高優先權的節點所做的變更會在任何衝突中優先。 對於客訂閱，第一個寫入「發行者」的變更會在衝突中優先。  
  
     建立訂閱之後，就不能變更訂閱的類型。  
  
-   商務邏輯處理常式  
  
     商務邏輯處理常式架構允許您撰寫在合併同步處理過程中呼叫的 Managed 程式碼組件。 該組件包含商務邏輯，可在同步處理期間回應衝突及一些其他條件。 如需詳細資訊，請參閱 [執行商務邏輯合併同步處理期間](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)。  
  
-   以 COM 為基礎的自訂解析程式  
  
     合併式複寫提供一個 API，用於以 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vcprvc](../../../includes/vcprvc-md.md)] 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]等語言將解析程式撰寫為 COM 物件。 如需詳細資訊，請參閱 [以 COM 為基礎的自訂解析程式](../../../relational-databases/replication/merge/com-based-custom-resolvers.md)。  
  
-   所提供的 COM 型解析程式 [!INCLUDE[msCoName](../../../includes/msconame-md.md)]  
  
     [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 包含多個以 COM 為基礎的解析程式。 如需詳細資訊，請參閱 [Microsoft 以 COM 為基礎的解析程式](../../../relational-databases/replication/merge/microsoft-com-based-resolvers.md)。  
  
 如需如何選取適當的型別解析程式的資訊，請參閱 [選擇解決器](../../../relational-databases/replication/merge/choose-a-resolver.md)。  
  
> [!NOTE]  
>  某些發行項解析程式的撰寫僅供處理特定作業的衝突。 例如，某個解析程式可以處理更新，但無法處理插入或刪除。 預設的優先權式衝突解析程式會處理沒有由發行項解析程式所處理的任何衝突。  
  
 若要指定合併訂閱類型與衝突解決優先權，請參閱  
  
-   [!包含 [ssManStudioFull] (.../ Token/ssManStudioFull_md.md)]: [Specify a Merge Subscription Type and Conflict Resolution Priority &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify a merge subscription type and conflict resolution priority.md)  
  
-   複寫 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 程式設計與 Replication Management Objects (RMO) 程式設計︰ [建立提取訂閱](../../../relational-databases/replication/create-a-pull-subscription.md) 和 [建立發送訂閱](../../../relational-databases/replication/create-a-push-subscription.md)  
  
### 互動解析程式  
 複寫提供「互動解析程式」使用者介面，可與預設的優先權式衝突解析程式或發行項解析程式一起使用。 透過 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Synchronization Manager 執行視需要的同步處理時，「互動解析程式」會在執行階段顯示衝突資料，並讓您選擇如何解決衝突。 如需有關如何啟用互動式解決及啟動「互動解析程式」的詳細資訊，請參閱＜ [Interactive Conflict Resolution](../../../relational-databases/replication/merge/interactive-conflict-resolution.md)＞。  
  
## 檢視衝突  
 檢視衝突最直接的方法是使用「複寫衝突檢視器」，該檢視器可從 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 取得 ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 也提供允許查詢衝突資料表的預存程序)。 「衝突檢視器」和「互動解析程式」是類似的工具，不過「互動解析程式」可讓您在同步處理發生時解決衝突，而「衝突解析程式」是設計用來在已解決衝突後檢視衝突。 如果系統資料表中仍有可用的衝突中繼資料 (衝突中繼資料依預設會保留 14 天)，您可以在「衝突檢視器」中覆寫衝突解決結果，不過如果經常需要直接介入，請考慮使用「互動解析程式」。  
  
> [!NOTE]  
>  「衝突檢視器」中不會顯示涉及邏輯記錄的衝突。 若要檢視這些衝突的相關資訊，請使用複寫預存程序。 如需詳細資訊，請參閱 [檢視衝突資訊適用於合併式發行集和 #40。複寫 TRANSACT-SQL 程式設計 & #41;](../../../relational-databases/replication/view conflict information for merge publications.md)。  
  
 「衝突檢視器」會顯示下列三個系統資料表中的資訊：  
  
-   複寫衝突資料表的每個資料表建立合併發行項，在表單中的名稱與 **MSmerge_conflict_ \< p u b l>_ \< e>**。  
  
     衝突資料表的結構與其所根據的資料表相同。 其中一個資料表內的資料列含有衝突資料列的失敗版本 (資料列的優先版本位在實際的使用者資料表中)。  
  
-    **MSmerge_conflicts_info** 表提供每個衝突，包括衝突類型的資訊。  
  
-   **sysmergearticles** 資料表可識別哪些使用者資料表具有衝突資料表，並提供衝突資料表的相關資訊。  
  
 依預設，會儲存衝突資訊：  
  
-   如果發行集相容性層級為 90RTM 或更高，則是在「發行者」與「訂閱者」端。  
  
-   如果發行集相容性層級低於 80RTM，則是在發行者端。  
  
-   如果「訂閱者」執行 [!INCLUDE[ssEW](../../../includes/ssew-md.md)]，則會儲存在「發行者」端。 衝突資料無法儲存在 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 訂閱者上。  
  
 **若要檢視衝突**  
  
-   [!包含 [ssManStudioFull] (.../ Token/ssManStudioFull_md.md)]: [View and Resolve Data Conflicts for Merge Publications &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/view and resolve data conflicts for merge publications.md)  
  
-   複寫 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 程式設計︰ [檢視合併式發行集與 #40; 的衝突資訊複寫 TRANSACT-SQL 程式設計 & #41;](../../../relational-databases/replication/view conflict information for merge publications.md)  
  
## 另請參閱  
 [同步處理資料](../../../relational-databases/replication/synchronize-data.md)  
  
  
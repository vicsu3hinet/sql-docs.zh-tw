---
title: "篩選追蹤中的伺服器處理序識別碼 (SPID) (SQL Server Profiler) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "篩選 [SQL Server], 追蹤"
  - "篩選 [SQL Server], SPID"
  - "追蹤 [SQL Server], 篩選"
ms.assetid: f5945c39-be6b-4632-91cb-92066c80e188
caps.latest.revision: 25
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 25
---
# 篩選追蹤中的伺服器處理序識別碼 (SPID) (SQL Server Profiler)
  此主題描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，篩選追蹤中的伺服器處理序識別碼 (SPID)。  
  
### 若要篩選追蹤系統識別碼  
  
1.  在 **[檔案]** 功能表上按一下 **[新增追蹤]**，然後連接到 SQL Server 的執行個體。  
  
     會出現 [追蹤屬性] **[追蹤屬性]**對話方塊。  
  
    > [!NOTE]  
    >  如果選取 [進行連接後立即啟動追蹤]，將不會顯示 [追蹤屬性] 對話方塊，而是開始追蹤。 在 [工具] 功能表，按一下 [選項]，並清除 [進行連接後立即啟動追蹤] 核取方塊，以關閉這項設定。  
  
2.  在 **[追蹤名稱]** 方塊中，輸入追蹤的名稱。  
  
3.  在 [使用範本] 名稱清單中，選取追蹤範本。  
  
4.  選擇性，指定要儲存追蹤結果的目的地檔案或資料表。  
  
5.  在 [事件選取範圍] 索引標籤上，按一下 [SPID] 資料行標題，以啟動 [編輯篩選] 對話方塊。 您也可以用滑鼠右鍵按一下資料行標題，然後選擇 [編輯資料行篩選]。 如果 [SPID] 資料行未出現，請核取 [顯示所有資料行] 方塊。  
  
6.  在 [編輯篩選] 對話方塊中，展開適當的比較運算子，然後輸入 SPID 作為比較的值。  
  
## 另請參閱  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
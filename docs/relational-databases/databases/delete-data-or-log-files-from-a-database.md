---
title: "刪除資料庫的資料或記錄檔 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "記錄 [SQL Server], 檔案"
  - "刪除檔案"
  - "移除檔案"
  - "移除資料"
  - "資料刪除 [SQL Server]"
  - "刪除檔案 [SQL Server]"
  - "刪除資料"
ms.assetid: 0db4018c-ce2c-4ba1-bb29-1e4f3791c925
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# 刪除資料庫的資料或記錄檔
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來刪除 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的資料或記錄檔。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [必要條件](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **使用下列方法刪除資料庫的資料或記錄檔：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
  
-   在刪除檔案之前，檔案必須空白。 如需詳細資訊，請參閱[壓縮檔案](../../relational-databases/databases/shrink-a-file.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要資料庫的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 若要刪除資料庫的資料或記錄檔  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開 [資料庫]，以滑鼠右鍵按一下要從中刪除檔案的資料庫，然後按一下 [屬性]。  
  
3.  選取 **[檔案]** 頁面。  
  
4.  在 **[資料庫檔案]** 方格中，選取要刪除的檔案，再按一下 **[移除]**。  
  
5.  按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 若要刪除資料庫的資料或記錄檔  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 這個範例會移除 `test1dat4` 檔案。  
  
 [!code-sql[DatabaseDDL#AlterDatabase4](../../relational-databases/databases/codesnippet/tsql/delete-data-or-log-files_1.sql)]  
  
 如需其他範例，請參閱 [ALTER DATABASE 檔案及檔案群組選項 &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20File%20and%20Filegroup%20Options%20\(Transact-SQL\).md)。  
  
## 另請參閱  
 [壓縮資料庫](../../relational-databases/databases/shrink-a-database.md)   
 [將資料或記錄檔加入資料庫](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)  
  
  
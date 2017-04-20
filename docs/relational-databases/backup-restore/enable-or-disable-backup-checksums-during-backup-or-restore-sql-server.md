---
title: "在備份或還原期間啟用或停用備份總和檢查碼 (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "備份總和檢查碼 [SQL Server]"
  - "停用總和檢查碼"
  - "總和檢查碼 [SQL Server]"
ms.assetid: 6786bd1e-ad97-430a-8dfb-d4ba952d6c4d
caps.latest.revision: 31
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 31
---
# 在備份或還原期間啟用或停用備份總和檢查碼 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中備份或還原資料庫時啟用或停用備份總和檢查碼。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目啟用或停用備份總和檢查碼：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 BACKUP  
 BACKUP DATABASE 和 BACKUP LOG 權限預設為**系統管理員**固定伺服器角色以及 **db_owner** 和 **db_backupoperator** 固定資料庫角色的成員。  
  
 備份裝置實體檔案的擁有權和權限問題可能會干擾備份作業。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須能夠讀取和寫入裝置；執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的帳戶必須具備寫入權限。 不過，在系統資料表中加入備份裝置項目的 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md) 並不會檢查檔案存取權限。 當您嘗試備份或還原時，存取實體資源之前不一定會出現備份裝置實體檔案的這些問題。  
  
 RESTORE  
 如果還原的資料庫不存在，使用者必須有 CREATE DATABASE 權限，才能執行 RESTORE。 如果資料庫存在 (若是 FROM DATABASE_SNAPSHOT 選項，資料庫一律存在)，預設會將 RESTORE 權限授與**系統管理員**和 **dbcreator** 固定伺服器角色的成員，以及資料庫的擁有者 (**dbo**)。  
  
 RESTORE 權限提供給伺服器隨時可以取得其成員資格資訊的角色。 由於資料庫必須是可存取且未損毀，才能夠檢查固定資料庫角色成員資格，但執行 RESTORE 時未必如此，因此，**db_owner** 固定資料庫角色的成員並沒有 RESTORE 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 若要在備份作業期間啟用或停用總和檢查碼  
  
1.  請依照＜ [建立資料庫備份](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)＞的步驟執行。  
  
2.  在 **[選項]** 頁面的 **[可靠性]** 區段中，按一下 **[寫入媒體之前執行總和檢查碼]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 若要為備份作業啟用或停用備份總和檢查碼  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  若要在 [BACKUP](../../t-sql/statements/backup-transact-sql.md) 陳述式中啟用備份總和檢查碼，請指定 WITH CHECKSUM 選項。 若要停用備份總和檢查碼，請指定 WITH NO_CHECKSUM 選項。 這是預設行為，但是壓縮備份除外。 下列範例指定應執行總和檢查碼。  
  
```tsql  
BACKUP DATABASE AdventureWorks2012   
 TO DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'  
   WITH CHECKSUM;  
GO  
```  
  
#### 若要為還原作業啟用或停用備份總和檢查碼  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  若要在 [RESTORE](../Topic/RESTORE%20\(Transact-SQL\).md) 陳述式中啟用備份總和檢查碼，請指定 WITH CHECKSUM 選項。 這是壓縮備份的預設行為。 若要停用備份總和檢查碼，請指定 WITH NO_CHECKSUM 選項。 這是預設行為，但是壓縮備份除外。 下列範例指定應執行備份總和檢查碼。  
  
```tsql  
RESTORE DATABASE AdventureWorks2012   
 FROM DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'  
   WITH CHECKSUM;  
GO  
```  
  
> [!WARNING]  
>  如果您明確地在還原作業中要求 CHECKSUM，而且備份包含備份總和檢查碼，就會和預設情況一樣，備份總和檢查碼及分頁總和檢查碼都會加以驗證。 然而，如果備份組沒有備份總和檢查碼，則還原作業就會失敗，並且會產生訊息指出總和檢查碼不存在。  
  
## 另請參閱  
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../Topic/RESTORE%20FILELISTONLY%20\(Transact-SQL\).md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../Topic/RESTORE%20HEADERONLY%20\(Transact-SQL\).md)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](../Topic/RESTORE%20LABELONLY%20\(Transact-SQL\).md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../Topic/RESTORE%20VERIFYONLY%20\(Transact-SQL\).md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [RESTORE 引數 &#40;Transact-SQL&#41;](../Topic/RESTORE%20Arguments%20\(Transact-SQL\).md)   
 [備份和還原期間可能發生的媒體錯誤 &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)   
 [指定在發生錯誤後備份或還原作業應該繼續還是停止 &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify if backup or restore continues or stops after error.md)  
  
  
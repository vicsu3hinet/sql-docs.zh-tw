---
title: "設定 user connections 伺服器組態選項 | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "同時連接 [SQL Server]"
  - "使用者連接選項 [SQL Server]"
  - "使用者 [SQL Server], 同時連接"
  - "同時連接的使用者數目上限"
  - "連接 [SQL Server], 同時"
ms.assetid: 53beee6e-59fe-4276-9abb-8f1cec2a3508
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# 設定 user connections 伺服器組態選項
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  此主題描述如何使用 **或** ，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中設定 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] user connections [!INCLUDE[tsql](../../includes/tsql-md.md)]伺服器組態選項。 **user connections** 選項會指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上可同時連接的使用者數目上限。 實際允許的使用者連接數也取決於您所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本，以及應用程式的限制或應用程式和硬體的限制而定。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 最多允許 32,767 個使用者連接。 因為 [使用者連接] 是動態的 (自我設定) 選項，所以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會視需要自動調整使用者連接數上限，最多可調整到允許的最大值。 例如，如果只有 10 個使用者登入，就配置 10 個使用者連線物件。 在大部分情況下，不需要變更這個選項的值。 預設值為 0，表示允許最大量 (32,767) 的使用者連接數。  
  
 若要判斷系統允許的最大使用者連接數目，您可以執行 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 或查詢 [sys.configuration](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 目錄檢視。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **使用下列方法設定 user connections 選項：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **待處理**  [設定 user connections 選項之後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Recommendations"></a> 建議  
  
-   這個選項是進階選項，只有有經驗的資料庫管理員或通過認證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術人員才可變更。  
  
-   使用 **user connections** 選項有助於避免因並行連接過多，而導致伺服器超過負載。 您可以根據系統與使用者需求估計連接數。 例如，在有許多使用者的系統上，通常不會每個使用者各要求一個唯一的連接。 連接可以由使用者共用。 執行 OLE DB 應用程式的使用者，對每個開啟的連接物件都必須各有一個連接；執行開放式資料庫連接 (ODBC) 應用程式的使用者，對應用程式中的每個使用中連接控制代碼都必須各有一個連接；而執行 DB-Library 應用程式的使用者，則對呼叫 DB-Library **dbopen** 函數的每個啟動處理序都必須各有一個連接。  
  
    > [!IMPORTANT]  
    >  如果必須使用這個選項，請不要將這個值設得太大，因為每個連接不論使用與否，都會造成額外負擔。 如果超過最大使用者連接數，就會收到錯誤訊息，然後要等到可以使用另一個連接後，才能再繼續進行連接。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 依預設，所有使用者都會取得不含參數或只含第一個參數之 **sp_configure** 的執行權限。 若要執行同時設定了兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 設定 user connections 選項  
  
1.  在物件總管中，以滑鼠右鍵按一下伺服器，然後按一下 [屬性]。  
  
2.  按一下 **[連接]** 節點。  
  
3.  在 **[連接]**下的 **[並行連接的最大數目]** 方塊中，輸入或選取 0 至 32767 之間的值，以設定可同時連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的最大使用者數目。  
  
4.  重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 設定 user connections 選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 此範例示範如何使用 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 以將 `user connections` 選項的值設定為 `325` 位使用者。  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'user connections', 325 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 如需詳細資訊，請參閱[伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)。  
  
##  <a name="FollowUp"></a> 待處理：設定 user connections 選項之後  
 伺服器必須重新啟動之後，設定才能生效。  
  
## 另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [伺服器設定選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
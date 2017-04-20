---
title: "伺服器層級角色 | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.Security.NT_AUTHORITY.SYSTEM"
  - "sql13.Security.BUILTIN.administrators"
helpviewer_keywords: 
  - "角色 [SQL Server], 伺服器層級"
  - "主體 [SQL Server], 伺服器層級"
  - "CONTROL SERVER 權限"
  - "固定伺服器角色 [SQL Server]"
  - "認證 [SQL Server], 角色"
  - "sysadmin 固定伺服器角色"
  - "伺服器層級角色 [SQL Server]"
  - "驗證 [SQL Server], 角色"
ms.assetid: 7adf2ad7-015d-4cbe-9e29-abaefd779008
caps.latest.revision: 52
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 50
---
# 伺服器層級角色
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會提供伺服器層級角色來協助您管理伺服器的權限。 這些角色是將其他主體組成群組的安全性主體。 伺服器層級角色的權限範圍為整個伺服器  (「角色」就像是 Windows 作業系統中的「群組」)。  
  
 固定伺服器角色是為了方便和回溯相容性所提供。 請盡可能指派更特定的權限。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供了九種固定伺服器角色。 您無法變更授與固定伺服器角色的權限。 從 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 開始，您就可以建立使用者定義伺服器角色，並將伺服器層級權限加入至使用者定義伺服器角色。  
  
 您可以將伺服器層級主體 ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入、Windows 帳戶和 Windows 群組) 加入伺服器層級角色。 固定伺服器角色的每個成員可以對相同的角色增加其他登入。 使用者定義伺服器角色的成員無法將其他伺服器主體加入至此角色。  
  
## 固定伺服器層級角色  
 下表顯示固定伺服器層級角色及其功能。  
  
|固定伺服器層級角色|描述|  
|------------------------------|-----------------|  
|sysadmin|系統管理員 (sysadmin) 固定伺服器角色的成員可以執行伺服器中的所有活動。|  
|serveradmin|伺服器管理員 (serveradmin) 固定伺服器角色的成員可以變更整個伺服器的組態選項及關閉伺服器。|  
|securityadmin|安全性管理員 (securityadmin) 固定伺服器角色的成員可以管理登入及其屬性。 他們可以 GRANT、DENY 及 REVOKE 伺服器層級權限。 如果他們擁有資料庫的存取權，也可以 GRANT、DENY 和 REVOKE 資料庫層級權限。 此外，他們可以重設 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入的密碼。<br /><br /> **\*\* 安全性注意事項 \*\*** 安全性管理員可使用授與 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 存取權和設定使用者權限的功能，來指派大部分的伺服器權限。 您應該將 **securityadmin** 角色視為相當於**系統管理員**角色。|  
|processadmin|處理序管理員 (processadmin) 固定伺服器角色的成員可以結束在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體中執行的處理序。|  
|setupadmin|setupadmin 固定伺服器角色的成員可以使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式加入和移除連結的伺服器 (使用 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 時需要系統管理員成員資格)。|  
|bulkadmin|大量管理員 (bulkadmin) 固定伺服器角色的成員可以執行 BULK INSERT 陳述式。|  
|diskadmin|diskadmin 固定伺服器角色是用來管理磁碟檔案。|  
|dbcreator|資料庫建立者 (dbcreator) 固定伺服器角色的成員可以建立、改變、卸除及還原任何資料庫。|  
|public|每一個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入都屬於 public 伺服器角色。 當伺服器主體未被授與或拒絕安全性實體物件的特定權限時，該使用者會繼承授與給該物件之 public 的權限。 只有當您想要將任何物件提供給所有使用者使用時，才指派該物件的 public 權限。 您無法變更 public 的成員資格。<br /><br /> 注意：public 的實作方式與其他角色不同。 不過，您可以在 public 中授與、拒絕或撤銷權限。|  
  
## 固定伺服器角色的權限  
 每個固定伺服器角色都擁有指派給它的特定權限。 如需指派給伺服器角色之權限的圖表，請參閱 [Database Engine Fixed Server and Fixed Database Roles](http://social.technet.microsoft.com/wiki/contents/articles/2024.database-engine-fixed-server-and-fixed-database-roles.aspx) (資料庫引擎固定伺服器與固定資料庫角色)。  
  
> [!IMPORTANT]  
>  **CONTROL SERVER** 權限與**系統管理員**固定伺服器角色類似但不完全相同。 權限不代表角色成員資格，角色成員資格也不會授與權限。 (例如， **CONTROL SERVER** 不代表**系統管理員**固定伺服器角色的成員資格)。不過，角色與相等權限之間有時候可以互相模擬。 大部分 **DBCC** 命令與許多系統程序都需要**系統管理員**固定伺服器角色的成員資格。 如需需要**系統管理員**成員資格的 171 個系統預存程序清單，請參閱 Andreas Wolter 的下列部落格文章：[CONTROL SERVER vs. sysadmin/sa: permissions, system procedures, DBCC, automatic schema creation and privilege escalation - caveats](http://www.insidesql.org/blogs/andreaswolter/2013/08/control-server-vs-sysadmin-sa-permissions-privilege-escalation-caveats)。  
  
## 伺服器層級權限  
 只有伺服器層級權限可加入至使用者定義伺服器角色。 若要列出伺服器層級權限，請執行以下陳述式。 伺服器層級權限為：  
  
```tsql  
SELECT * FROM sys.fn_builtin_permissions('SERVER') ORDER BY permission_name;  
```  
  
 如需權限的詳細資訊，請參閱[權限 &#40;Database Engine&#41;](../../../relational-databases/security/permissions-database-engine.md) 和 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)。  
  
## 處理伺服器層級角色  
 下表將說明可用來處理伺服器層級角色的命令、檢視和函數。  
  
|功能|型別|描述|  
|-------------|----------|-----------------|  
|[sp_helpsrvrole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpsrvrole-transact-sql.md)|中繼資料|傳回伺服器層級角色的清單。|  
|[sp_helpsrvrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)|中繼資料|傳回伺服器層級角色成員的相關資訊。|  
|[sp_srvrolepermission &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql.md)|中繼資料|顯示伺服器層級角色的權限。|  
|[IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../../t-sql/functions/is-srvrolemember-transact-sql.md)|中繼資料|指出 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入是否為指定之伺服器層級角色的成員。|  
|[sys.server_role_members &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)|中繼資料|針對每個伺服器層級角色的每個成員，各傳回一個資料列。|  
|[sp_addsrvrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)|Command|加入一個登入，做為伺服器層級角色的成員。 已被取代。 請改用 [ALTER SERVER ROLE](../../../t-sql/statements/alter-server-role-transact-sql.md)。|  
|[sp_dropsrvrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)|Command|從伺服器層級角色移除 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入或是 Windows 使用者或群組。 已被取代。 請改用 [ALTER SERVER ROLE](../../../t-sql/statements/alter-server-role-transact-sql.md)。|  
|[CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-role-transact-sql.md)|Command|建立使用者定義伺服器角色。|  
|[ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-role-transact-sql.md)|Command|變更伺服器角色的成員資格或變更使用者定義伺服器角色的名稱。|  
|[DROP SERVER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-server-role-transact-sql.md)|Command|移除使用者定義伺服器角色。|  
|[IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../../t-sql/functions/is-srvrolemember-transact-sql.md)|函數|判斷伺服器角色的成員資格。|  
  
## 另請參閱  
 [資料庫層級角色](../../../relational-databases/security/authentication-access/database-level-roles.md)   
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [安全性函數 &#40;Transact-SQL&#41;](../../../t-sql/functions/security-functions-transact-sql.md)   
 [保護 SQL Server 的安全](../../../relational-databases/security/securing-sql-server.md)   
 [GRANT 伺服器主體權限 &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)   
 [REVOKE 伺服器主體權限 &#40;Transact-SQL&#41;](../../../t-sql/statements/revoke-server-principal-permissions-transact-sql.md)   
 [DENY 伺服器主體權限 &#40;Transact-SQL&#41;](../../../t-sql/statements/deny-server-principal-permissions-transact-sql.md)   
 [建立伺服器角色](../../../relational-databases/security/authentication-access/create-a-server-role.md)  
  
  
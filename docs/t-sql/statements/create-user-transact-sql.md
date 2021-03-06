---
title: "建立使用者 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/28/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WITHOUT_LOGIN_TSQL
- CREATE_USER_TSQL
- SQL13.SWB.DATABASEUSER.OWNEDSCHEMAS.F1
- WITHOUT LOGIN
- CREATE USER
- ALLOW_ENCRYPTED_VALUE_MODIFICATIONS
- ALLOW_ENCRYPTED_VALUE_MODIFICATIONS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- adding users
- WITHOUT LOGIN [SQL Server]
- CREATE USER statement
- database user additions [SQL Server]
- USER WITHOUT LOGIN [SQL Server]
- users [SQL Server], adding
- users [SQL Server]
ms.assetid: 01de7476-4b25-4d58-85b7-1118fe64aa80
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: cc1b66f561ce413016e154bc329384566a8384b8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="create-user-transact-sql"></a>CREATE USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  將使用者加入目前資料庫中。 以下列出 11 種使用者類型使用的最基本的語法範例：  
  
**依據 master 登入的使用者**這是最常見的使用者類型。  
  
-   根據基礎 Windows Active Directory 帳戶的登入的使用者。 `CREATE USER [Contoso\Fritz];`     
-   依據 Windows 群組登入的使用者。 `CREATE USER [Contoso\Sales];`   
-   依據使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證登入的使用者。 `CREATE USER Mary;`  
  
**在資料庫進行驗證的使用者**建議來協助進行更容易移植您的資料庫。  
 一律允許在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。 在自主資料庫中只允許[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。  
  
-   依據沒有登入之 Windows 使用者的使用者。 `CREATE USER [Contoso\Fritz];`    
-   依據沒有登入之 Windows 群組的使用者。 `CREATE USER [Contoso\Sales];`  
-   在使用者[!INCLUDE[ssSDS](../../includes/sssds-md.md)]或[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]根據 Azure Active Directory 的使用者。 `CREATE USER [Contoso\Fritz] FROM EXTERNAL PROVIDER;`     

-   具有密碼之自主資料庫使用者。 (不適用於[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]。)`CREATE USER Mary WITH PASSWORD = '********';`   
  
**依據 Windows 主體的使用者，透過 Windows 群組登入**  
  
-   依據沒有登入之 Windows 使用者，但可透過 Windows 群組成員資格連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的使用者。 `CREATE USER [Contoso\Fritz];`  
  
-   依據沒有登入之 Windows 群組，但可透過不同的 Windows 群組成員資格連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的使用者。 `CREATE USER [Contoso\Fritz];`  
  
**無法驗證的使用者**這些使用者無法登入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
-   沒有登入的使用者。 無法登入但可獲得權限。 `CREATE USER CustomApp WITHOUT LOGIN;`    
-   依據憑證的使用者。 無法登入，但可獲得權限而且可簽署模組。 `CREATE USER TestProcess FOR CERTIFICATE CarnationProduction50;`  
-   依據非對稱金鑰的使用者。 無法登入，但可獲得權限而且可簽署模組。 `CREATE User TestProcess FROM ASYMMETRIC KEY PacificSales09;`   
 
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Syntax Users based on logins in master  
CREATE USER user_name   
    [   
        { FOR | FROM } LOGIN login_name   
    ]  
    [ WITH <limited_options_list> [ ,... ] ]   
[ ; ]  
  
--Users that authenticate at the database  
CREATE USER   
    {  
      windows_principal [ WITH <options_list> [ ,... ] ]  
  
    | user_name WITH PASSWORD = 'password' [ , <options_list> [ ,... ]   
    | Azure_Active_Directory_principal FROM EXTERNAL PROVIDER   
    }  
  
 [ ; ]  
  
--Users based on Windows principals that connect through Windows group logins  
CREATE USER   
    {   
          windows_principal [ { FOR | FROM } LOGIN windows_principal ]  
        | user_name { FOR | FROM } LOGIN windows_principal  
}  
    [ WITH <limited_options_list> [ ,... ] ]   
[ ; ]  
  
--Users that cannot authenticate   
CREATE USER user_name   
    {  
         WITHOUT LOGIN [ WITH <limited_options_list> [ ,... ] ]  
       | { FOR | FROM } CERTIFICATE cert_name   
       | { FOR | FROM } ASYMMETRIC KEY asym_key_name   
    }  
 [ ; ]  
  
<options_list> ::=  
      DEFAULT_SCHEMA = schema_name  
    | DEFAULT_LANGUAGE = { NONE | lcid | language name | language alias }  
    | SID = sid   
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ] ]  
  
<limited_options_list> ::=  
      DEFAULT_SCHEMA = schema_name ]   
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ] ]  
  
-- SQL Database syntax when connected to a federation member  
CREATE USER user_name  
[;]  
```  

```  
-- Syntax for Azure SQL Data Warehouse  
  
CREATE USER user_name   
    [ { { FOR | FROM } { LOGIN login_name }   
      | WITHOUT LOGIN  
    ]   
    [ WITH DEFAULT_SCHEMA = schema_name ]  
[;]

CREATE USER Azure_Active_Directory_principal FROM EXTERNAL PROVIDER  
    [ WITH DEFAULT_SCHEMA = schema_name ]  
[;]
``` 
  
```  
-- Syntax for Parallel Data Warehouse  
  
CREATE USER user_name   
    [ { { FOR | FROM }  
      {   
        LOGIN login_name   
      }   
      | WITHOUT LOGIN  
    ]   
    [ WITH DEFAULT_SCHEMA = schema_name ]  
[;]  
```  
  
## <a name="arguments"></a>引數  
 *user_name*  
 指定在這個資料庫內用來識別使用者的名稱。 *user_name*是**sysname**。 該名稱長度最多可達 128 個字元。 當建立依據 Windows 主體的使用者時，除非指定另一個使用者名稱，否則 Windows 主體名稱會成為使用者名稱。  
  
 登入*login_name*  
 指定目前建立之資料庫使用者的登入。 *login_name*必須是有效的登入伺服器。 可以是依據 Windows 主體 (使用者或群組) 的登入，或是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的登入。 當這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入進入資料庫時，它會取得正在建立之資料庫使用者的名稱和識別碼。 在建立對應從 Windows 主體的登入，使用格式**[***\<domainName >*  **\\**   *\<loginName >***]**。 如需範例，請參閱[語法摘要](#SyntaxSummary)。  
  
 如果 CREATE USER 陳述式是 SQL 批次中的唯一陳述式，Windows Azure SQL Database 會支援 WITH LOGIN 子句。 如果 CREATE USER 陳述式不是 SQL 批次中的唯一陳述式或是在動態 SQL 中執行，則不支援 WITH LOGIN 子句。  
  
 DEFAULT_SCHEMA = *schema_name*  
 指定在解析這個資料庫使用者的物件名稱時，伺服器所搜尋到的第一個結構描述。  
  
 '*windows_principal*'  
 為正在建立的資料庫使用者指定 Windows 主體。 *Windows_principal*可以是 Windows 使用者或 Windows 群組。 將會建立使用者即使*windows_principal*沒有登入。 當連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，如果*windows_principal*沒有登入，主體必須在進行驗證的 Windows[!INCLUDE[ssDE](../../includes/ssde-md.md)]透過 Windows 群組成員資格有登入，或連接字串必須指定在自主的資料庫做為初始目錄。 從 Windows 主體建立使用者，當使用格式**[***\<domainName >*  **\\**   *\<loginName >***]**。 如需範例，請參閱[語法摘要](#SyntaxSummary)。 根據 Active Directory 使用者，使用者會限制為小於 21 個字元的名稱。    
  
 '*Azure_Active_Directory_principal*'  
 **適用於**: [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]， [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]。  
  
 指定正在建立資料庫使用者的 Azure Active Directory 主體。 *Azure_Active_Directory_principal*可以是 Azure Active Directory 使用者或 Azure Active Directory 群組。 (Azure Active Directory 使用者中不能有 Windows 驗證登入[!INCLUDE[ssSDS](../../includes/sssds-md.md)]; 只有資料庫使用者。)連接字串必須指定自主的資料庫做為初始目錄。 

 對於使用者而言，您可以使用其主體的網域的完整別名。   
 
-   `CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;`  
  
-   `CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;`

 在您使用安全性群組、*顯示名稱*的安全性群組。 如*護士*安全性群組，您會使用：  
  
-   `CREATE USER [Nurses] FROM EXTERNAL PROVIDER;`  
  
 如需詳細資訊，請參閱 [使用 Azure Active Directory 驗證連線到 SQL 資料庫](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication)。  
  
密碼 = '*密碼*'  
 **適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 只能用於自主資料庫。 指定正在建立之使用者的密碼。 開頭為[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 預存密碼資訊會計算使用之 salt 的密碼 sha-512。  
  
WITHOUT LOGIN  
 指定使用者不對應到現有的登入。  
  
憑證*cert_name*  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 指定目前建立之資料庫使用者的憑證。  
  
非對稱金鑰*asym_key_name*  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 指定目前建立之資料庫使用者的非對稱金鑰。  
  
DEFAULT_LANGUAGE = *{NONE |\<lcid > |\<語言名稱 > |\<語言別名 >}*  
 **適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 指定新使用者的預設語言。 如果已指定使用者的預設語言，但稍後變更資料庫的預設語言，使用者預設語言會保持為指定值。 如果未指定預設語言，則使用者的預設語言將是資料庫的預設語言。 如果未指定使用者的預設語言，而稍後變更資料庫的預設語言，使用者的預設語言會變成資料庫的新預設語言。  
  
> [!IMPORTANT]  
>  *DEFAULT_LANGUAGE*只能用於自主的資料庫使用者。  
  
SID = *sid*  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 僅適用於具有密碼之自主資料庫使用者 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證)。 指定新資料庫使用者的 SID。 如果未選取這個選項，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將自動指派 SID。 使用 SID 參數即可在多個資料庫中建立具有相同識別 (SID) 的使用者。 若要準備 Alwayson 容錯移轉多個資料庫中建立使用者時，這非常有用。 若要判斷使用者的 SID，請查詢 sys.database_principals。  
  
ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ON |**OFF** ]]  
 **適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 隱藏在大量複製作業的伺服器上的密碼編譯中繼資料檢查。 這可讓資料表或資料庫之間大量複製加密的資料使用者，無須解密資料。 預設值為 OFF。  
  
> [!WARNING]  
>  不當使用這個選項會導致資料損毀。 如需詳細資訊，請參閱[移轉保護的敏感性資料透過永遠加密](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)。  
  
## <a name="remarks"></a>備註  
 如果省略了 FOR LOGIN，新的資料庫使用者就會對應至同名的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
 預設結構描述是伺服器在解析這個資料庫使用者之物件名稱時，所搜尋到的第一個結構描述。 除非另有指定，否則預設結構描述是此資料庫使用者建立之物件的擁有者。  
  
 如果使用者有預設結構描述，則使用預設結構描述。 如果使用者沒有預設結構描述，但使用者是有預設結構描述之群組的成員，則使用群組的預設結構描述。 如果使用者沒有預設結構描述，而且是有一個以上之群組的成員，使用者的預設結構描述將會是具有最低 principle_id 且明確設定預設結構描述之 Windows 群組的結構描述。 (您無法明確選取其中一個可用的預設結構描述當做慣用結構描述)。如果無法判斷使用者時，沒有預設結構描述**dbo**會使用結構描述。  
  
 DEFAULT_SCHEMA 可以在它所指向的結構描述建立之前設定。  
  
 當您建立對應到憑證或非對稱金鑰的使用者時，不能指定 DEFAULT_SCHEMA。  
  
 如果使用者是系統管理員 (sysadmin) 固定伺服器角色的成員，則會忽略 DEFAULT_SCHEMA 的值。 系統管理員 (sysadmin) 固定伺服器角色的所有成員都有預設的 `dbo` 結構描述。  
  
 WITHOUT LOGIN 子句會建立沒有對應至 SQL Server 登入的使用者。 這個使用者可以用 guest 的身分連接到其他資料庫。 可指派權限給這位沒有登入的使用者，而且在安全性內容變更為沒有登入的使用者時，原始使用者會收到沒有登入之使用者的權限。 請參閱範例[D.建立和使用的使用者沒有登入](#withoutLogin)。  
  
 只有對應到 Windows 主體的使用者可以包含反斜線字元 (**\\**)。  
  
 您不能以 CREATE USER 建立 guest 使用者，因為每一個資料庫都已經有 guest 使用者了。 您可以授與 guest 使用者 CONNECT 權限來啟用它，如下所示：  
  
```  
GRANT CONNECT TO guest;  
GO  
```  
  
 資料庫使用者的相關資訊會顯示在[sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)目錄檢視。  
  
##  <a name="SyntaxSummary"></a>語法摘要  
 **依據 master 登入的使用者**  
  
 下列清單顯示依據登入之使用者的可能語法。 未列出預設的結構描述選項。  
  
-   `CREATE USER [Domain1\WindowsUserBarry]`  
-   `CREATE USER [Domain1\WindowsUserBarry] FOR LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsUserBarry] FROM LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FOR LOGIN [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FROM LOGIN [Domain1\WindowsGroupManagers]`  
-   `CREATE USER SQLAUTHLOGIN`  
-   `CREATE USER SQLAUTHLOGIN FOR LOGIN SQLAUTHLOGIN`  
-   `CREATE USER SQLAUTHLOGIN FROM LOGIN SQLAUTHLOGIN`  
  
**在資料庫進行驗證的使用者**  
  
 下列清單顯示只能用於自主資料庫使用者的可能語法。 中的任何登入不相關的使用者建立**主要**資料庫。 未列出預設的結構描述和語言選項。  
  
> [!IMPORTANT]  
>  此語法將資料庫的存取權以及 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的新存取權授與使用者。  
  
-   `CREATE USER [Domain1\WindowsUserBarry]`  
-   `CREATE USER [Domain1\WindowsGroupManagers]`  
-   `CREATE USER Barry WITH PASSWORD = 'sdjklalie8rew8337!$d'`  
  
**依據沒有 master 登入的 Windows 主體的使用者**  
  
 下列清單顯示使用者的存取權的可能語法[!INCLUDE[ssDE](../../includes/ssde-md.md)]透過 Windows 群組，但沒有登入**主要**。 這個語法可以用於所有類型的資料庫。 未列出預設的結構描述和語言選項。  
  
 這個語法與依據 master 登入的使用者類似，但這個類別的使用者沒有 master 的登入。 使用者必須可透過 Windows 群組登入來存取 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
 這個語法與依據 Windows 主體的自主資料庫使用者類似，但這個類別的使用者沒有 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的新存取權。  
  
-   `CREATE USER [Domain1\WindowsUserBarry]`  
-   `CREATE USER [Domain1\WindowsUserBarry] FOR LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsUserBarry] FROM LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FOR LOGIN [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FROM LOGIN [Domain1\WindowsGroupManagers]`  
  
**無法驗證的使用者**  
  
 下列清單顯示無法登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之使用者的可能語法。  
  
-   `CREATE USER RIGHTSHOLDER WITHOUT LOGIN`  
-   `CREATE USER CERTUSER FOR CERTIFICATE SpecialCert`  
-   `CREATE USER CERTUSER FROM CERTIFICATE SpecialCert`  
-   `CREATE USER KEYUSER FOR ASYMMETRIC KEY SecureKey`  
-   `CREATE USER KEYUSER FROM ASYMMETRIC KEY SecureKey`  
  
## <a name="security"></a>安全性  
 建立使用者會授與資料庫存取權，但不會自動授與資料庫物件的任何存取權。 在建立使用者之後，一般動作是將使用者加入至有權存取資料庫物件的資料庫角色，或將物件權限授與使用者。 如需設計權限系統的資訊，請參閱 [資料庫引擎權限使用者入門](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)。  
  
### <a name="special-considerations-for-contained-databases"></a>適用於自主資料庫的特殊考量  
 如果使用者沒有登入自主資料庫中，連接時**主要**資料庫中，連接字串必須包含自主的資料庫名稱做為初始目錄。 具有密碼之自主資料庫使用者永遠需要初始目錄參數。  
  
 在自主資料庫中，建立使用者有助於區隔資料庫與 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，以便輕易將資料庫移至另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 如需詳細資訊，請參閱[自主資料庫](../../relational-databases/databases/contained-databases.md)和[自主資料庫使用者-使資料庫可攜](../../relational-databases/security/contained-database-users-making-your-database-portable.md)。 若要變更資料庫使用者從依據的使用者[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證登入自主的資料庫使用者與密碼，請參閱[sp_migrate_user_to_contained &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md).  
  
 在自主資料庫中，使用者並不需要有登入**主要**資料庫。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 管理員應該了解自主資料庫存取權可在資料庫層級授與，而非 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 層級。 如需詳細資訊，請參閱 [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md)。  
  
 當您使用自主的資料庫使用者時[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，使用資料庫層級防火牆規則來設定存取，而非使用伺服器層級防火牆規則。 如需詳細資訊，請參閱[sp_set_database_firewall_rule &#40;Azure SQL Database &#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md).
 
如[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]和[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]自主的資料庫使用者，SSMS 可以支援多因素驗證。 如需詳細資訊，請參閱 [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/)(SQL 資料庫和 SQL 資料倉儲的 Azure AD MFA SSMS 支援)。  
  
### <a name="permissions"></a>Permissions  
 需要資料庫的 ALTER ANY USER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-database-user-based-on-a-sql-server-login"></a>A. 依據 SQL Server 登入建立資料庫使用者  
 下列範例會先建立一個名為 `AbolrousHazem` 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，然後在 `AbolrousHazem` 建立對應的資料庫使用者 `AdventureWorks2012`。  
  
```  
CREATE LOGIN AbolrousHazem   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
```   
變更使用者資料庫。 例如，在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用`USE AdventureWorks2012`陳述式。 在[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，您必須建立新的連接，使用者資料庫。

```   
CREATE USER AbolrousHazem FOR LOGIN AbolrousHazem;  
GO   
```  
  
### <a name="b-creating-a-database-user-with-a-default-schema"></a>B. 以預設的結構描述建立資料庫使用者  
 下列範例會先建立一個具有密碼且名叫 `WanidaBenshoof` 的伺服器登入，然後再以預設的結構描述 `Wanida`，建立對應的資料庫使用者 `Marketing`。  
  
```  
CREATE LOGIN WanidaBenshoof   
    WITH PASSWORD = '8fdKJl3$nlNv3049jsKK';  
USE AdventureWorks2012;  
CREATE USER Wanida FOR LOGIN WanidaBenshoof   
    WITH DEFAULT_SCHEMA = Marketing;  
GO  
```  
  
### <a name="c-creating-a-database-user-from-a-certificate"></a>C. 從憑證建立資料庫使用者  
 下列範例會從憑證 `JinghaoLiu` 建立一個資料庫使用者 `CarnationProduction50`。  
  
**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
USE AdventureWorks2012;  
CREATE CERTIFICATE CarnationProduction50  
    WITH SUBJECT = 'Carnation Production Facility Supervisors',  
    EXPIRY_DATE = '11/11/2011';  
GO  
CREATE USER JinghaoLiu FOR CERTIFICATE CarnationProduction50;  
GO   
```  
  
###  <a name="withoutLogin"></a> D. 建立及使用不含登入的使用者  
 下列範例會建立未對應至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的資料庫使用者 `CustomApp`。 然後此範例會授與使用者 `adventure-works\tengiz0` 權限來模擬 `CustomApp` 使用者。  
  
```  
USE AdventureWorks2012 ;  
CREATE USER CustomApp WITHOUT LOGIN ;  
GRANT IMPERSONATE ON USER::CustomApp TO [adventure-works\tengiz0] ;  
GO   
```  
  
 若要使用 `CustomApp` 認證，使用者 `adventure-works\tengiz0` 會執行下列陳述式。  
  
```  
EXECUTE AS USER = 'CustomApp' ;  
GO  
```  
  
 若要還原回 `adventure-works\tengiz0` 認證，使用者會執行下列陳述式。  
  
```  
REVERT ;  
GO  
```  
  
### <a name="e-creating-a-contained-database-user-with-password"></a>E. 建立具有密碼的自主資料庫使用者  
 下列範例會建立具有密碼之自主資料庫使用者。 您只能在自主資料庫中執行這個範例。  
  
**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 如果 DEFAULT_LANGUAGE 已移除，則這個範例才能運作[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE USER Carlo  
WITH PASSWORD='RN92piTCh%$!~3K9844 Bl*'  
    , DEFAULT_LANGUAGE=[Brazilian]  
    , DEFAULT_SCHEMA=[dbo]  
GO   
```  
  
### <a name="f-creating-a-contained-database-user-for-a-domain-login"></a>F. 為網域登入建立自主資料庫使用者  
 下列範例會為 Contoso 網域中的登入 Fritz，建立自主資料庫使用者。 您只能在自主資料庫中執行這個範例。  
  
**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE USER [Contoso\Fritz] ;  
GO   
```  
  
### <a name="g-creating-a-contained-database-user-with-a-specific-sid"></a>G. 建立具有指定 SID 之自主資料庫使用者  
 下列範例會建立名稱為 CarmenW 的 SQL Server 驗證自主資料庫使用者。 您只能在自主資料庫中執行這個範例。  
  
**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE USER CarmenW WITH PASSWORD = 'a8ea v*(Rd##+'  
, SID = 0x01050000000000090300000063FF0451A9E7664BA705B10E37DDC4B7;  
  
```  
  
### <a name="h-creating-a-user-to-copy-encrypted-data"></a>H. 建立要複製加密的資料使用者  
 下列範例會建立包含加密的資料行，以另一組具有加密資料行 （位於相同或不同的資料庫） 的資料表可以複製資料從某一組資料表，「 永遠加密 」 功能所保護的使用者。  如需詳細資訊，請參閱[移轉保護的敏感性資料透過永遠加密](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)。  
  
**適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
```  
CREATE USER [Chin]   
WITH   
      DEFAULT_SCHEMA = dbo  
    , ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = ON ;  
```  
  

## <a name="next-steps"></a>後續的步驟  
一旦建立使用者時，請考慮將使用者加入至資料庫角色使用[ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md)陳述式。  
您可能也要[GRANT 物件權限](../../t-sql/statements/grant-object-permissions-transact-sql.md)至角色，讓他們可以存取的資料表。 如需 SQL Server 安全性模型的一般資訊，請參閱[權限](../../relational-databases/security/permissions-database-engine.md)。   
  
## <a name="see-also"></a>請參閱＜  
 [建立資料庫使用者](../../relational-databases/security/authentication-access/create-a-database-user.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [ALTER USER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-user-transact-sql.md)   
 [卸除使用者 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [自主資料庫](../../relational-databases/databases/contained-databases.md)   
 [使用 Azure Active Directory 驗證連接到 SQL 資料庫](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication)   
 [資料庫引擎權限使用者入門](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
  



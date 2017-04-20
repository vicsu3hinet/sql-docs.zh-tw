---
title: "複寫代理程式安全性模型 | Microsoft Docs"
ms.custom: ""
ms.date: "10/07/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Snapshot Agent, security"
  - "agents [SQL Server replication], security"
  - "Distribution Agent, security"
  - "logins [SQL Server replication], permissions for agents"
  - "security [SQL Server replication], agent security model"
  - "Log Reader Agent, security"
  - "Queue Reader Agent, security"
  - "Merge Agent, security"
  - "複寫 [SQL Server], 代理程式和設定檔"
ms.assetid: 6d09fc8d-843a-4a7a-9812-f093d99d8192
caps.latest.revision: 72
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 72
---
# 複寫代理程式安全性模型
  複寫代理程式安全性模型允許精確控制複寫代理程式執行並建立連接所使用的帳戶：您可為每個代理程式指定不同的帳戶。 如需如何指定帳戶的詳細資訊，請參閱 [管理登入和密碼的複寫](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)。  
  
> [!IMPORTANT]  
>  當 **系統管理員 (sysadmin)** 固定伺服器角色的成員設定複寫時，複寫代理程式可以設定為模擬 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 帳戶。 完成這項作業的方法，就是不指定複寫代理程式的登入和密碼；不過，我們不建議此方式。 反之，就安全性最佳做法而言，我們建議您為每個具有最小權限的代理程式指定帳戶；本主題稍後的＜代理程式所需的權限＞一節會描述最小權限。  
  
 跟所有可執行檔一樣，複寫代理程式也是在 Windows 帳戶的內容下執行。 代理程式會利用此帳戶來建立「Windows 整合式安全性」連接。 執行代理程式所使用的帳戶取決於代理程式的啟動方式：  
  
-   從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 作業啟動代理程式 (預設值)：當 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理程式作業用來啟動複寫代理程式時，代理程式會在您設定複寫時指定的帳戶內容下執行。 如需有關 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 和複寫的詳細資訊，請參閱本主題稍後的＜SQL Server Agent 下的代理程式安全性＞一節。 如需有關權限資訊所需的帳戶所在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行代理程式，請參閱 [設定 SQL Server Agent](../../../ssms/agent/configure-sql-server-agent.md)。  
  
-   從 MS-DOS 命令列直接啟動代理程式或透過指令碼啟動代理程式：代理程式會在特定使用者帳戶內容下執行，該特定帳戶就是在命令列執行代理程式的帳戶。  
  
-   從使用 Replication Management Objects (RMO) 或 ActiveX 控制項的應用程式啟動代理程式：代理程式會在呼叫 RMO 或 ActiveX 控制項的應用程式的內容下執行。  
  
    > [!NOTE]  
    >  ActiveX 控制項已被取代。  
  
 我們建議您在 Windows 整合式安全性的內容下建立連接。 為了回溯相容性，您也可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安全性。 如需最佳作法的相關資訊，請參閱 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)。  
  
## 代理程式所需的權限  
 執行代理程式和建立連接所使用的帳戶需要多種權限。 下表描述這些權限。 我們建議每個代理程式均應使用不同的 Windows 帳戶執行，且帳戶應僅被授與所需權限。 如需有關發行集的存取清單 (PAL)，也就是代理程式的相關資訊，請參閱 [保護發行者](../../../relational-databases/replication/security/secure-the-publisher.md)。  
  
> [!NOTE]  
>  某些 Windows 作業系統中的「使用者帳戶控制」(UAC) 可以防止以管理員權限存取快照集共用。 因此，您必須針對快照集代理程式、散發代理程式和合併代理程式所使用的 Windows 帳戶，明確地授與快照集共用權限。 即使 Windows 帳戶是管理員群組的成員，也必須這麼做。 如需詳細資訊，請參閱 [保護快照集資料夾](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
|代理程式|Permissions|  
|-----------|-----------------|  
|快照集代理程式|在連接到散發者時，需使用執行代理程式的 Windows 帳戶。 這個帳戶必須：<br /><br /> -在最小值是成員 **db_owner** 散發資料庫中的固定的資料庫角色。<br /><br /> -具備快照集共用的讀取、寫入及修改權限。<br /><br /> <br /><br /> 請注意，此帳戶，是用來 *連接* 到 「 發行者 」 必須至少是屬於 **db_owner** 發行集資料庫中的固定的資料庫角色。|  
|記錄讀取器代理程式|在連接到散發者時，需使用執行代理程式的 Windows 帳戶。 此帳戶必須至少是成員的 **db_owner** 散發資料庫中的固定的資料庫角色。<br /><br /> 用來連接到 「 發行者 」 的帳戶必須至少是成員的 **db_owner** 發行集資料庫中的固定的資料庫角色。<br /><br /> 選取時 **sync_type** 選項 *僅支援複寫*, ，*的備份初始化*, ，或 *初始化從 lsn*, ，記錄讀取器代理程式必須在執行後執行 **sp_addsubscription**, ，以便設定指令碼會寫入散發資料庫。 記錄讀取器代理程式必須在屬於 **系統管理員 (sysadmin)** 固定伺服器角色成員的 Windows 帳戶底下執行。 當 **sync_type** 選項設定為 *自動*, ，所需的任何特殊的記錄讀取器代理程式動作。|  
|發送訂閱的散發代理程式|在連接到散發者時，需使用執行代理程式的 Windows 帳戶。 這個帳戶必須：<br /><br /> -在最小值是成員 **db_owner** 散發資料庫中的固定的資料庫角色。<br /><br /> -為 PAL 的成員。<br /><br /> -擁有快照集共用的讀取權限。<br /><br /> -如果訂閱是針對非 SQL Server 訂閱者，訂閱者之 OLE DB 提供者的安裝目錄上，就要擁有讀取權限。<br /><br /> -當複寫 LOB 資料，散發代理程式必須具有寫入權限複寫 **C:\Program Files\Microsoft SQL Server\XX\COMfolder** 其中 XX 代表執行個體識別碼。<br /><br /> <br /><br /> 請注意，此帳戶，是用來 *連接* 到訂閱者必須至少是屬於 **db_owner** 在訂閱資料庫中，固定資料庫角色或具有同等權限，如果訂閱是針對非 SQL Server 訂閱者。<br /><br /> 也請注意，當使用 `-subscriptionstreams >= 2` 散發代理程式，您也必須授與 **View Server State** 「 訂閱者 」 的權限，來偵測死結。|  
|提取訂閱的散發代理程式|在連接到訂閱者時，需使用執行代理程式的 Windows 帳戶。 此帳戶必須至少是成員的 **db_owner** 訂閱資料庫中的固定的資料庫角色。 用於連接散發者的帳戶必須：<br /><br /> -為 PAL 的成員。<br /><br /> -擁有快照集共用的讀取權限。<br /><br /> -當複寫 LOB 資料，散發代理程式必須具有寫入權限複寫 **C:\Program Files\Microsoft SQL Server\XX\COMfolder** 其中 XX 代表執行個體識別碼。<br /><br /> <br /><br /> 請注意，當使用 `-subscriptionstreams >= 2` 散發代理程式，您也必須授與 **的 View Server State** 「 訂閱者 」 的權限，來偵測死結。|  
|發送訂閱的合併代理程式|與發行者和散發者建立連接時，需使用代理程式執行時所用的 Windows 帳戶。 這個帳戶必須：<br /><br /> -在最小值是成員 **db_owner** 散發資料庫中的固定的資料庫角色。<br /><br /> -為 PAL 的成員。<br /><br /> -為與發行集資料庫中使用者相關聯的登入。<br /><br /> -擁有快照集共用的讀取權限。<br /><br /> <br /><br /> 請注意，若要使用的帳戶 *連接* 到訂閱者必須至少是屬於 **db_owner** 訂閱資料庫中的固定的資料庫角色。|  
|提取訂閱的合併代理程式|在連接到訂閱者時，需使用執行代理程式的 Windows 帳戶。 此帳戶必須至少是成員的 **db_owner** 訂閱資料庫中的固定的資料庫角色。 用於連接發行者和散發者的帳戶必須：<br /><br /> -為 PAL 的成員。<br /><br /> -為與發行集資料庫中使用者相關聯的登入。<br /><br /> -為與散發資料庫中使用者相關聯的登入。 使用者可以是 **Guest** 使用者。<br /><br /> -擁有快照集共用的讀取權限。|  
|佇列讀取器代理程式|在連接到散發者時，需使用執行代理程式的 Windows 帳戶。 此帳戶必須至少是成員的 **db_owner** 散發資料庫中的固定的資料庫角色。<br /><br /> 用來連接到 「 發行者 」 的帳戶必須至少是成員的 **db_owner** 發行集資料庫中的固定的資料庫角色。<br /><br /> 用來連接到 「 訂閱者 」 的帳戶必須至少是成員的 **db_owner** 訂閱資料庫中的固定的資料庫角色。|  
  
## SQL Server Agent 下的代理程式安全性  
 利用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 程序或 RMO 設定複寫時，依預設，會為每個代理程式建立 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 作業。 然後，代理程式將在作業步驟內容下執行，無論是連續執行、按排程執行，或者在需要時執行。 您可以在 **中的** [作業] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]資料夾下檢視這些作業。 下表列出各個作業名稱。  
  
|代理程式|作業名稱|  
|-----------|--------------|  
|快照集代理程式|**\< 發行者>-\< u>-\< 發行集>-\< 整數>**|  
|合併式發行集分割區的快照集代理程式|**Dyn_ \< 發行者>-\< u>-\< 發行集>-\< GUID>**|  
|記錄讀取器代理程式|**\< 發行者>-\< u>-\< 整數>**|  
|提取訂閱的合併代理程式|**\< 發行者>-\< u>-\< 發行集>-\< 訂閱者>-\< u>-\< 整數>**|  
|發送訂閱的合併代理程式|**\< 發行者>-\< u>-\< 發行集>-\< 訂閱者>-\< 整數>**|  
|發送訂閱的散發代理程式|**\< 發行者>-\< u>-\< 發行集>-\< 訂閱者>-\< 整數>***|  
|提取訂閱的散發代理程式|**\< 發行者>-\< u>-\< 發行集>-\< 訂閱者>-\< u>-\< GUID>***\*|  
|發送訂閱至非 SQL Server 訂閱者的散發代理程式|**\< 發行者>-\< u>-\< 發行集>-\< 訂閱者>-\< 整數>**|  
|佇列讀取器代理程式|**[\< 散發者>]。\< 整數>**|  
  
 \*對於 Oracle 發行集的發送訂閱，作業名稱是 **\< 發行者>-\< 發行者**> 而不是 **\< 發行者>-\< u>**。  
  
 \*\*對於 Oracle 發行集的提取訂閱，作業名稱是 **\< 發行者>-\< DistributionDatabase**> 而不是 **\< 發行者>-\< u>**。  
  
 在複寫設定期間，指定代理程式應在其下執行的帳戶。 但是，所有作業步驟均在 *Proxy*安全性內容下執行，因此複寫將為您指定的代理程式帳戶在內部執行下列對應：  
  
-   先利用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] [CREATE CREDENTIAL](../../../t-sql/statements/create-credential-transact-sql.md) 陳述式將帳戶對應至認證。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent Proxy 使用認證來儲存 Windows 使用者帳戶的相關資訊。  
  
-    [Sp_add_proxy](../../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md) 呼叫預存程序，以及認證用來建立 proxy...  
  
> [!NOTE]  
>  提供此資訊的目的，是為了協助您了解，利用適當的安全性內容執行代理程式時會涉及哪些項目。 您不應該直接與已建立的認證或 Proxy 互動。  
  
## 另請參閱  
 [複寫安全性最佳做法](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [安全性和保護 & #40。複寫 & #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)   
 [保護快照集資料夾](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
---
title: "設定 Database Engine 接聽多個 TCP 通訊埠 | Microsoft Docs"
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
  - "通訊埠 [SQL Server], 多個"
  - "表格式資料流 (TDS)"
  - "接聽多個通訊埠"
  - "端點 [SQL Server], TDS"
  - "新增通訊埠"
  - "表格式資料流"
  - "多個通訊埠"
ms.assetid: 8e955033-06ef-403f-b813-3d8241b62f1f
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# 設定 Database Engine 接聽多個 TCP 通訊埠
  此主題描述如何使用 SQL Server 組態管理員，在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中設定 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 於多個 TCP 通訊埠上接聽。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟用 TCP/IP 時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 將會在由 IP 位址及 TCP 通訊埠編號構成的連接點上接聽內送連接。下列程序會建立表格式資料流 (TDS) 端點，因此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將可以在其他 TCP 通訊埠上接聽。  
  
 必須建立第二個 TDS 端點的原因包括：  
  
-   設定防火牆以對特定子網路的本機用戶端電腦，限制存取預設端點。 建立該防火牆對網際網路公開的新端點，以及對伺服器支援團隊限制連接此端點的權限，為您的支援團隊維護 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的網際網路存取。  
  
-   在使用非統一記憶體存取 (NUMA) 時，相似化特定處理器的連接。  
  
 設定 TDS 端點包含下列步驟，您能夠以任意順序來完成：  
  
-   建立 TCP 通訊端的 TDS 端點，然後還原預設端點的存取權 (如有必要)。  
  
-   對想要的伺服器主體授與端點存取權。  
  
-   指定選取 IP 位址的 TCP 通訊埠編號。  
  
 如需預設 Windows 防火牆設定的詳細資訊以及影響 Database Engine、Analysis Services、Reporting Services 和 Integration Services 之 TCP 通訊埠的描述，請參閱[設定 Windows 防火牆以允許 SQL Server 存取](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
##  <a name="SSMSProcedure"></a>  
  
#### 建立 TDS 端點  
  
-   發出以下陳述式以為伺服器上所有可用的 TCP 位址，為通訊埠 1500 建立一個稱為 **CustomConnection** 的端點。  
  
    ```  
    USE master;  
    GO  
    CREATE ENDPOINT [CustomConnection]  
    STATE = STARTED  
    AS TCP  
       (LISTENER_PORT = 1500, LISTENER_IP =ALL)  
    FOR TSQL() ;  
    GO  
    ```  
  
 當您建立新的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 端點時，就會撤銷預設 TDS 端點的 **public** 連接權限。 如果預設端點需要存取 **public** 群組，請使用 `GRANT CONNECT ON ENDPOINT::[TSQL Default TCP] to [public];` 陳述式重新套用此權限。  
  
#### 授與端點的存取權  
  
-   發出以下陳述式以對公司網域的 SQLSupport，授與 **CustomConnection** 端點的存取權。  
  
    ```  
    GRANT CONNECT ON ENDPOINT::[CustomConnection] to [corp\SQLSupport] ;  
    GO  
    ```  
  
#### 設定 SQL Server Database Engine 接聽其他 TCP 通訊埠。  
  
1.  在 SQL Server 組態管理員中，展開 [SQL Server 網路組態]，然後按一下 [\<執行個體名稱> 的通訊協定]。  
  
2.  展開 [\<執行個體名稱> 的通訊協定]，然後按一下 [TCP/IP]。  
  
3.  在右窗格中，以滑鼠右鍵按一下您要啟用之已停用的 IP 位址，然後按一下 [啟用]。  
  
4.  以滑鼠右鍵按一下 [IPAll]，然後按一下 [內容]。  
  
5.  在 **[TCP 通訊埠]** 方塊中，輸入想要 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 接聽的通訊埠，並以逗號分隔。 在此範例中，如果列出預設通訊埠 1433，請輸入 **,1500** ，如此該方塊會讀為 **1433,1500**，然後按一下 [確定] 。  
  
    > [!NOTE]  
    >  如果未啟用所有 IP 位址上的通訊埠，請只有在想要的位址，以內容方塊設定其他通訊埠。 接著在主控台窗格中，以滑鼠右鍵按一下 [TCP/IP]，按一下 [內容]，然後在 [全部接聽] 方塊中選取 [否]。  
  
6.  在左窗格中，按一下 **[SQL Server 服務]**。  
  
7.  在右窗格中，以滑鼠右鍵按一下 [SQL Server \<執行個體名稱>]，然後按一下 [重新啟動]。  
  
     當 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 重新啟動時，錯誤記錄檔將會列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在接聽的通訊埠。  
  
#### 連接新的端點  
  
-   使用信任連接，並假設使用者是 [corp\SQLSupport] 群組的成員，在稱為 ACCT 的伺服器上發出以下陳述式，連接 SQL Server 之預設執行個體的 **CustomConnection** 端點。  
  
    ```  
    sqlcmd -SACCT,1500  
    ```  
  
## 另請參閱  
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [DROP ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-endpoint-transact-sql.md)   
 [GRANT 端點權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)   
 [將 TCP/IP 通訊埠對應到 NUMA 節點 &#40;SQL Server&#41;](../../database-engine/configure-windows/map-tcp-ip-ports-to-numa-nodes-sql-server.md)  
  
  
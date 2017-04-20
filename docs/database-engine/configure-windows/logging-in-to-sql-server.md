---
title: "登入 SQL Server | Microsoft Docs"
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
  - "SQL Server, 登入"
  - "服務 [SQL Server], 登入"
  - "TCP 連接字串"
  - "連接至 Database Engine"
  - "登入 [SQL Server], 關於登入"
  - "具名管道連接字串"
  - "登入 [SQL Server]"
  - "共用的記憶體連接字串"
  - "登入 [SQL Server]"
  - "登入 [SQL Server]"
ms.assetid: 77158a9a-d638-4818-90a1-cb2eb57df514
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# 登入 SQL Server
  您可以利用任何圖形化管理工具，或是從命令提示字元登入 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
 當您利用圖形化管理工具 (例如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) 登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，必要時會提示您輸入伺服器名稱、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和密碼。 若使用「Windows 驗證」登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則不需要在每次存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時提供 SQL Server 登入。 相反地，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會利用您的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶自動將您登入。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是以混合模式驗證 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 驗證模式) 執行，且您選擇使用「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證」來登入，則必須提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和密碼。 盡可能使用 Windows 驗證。  
  
> [!NOTE]  
>  安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時若使用區分大小寫的定序，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入也會區分大小寫。  
  
## 指定 SQL Server 名稱的格式  
 連接至 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體時，必須指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體是預設執行個體 (未命名的執行個體)，請指定已安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦名稱，或電腦的 IP 位址。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體是具名執行個體 (例如 SQLEXPRESS)，請指定已安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦名稱，或電腦的 IP 位址，並加入斜線和執行個體名稱。  
  
 下列範例連接至 APPHOST 電腦上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 指定具名執行個體時，範例會使用執行個體名稱 SQLEXPRESS。  
  
 **範例:**  
  
|執行個體類型|伺服器名稱的項目|  
|----------------------|-------------------------------|  
|使用預設通訊協定連接至預設執行個體  (這是預設執行個體的建議項目)。|APPHOST|  
|使用預設通訊協定連接至具名執行個體  (這是具名執行個體的建議項目)。|APPHOST\SQLEXPRESS|  
|使用句號連接至同一部電腦上的預設執行個體，指出執行個體是在本機電腦上執行。|。|  
|使用句號連接至同一部電腦上的具名執行個體，指出執行個體是在本機電腦上執行。|.\SQLEXPRESS|  
|使用 localhost 連接至同一部電腦上的預設執行個體，指出執行個體是在本機電腦上執行。|localhost|  
|使用 localhost 連接至同一部電腦上的具名執行個體，指出執行個體是在本機電腦上執行。|localhost\SQLEXPRESS|  
|使用 (local) 連接至同一部電腦上的預設執行個體，指出執行個體是在本機電腦上執行。|(local)|  
|使用 (local) 連接至同一部電腦上的具名執行個體，指出執行個體是在本機電腦上執行。|(local)\SQLEXPRESS|  
|連接至同一部電腦上的預設執行個體，會強制進行共用記憶體連線。|lpc:APPHOST|  
|連接至同一部電腦上的具名執行個體，會強制進行共用記憶體連接。|lpc:APPHOST\SQLEXPRESS|  
|使用 IP 位址，連接至接聽 TCP 位址 192.168.17.28 的預設執行個體。|192.168.17.28|  
|使用 IP 位址，連接至接聽 TCP 位址 192.168.17.28 的具名執行個體。|192.168.17.28\SQLEXPRESS|  
|指定正在使用的通訊埠 (在此情況下，是 2828)，以連接至未接聽預設 TCP 通訊埠的預設執行個體  (如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 接聽預設通訊埠 (1433)，則不需要進行此作業)。|APPHOST,2828|  
|連接至所指定 TCP 通訊埠 (在此情況下，是 2828) 的具名執行個體  (如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務不是在主機電腦上執行，通常會需要進行此作業)。|APPHOST,2828|  
|指定正在使用的 IP 位址和 TCP 通訊埠 (在此情況下，是 2828)，以連接至未接聽預設 TCP 通訊埠的預設執行個體。|192.168.17.28,2828|  
|指定正在使用的 IP 位址和 TCP 通訊埠 (在此情況下，是 2828)，以連接至具名執行個體。|192.168.17.28,2828|  
|依名稱連接至預設執行個體，強制進行 TCP 連接。|tcp:APPHOST|  
|依名稱連接至具名執行個體，強制進行 TCP 連接。|tcp:APPHOST\SQLEXPRESS|  
|指定具名管道名稱，以連接至預設執行個體。|\\\APPHOST\pipe\unit\app|  
|指定具名管道名稱，以連接至具名執行個體。|\\\APPHOST\pipe\MSSQL$SQLEXPRESS\SQL\query|  
|依名稱連接至預設執行個體，強制進行具名管道連接。|np:APPHOST|  
|依名稱連接至具名執行個體，強制進行具名管道連接。|np:APPHOST\SQLEXPRESS|  
  
## 驗證您的連接通訊協定  
 連接至 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 時，下列查詢會傳回用於目前連接的通訊協定和驗證方法 (NTLM 或 Kerberos)，並指出是否加密連接。  
  
```tsql  
SELECT net_transport, auth_scheme, encrypt_option   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
```  
  
## 相關工作  
 [登入 SQL Server 的執行個體 &#40;命令提示字元&#41;](../../database-engine/configure-windows/log-in-to-an-instance-of-sql-server-command-prompt.md)  
  
 下列資源可協助您疑難排解連接問題。  
  
-   [如何疑難排解與 SQL Server Database Engine 的連接](http://social.technet.microsoft.com/wiki/contents/articles/how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx)  
  
-   [疑難排解 SQL 連接性問題的步驟](http://blogs.msdn.com/b/sql_protocols/archive/2008/04/30/steps-to-troubleshoot-connectivity-issues.aspx)  
  
## 相關內容  
 [選擇驗證模式](../../relational-databases/security/choose-an-authentication-mode.md)  
  
 [使用 sqlcmd 公用程式](../../relational-databases/scripting/use-the-sqlcmd-utility.md)  
  
 [建立登入](../../t-sql/creating-a-login.md)  
  
  
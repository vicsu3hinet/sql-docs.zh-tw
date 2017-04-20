---
title: "散發代理程式安全性 (點對點複寫) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.p2pwizard.DA.f1"
ms.assetid: def6bf26-c640-4caf-ad30-05d1e649541d
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# 散發代理程式安全性 (點對點複寫)
   **散發代理程式安全性** 頁面可讓您指定的散發代理程式執行和連接到電腦的端對端拓撲中的帳戶。 代理程式和複寫安全性的最佳做法所需的權限的資訊，請參閱 [複寫代理程式安全性模型](../../relational-databases/replication/security/replication-agent-security-model.md) 和 [複寫安全性最佳作法](../../relational-databases/replication/security/replication-security-best-practices.md)。  
  
> [!NOTE]  
>  如果在上一回執行此精靈時，已為訂閱設定散發代理程式，您就無法變更其在此精靈中使用的認證。 如果您指定新認證，將會忽略這些認證。 若要變更認證，請使用 **訂閱屬性** 對話方塊。 如需詳細資訊，請參閱 [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
## 選項  
 按一下屬性按鈕 (**...**) 來存取每一個訂閱者資料列中 **散發代理程式安全性** 對話方塊。 按一下 [ **協助** 上 **散發代理程式安全性** 啟動的代理程式所使用的帳戶所需的權限的詳細資訊] 對話方塊。  
  
 在其中的一個對話方塊中輸入設定之後，訂閱者的連接資訊就會在方格中顯示。  
  
 **訂閱者的代理程式**  
 每個對等 (Peer) 的名稱。  
  
 **對等 (Peer) 資料庫**  
 對等 (Peer) 端的資料庫，會同時作為發行集資料庫與訂閱資料庫。  
  
 **散發者的連接**  
 用於連接到散發者的內容。 本機連接一律會使用執行代理程式之 Windows 帳戶的內容來進行。 此精靈會建立發送訂閱 （本機連接會連接到散發者），所以此欄位一律會顯示︰ **模擬 '\< 網域>\\< 登入\>'** 或 **模擬 '\< 電腦>\\< 登入\>'**。  
  
 **訂閱者的連接**  
 與訂閱者進行連接的內容。 連接可以使用執行代理程式之 Windows 帳戶的內容，或使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的內容來進行。 欄位會顯示下列其中之一︰ **使用登入 '\< 登入>'**, ，**模擬 '\< 網域>\\< 登入\>'** 或 **模擬 '\< 電腦>\\< 登入\>'**。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 使用 Windows 帳戶的內容進行所有連接的建議。  
  
## 另請參閱  
 [管理等式拓樸 & #40。複寫 TRANSACT-SQL 程式設計 & #41;](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [點對點異動複寫](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
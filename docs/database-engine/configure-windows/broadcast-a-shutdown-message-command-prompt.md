---
title: "廣播關機訊息 (命令提示字元) | Microsoft Docs"
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
  - "SQL Server, 停止"
  - "具名執行個體 [SQL Server], 廣播關機訊息"
  - "關機訊息廣播"
  - "廣播關機訊息"
  - "命令提示字元 [SQL Server], 廣播關機訊息"
  - "預設執行個體 [SQL Server], 廣播關機訊息"
  - "停止 SQL Server"
ms.assetid: 9f20ccd5-d952-431d-ba12-339911af9430
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# 廣播關機訊息 (命令提示字元)
  本主題描述如何在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中使用 **net send** 命令廣播關機訊息。 在訊息中包含要停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的時間，讓使用者能夠完成其工作。  
  
##  <a name="SSMSProcedure"></a>  
  
#### 若要廣播關閉訊息  
  
1.  在命令提示字元下，輸入：  
  
     **net send /users "message"**  
  
     **/users** 選項可指定將訊息傳送給連接到伺服器的所有使用者。  
  
> [!NOTE]  
>  **net send** 命令需要 Messenger 服務同時在傳送與接收電腦上執行。 Windows Server 2003 預設會停用 Messenger 服務。 如需有關 **net send**的詳細資訊，請參閱 Windows 文件。  
  
 在您的網路上，使用電子郵件或電話來連絡使用者可能會更加適合。 若要判斷目前有哪些使用者連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請使用活動監視器。 如需活動監視器的相關資訊，請參閱[活動監視器](../../relational-databases/performance-monitor/activity-monitor.md)和[開啟活動監視器 &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)。  
  
## 另請參閱  
 [啟動、停止、暫停、繼續、重新啟動 Database Engine、SQL Server Agent 或 SQL Server Browser 服務](../../database-engine/configure-windows/start, stop, pause, resume, restart sql server services.md)  
  
  
---
title: "資源管理員分類函數 | Microsoft Docs"
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
  - "資源管理員, 分類函數"
  - "使用者自訂函數 [SQL Server], 分類函數"
  - "分類函數 [SQL Server]"
  - "分類函數 [SQL Server], 概觀"
ms.assetid: 64c25012-7068-476f-afa2-0b4f3adde9a4
caps.latest.revision: 7
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 7
---
# 資源管理員分類函數
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源管理員分類程序會根據內送工作階段的特性，將工作階段指派給工作負載群組。 您可以透過撰寫使用者定義函數 (稱為分類函數) 來自訂分類邏輯。  
  
## 分類  
 資源管理員支援內送工作階段的分類。 分類是以函數中包含的一組使用者撰寫準則為基礎。 函數邏輯的結果可讓資源管理員將工作階段分類至現有的工作負載群組中。  
  
> [!NOTE]  
>  內部工作負載群組會填入僅供內部使用的要求。 您無法變更用於路由傳送這些要求的準則，而且無法將要求分類至內部工作負載群組中。  
  
 您可以撰寫純量函數，其中包含用來將內送工作階段指派給工作負載群組的邏輯。 您必須先完成下列動作，然後才能使用這個函數：  
  
-   使用 ALTER RESOURCE GOVERNOR 陳述式來建立並註冊此函數。 如需詳細資訊，請參閱 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)。  
  
-   使用 ALTER RESOURCE GOVERNOR 陳述式搭配 RECONFIGURE 參數來更新資源管理員組態。  
  
 在您建立此函數並套用組態變更之後，資源管理員分類就會使用此函數傳回的工作負載群組名稱，將新的要求傳送至適當的工作負載群組。  
  
> [!IMPORTANT]  
>  如果分類函數沒有在指定的登入逾時設定內完成，用戶端工作階段可能會逾時。 但是，登入逾時是用戶端屬性，因此伺服器不知道發生逾時。 長時間執行的分類函數可能會長期給伺服器留下遭遺棄的連接。 因此，請務必建立在連接逾時之前執行完成的分類函數。  
  
 使用者定義的函數具有下列特性和行為：  
  
-   系統會針對每個新的工作階段評估使用者定義函數，即使啟用了連接共用也一樣。  
  
-   使用者定義的函數會提供工作負載群組內容給工作階段。 決定群組成員資格之後，此工作階段就會在工作階段的存留期間繫結至工作負載群組。  
  
-   如果使用者定義的函數傳回 NULL、預設值或不存在群組的名稱，系統就會提供預設工作負載群組內容給此工作階段。 此外，如果這個函數由於任何原因而失敗，系統也會提供預設內容給此工作階段。  
  
-   您應該使用伺服器範圍 (master 資料庫) 來定義此函數。  
  
-   只有在 ALTER RESOURCE GOVERNOR RECONFIGURE 執行之後，使用者定義的分類函數指定才會生效。  
  
-   您一次只能指定一個使用者定義函數當做分類函數。  
  
-   除非分類狀態被移除，否則您無法卸除或更改使用者定義的分類函數。  
  
-   如果使用者定義的分類函數不存在，所有工作階段都會分類至預設群組中。  
  
-   分類函數所傳回工作負載群組位於結構描述繫結限制的範圍以外。 例如，雖然您無法卸除資料表，但是卻能夠卸除工作負載群組。  
  
> [!IMPORTANT]  
>  我們建議您在伺服器上啟用專用管理員連接 (DAC)。 DAC 不受資源管理員分類限制，而且可用來監視和疑難排解分類函數。 如需詳細資訊，請參閱[資料庫管理員的診斷連接](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)。 如果 DAC 無法用於疑難排解，其他選項就是在單一使用者模式中重新啟動系統。 雖然單一使用者模式不受分類限制，但是您無法在資源管理員分類執行時進行診斷。  
  
### 分類程序  
 在資源管理員的內容中，工作階段的登入程序包含下列步驟：  
  
1.  登入驗證  
  
2.  LOGON 觸發程序執行  
  
3.  分類  
  
 開始分類時，資源管理員就會執行分類函數並使用此函數所傳回的值，將要求傳送至適當的工作負載群組。  
  
> [!NOTE]  
>  [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) 和 [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) 中有公開執行分類函數和 LOGON 觸發程序的相關資訊。  
  
## 分類函數工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|描述如何建立和測試分類使用者定義函數。|[建立和測試分類使用者定義函數](../../relational-databases/resource-governor/create-and-test-a-classifier-user-defined-function.md)|  
  
## 另請參閱  
 [資源管理員](../../relational-databases/resource-governor/resource-governor.md)   
 [啟用資源管理員](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [資源管理員資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [資源管理員工作負載群組](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [使用範本來設定資源管理員](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)   
 [檢視資源管理員屬性](../../relational-databases/resource-governor/view-resource-governor-properties.md)  
  
  
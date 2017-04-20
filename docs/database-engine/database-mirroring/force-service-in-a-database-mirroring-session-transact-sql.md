---
title: "在資料庫鏡像工作階段中強制服務 (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "強制服務 [SQL Server]"
  - "資料庫鏡像 [SQL Server], 強制服務"
ms.assetid: 8b6ffe77-35f3-4e2a-a658-8a38a8e1c794
caps.latest.revision: 40
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 40
---
# 在資料庫鏡像工作階段中強制服務 (Transact-SQL)
  在高效能模式與不含自動容錯移轉的高安全性模式中，若主體伺服器失敗而鏡像伺服器可用，則資料庫擁有者就可以強制將服務容錯移轉到鏡像資料庫 (有遺失資料的可能)，讓資料庫成為可用。 只在下列所有狀況成立時才可使用此選項：  
  
-   主體伺服器已關閉。  
  
-   WITNESS 設定為 OFF，或連接到鏡像伺服器。  
  
> [!CAUTION]  
>  強制服務主要是一種損毀復原方法。 強制服務可能造成部分資料遺失。 因此，只有在您願意冒著遺失一些資料的風險來立即還原資料庫的服務時，才進行強制服務。 如果強制服務有遺失重要資料的風險，建議您停止鏡像並手動重新同步處理資料庫。 如需強制服務風險的詳細資訊，請參閱[資料庫鏡像作業模式](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)。  
  
 強制服務會暫停工作階段並啟動新的復原分岔。 強制服務的效果類似於移除鏡像並復原之前的主體資料庫。 不過，在鏡像繼續進行時，強制服務可方便您重新同步處理資料庫 (有遺失資料的可能)。  
  
### 若要在資料庫鏡像工作階段強制服務  
  
1.  連接鏡像伺服器。  
  
2.  發出下列陳述式：  
  
     ALTER DATABASE \<資料庫名稱> SET PARTNER FORCE_SERVICE_ALLOW_DATA_LOSS  
  
     其中 \<資料庫名稱> 是鏡像資料庫。  
  
     鏡像伺服器會立即轉換為主體伺服器，並暫停鏡像。  
  
## 另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [資料庫鏡像作業模式](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)  
  
  
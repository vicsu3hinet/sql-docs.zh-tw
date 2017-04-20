---
title: "設定追蹤篩選 (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "篩選 [SQL Server], 追蹤"
  - "追蹤 [SQL Server], 篩選"
ms.assetid: 7b976a84-7381-43a6-a828-ba83ada71cbe
caps.latest.revision: 20
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 20
---
# 設定追蹤篩選 (Transact-SQL)
  本主題描述如何使用預存程序來建立篩選，針對所追蹤的事件，只擷取您需要的資訊。  
  
### 若要設定追蹤篩選  
  
1.  如果追蹤已在執行，請指定 **@status = 0** 執行 **sp_trace_setstatus**，以停止追蹤。  
  
2.  執行 **sp_trace_setfilter** 以設定要從追蹤的事件中擷取的相關資訊類型。  
  
> [!IMPORTANT]  
>  不同於一般預存程序，所有 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 預存程序的參數 (**sp_trace_*xx***) 都有強制類型，而且不支援資料類型的自動轉換。 如果沒有依照引數描述所指定，以正確的輸入參數資料類型來呼叫這些參數，預存程序會傳回錯誤。  
  
## 另請參閱  
 [篩選追蹤](../../relational-databases/sql-trace/filter-a-trace.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [SQL Server Profiler 預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  